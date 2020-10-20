title: 使用Kolla部署OpenStack Train版本
author: 孙琦(Ray)
date: 2020-09-23 19:08:25
tags:
---
开源版本的OpenStack+Ceph的组合已经日趋稳定，所以搭建一朵私有云环境的难度在逐步降低。当然OpenStack安装问题其实一直没有得到有效的解决，学习曲线非常陡峭。本文主要介绍基于Kolla项目使用容器化快速部署OpenStack方法，该部署方法已经在内部环境得到了多次验证，安装简便容易维护。

<!-- more -->


# 1、云平台规划

在实际环境中，我们在一台2U的超微四子星服务器上进行了部署。由于是内部使用的研发环境，为了节约成本，我们并没有部署高可靠方案，而是采用了一台作为控制节点+计算节点+存储节点，另外三台作为计算节点+存储节点的方式进行部署。

由于OpenStack最新的Ussari在使用Kolla部署时，不再支持CentOS 7版本，所以这里我们选定了上一个稳定版本Train版本进行部署。

## 硬件配置

硬件名称 | 配置规格 | 备注
--------- | ------------- | -------------
CPU | Intel(R) Xeon(R) CPU E5-2630 v4 @ 2.20GHz	x 2 | 共40线程
内存 | DDR4 2400 MHz 64GB	|
硬盘 | 板载64 GB x 1 <br/> 240 GB Intel SSD x 1 <br/> 1.2 TB SAS x 5 | 经过测试，由于板载64GB空间过小，在控制节点需要损失一块SAS盘空间用于root分区挂载
网卡 | 千兆 x 4 <br/> 万兆 x 4 <br/> IPMI x 1|

### 分区规划

| 磁盘 | 规划 | 备注 |
| -- | -- | -- |
| 64G | 系统盘 | 不要使用LVM分区 |
| SSD 240G | Ceph Journal<br> | 1块盘 |
| SAS 1.2 T | Ceph OSD | 5块盘 |


## 网络规划

### 交换机配置

* 我们默认采用了VLAN模式，所以无须在交换机上进行Trunk配置

### 网络规划

| 网卡 | 网络类型 | VLAN ID | 网段 | 说明 | 网关 | 备注 |
| -- | -- | -- | -- | -- | -- | -- |
|  | 管理网络 | 3 | 192.168.10.0/24 | OpenStack管理 | 192.168.10.1 | 192.168.10.201 - 204 |
|  | 存储网络 |  | 10.0.100.0/24 | Ceph网络 | 无需网关 | 10.0.100.201 -&nbsp;204 |
|  | External网络 | 3 | 192.168.10.0/24 | External网络 | 192.168.10.1 | 可分配地址192.168.10.100 - 192.168.10.200 |
|  | Tunnel网络 |  | 172.16.100.0/24 | VxLAN通讯网络 | <br data-mce-bogus="1"> | 172.16.100.201 - 204 |
| console | IPMI | 4 | 192.168.10.0/24 |  |  | 与管理网地址一一对应, 192.168.10.201 |

### 网卡配置

| 主机名 | em1(管理网地址) | em2(存储网) | em3(External网络) | em4(Tunnel网络) | 备注 |
| -- | -- | -- | -- | -- | -- |
| control201 | 192.168.10.201 | 10.0.100.201 | <pre style="line-height: 1.42857;"><span class="na">DEVICE</span><span class="o">=</span><span class="s">INTERFACE_NAME</span><br><span class="na">TYPE</span><span class="o">=</span><span class="s">Ethernet</span><br><span class="na">ONBOOT</span><span class="o">=</span><span class="s">"yes"</span><br><span class="na">BOOTPROTO</span><span class="o">=</span><span class="s">"none"</span></pre> | 172.16.100.201 |  |
| compute202 | 192.168.10.202 | 10.0.100.202 | <pre style="line-height: 1.42857;"><span class="na">DEVICE</span><span class="o">=</span><span class="s">INTERFACE_NAME</span><br><span class="na">TYPE</span><span class="o">=</span><span class="s">Ethernet</span><br><span class="na">ONBOOT</span><span class="o">=</span><span class="s">"yes"</span><br><span class="na">BOOTPROTO</span><span class="o">=</span><span class="s">"none"</span></pre> | 172.16.100.202 |  |
| compute203 | 192.168.10.203 | 10.0.100.203 | <pre style="line-height: 1.42857;"><span class="na">DEVICE</span><span class="o">=</span><span class="s">INTERFACE_NAME</span><br><span class="na">TYPE</span><span class="o">=</span><span class="s">Ethernet</span><br><span class="na">ONBOOT</span><span class="o">=</span><span class="s">"yes"</span><br><span class="na">BOOTPROTO</span><span class="o">=</span><span class="s">"none"</span></pre> | 172.16.100.203 |  |
| compute204 | 192.168.10.204 | 10.10.20.204 | <pre style="line-height: 1.42857;"><span class="na">DEVICE</span><span class="o">=</span><span class="s">INTERFACE_NAME</span><br><span class="na">TYPE</span><span class="o">=</span><span class="s">Ethernet</span><br><span class="na">ONBOOT</span><span class="o">=</span><span class="s">"yes"</span><br><span class="na">BOOTPROTO</span><span class="o">=</span><span class="s">"none"</span></pre> | 172.16.100.203 |  |

## OpenStack规划

### 安装组件

Ceph采用单独安装方式，这目前也是Kolla项目主推的方式，在U版本中已经彻底不支持通过Kolla安装Ceph了。我们主要安装OpenStack核心模块，另外安装的是日志收集ELK的相关模块，便于运维。

* Horizon
* Nova
* Keystone
* Cinder
* Glance
* Neutron
* Heat

# 2、部署准备

## 部署架构图

![upload successful](/images/pasted-60.png)

## 服务器前期准备

* BIOS配置：在BIOS中打开VT，并且正确配置IPMI地址，方便远程管理
* RAID配置：所有磁盘需要配置成NON-RAID模式
* 操作系统安装：
    * 使用CentOS 7光盘进行最小化安装
    * 不要使用LVM分区
    * 配置主机名
    * 配置第一块网卡，并配置自动启动
    
## 网卡配置

### em1
```
cat << EOF > /etc/sysconfig/network-scripts/ifcfg-em1
TYPE=Ethernet
BOOTPROTO=static
NAME=em1
DEVICE=em1
ONBOOT=yes
IPADDR=192.168.10.201
NETMASK=255.255.255.0
GATEWAY=192.168.10.1
DNS1=114.114.114.114
EOF
```

### em2
```
cat << EOF > /etc/sysconfig/network-scripts/ifcfg-em2
TYPE=Ethernet
BOOTPROTO=static
DEFROUTE=yes
NAME=em2
DEVICE=em2
ONBOOT=yes
IPADDR=10.0.100.201
NETMASK=255.255.255.0
EOF
```

### em3
```
cat << EOF > /etc/sysconfig/network-scripts/ifcfg-em3
TYPE=Ethernet
BOOTPROTO=static
NAME=em3
DEVICE=em3
ONBOOT=yes
IPADDR=172.16.100.201
NETMASK=255.255.255.0
EOF
```

### em4
```
cat << EOF > /etc/sysconfig/network-scripts/ifcfg-em4
TYPE=Ethernet
BOOTPROTO=none
NAME=em4
DEVICE=em4
ONBOOT=yes
EOF
```


# 3、安装步骤


## 控制节点准备

该节点承担了后续所有的部署流程，包括运行OpenStack Kolla和Ceph Deploy。

### 下载初始化脚本

目前已经将常用的操作写成了Ansible脚本。

```
yum install -y git
git clone https://github.com/xiaoquqi/my_ansible_playbooks

cd my_ansible_playbooks
# ansible<2.10
prepare_on_centos7.sh
```

### 修改hosts.ini文件

修改hosts.ini文件来初始化所有节点

```
# my_ansible_playbooks/hosts.ini
compute201 ansible_host=192.168.10.201 ip=192.168.10.201 ansible_user=root
compute202 ansible_host=192.168.10.202 ip=192.168.10.202 ansible_user=root
compute203 ansible_host=192.168.10.202 ip=192.168.10.203 ansible_user=root
compute204 ansible_host=192.168.10.202 ip=192.168.10.204 ansible_user=root
```

### 初始化节点

该步骤主要包含了，更新软件，修改主机名，增加/etc/hosts等操作。

```
./run_ansible.sh playbooks/bootstrap_centos7.yml
./run_ansible.sh playbooks/change_hostname.yml
./run_ansible.sh playbooks/update_etc_hosts.yml
```

### 安装Ceph Deploy

```
yum install -y python3-pip
pip3 install pecan werkzeug
```

```
cat << EOF > /etc/yum.repos.d/ceph.repo
[ceph-noarch]
name=Ceph noarch packages
baseurl=https://mirrors.aliyun.com/ceph/rpm-octopus/el7/noarch/
enabled=1
gpgcheck=1
type=rpm-md
gpgkey=https://mirrors.aliyun.com/ceph/keys/release.asc
EOF
```

```
yum makecache
yum install -y ceph-deploy
```


### 安装Kolla

```
sudo yum -y install python-devel libffi-devel gcc openssl-devel libselinux-python

export VENV_HOME=/root/venv
yum install -y python-virtualenv
virtualenv $VENV_HOME
source $VENV_HOME/bin/activate

pip install kolla-ansible

mkdir -p /etc/kolla
cp -r $VENV_HOME/share/kolla-ansible/etc_examples/kolla/* /etc/kolla

mkdir -p /root/kolla
cp $VENV_HOME/share/kolla-ansible/ansible/inventory/* .
```

## 部署Ceph

之前有一篇软文详细介绍了使用Ceph Deploy部署Ceph的方法，这里不再赘述，下面直接给出部署命令，这里我们只部署块服务。

```
mkdir -p /root/ceph
cd /root/ceph

export CEPH_DEPLOY_REPO_URL=https://mirrors.aliyun.com/ceph/rpm-octopus/el7
export CEPH_DEPLOY_GPG_URL=https://mirrors.aliyun.com/ceph/keys/release.asc

# 集群初始化，这一步会生成初始化的ceph.conf，可以配置网络等信息
ceph-deploy new compute201
ceph-deploy install compute201 compute202 compute203 compute204

# 初始化monitor，并收集keys
ceph-deploy mon create-initial
ceph-deploy admin compute201 compute202 compute203 compute204

ceph-deploy mgr create compute201

# 需要根据实际情况修改
ceph-deploy osd create --data /dev/vdc --block-db /dev/vdb --block-wal /dev/vdb compute201
ceph-deploy osd create --data /dev/vdc --block-db /dev/vdb --block-wal /dev/vdb compute202
ceph-deploy osd create --data /dev/vdc --block-db /dev/vdb --block-wal /dev/vdb compute203
ceph-deploy osd create --data /dev/vdc --block-db /dev/vdb --block-wal /dev/vdb compute204

# 检查集群状态
ceph -s
```

## OpenStack部署