title: '[阿里云]使用DataQuotient 画像分析筛选优质基金'
author: 孙琦(Ray)
date: 2020-04-14 11:10:17
tags:
---
# 使用DataQuotient 画像分析筛选优质基金

该教程是阿里云帮助文档一部分，这里做了进一步完善：https://help.aliyun.com/document_detail/160711.html?spm=a2c4g.11174283.6.603.682fa00bJ7AHYK

# 需求描述

4433法则通过对同类基金（例如股票类基金）长期和短期的表现进行分析，为您在众多基金中筛选少数优质基金。

<pre>
4433法则如下：
4：代表近一年收益率排名前1/4的基金。
4：代表近两年、三年、五年以来，收益率排名前1/4的基金。
3：指近六个月收益率排名前1/3的基金。
3：指近三个月以来收益率排名前1/3的基金。
</pre>

本教程为您演示如何从当日的1126个股票类的基金产品中，筛选出符合4433法则的69条优质基金。

# 实现流程
![upload successful](/images/pasted-0.png)

## 准备数据
* 获取基金数据。
* 数据输入MaxCompute。

## 创建基金信息标签系统
* 新建实体
* 绑定标签

## 筛选并导出优质基金群体
* 同步标签至RDS
* 新建长期和短期表现较好群体
* 计算群体
* 导出优质基金列表

# 实现过程

## 前提条件
本教程基于DataQuotient 画像分析、MaxCompute和RDS产品，请确保您已购买该产品。

## 获取基础数据

根据教程提供的线索，从天天基金网获取了全部股票型基金的数据，脚本已经提交到Github上，有需要的可以直接拿过去用。

## 在MaxCompute导入数据

之前我并没有开通过MaxCompute服务，所以需要开通一下DataWorks，才能使用MaxCompute服务。

![upload successful](/images/pasted-1.png)

![upload successful](/images/pasted-2.png)

### 创建MaxCompute表


![upload successful](/images/pasted-3.png)

```
create table if not exists fund_profit_stocktype
( `fundid` bigint comment '基金编号',
 `fundname` string comment '基金名称',
 `latest3months` double comment '近三月',
 `latest6months` double comment '近六月',
 `latest1year` double comment '近一年',
 `latest2years` double comment '近两年',
 `latest3years` double comment '近三年',
 `currentyear` double comment '今年来',  
 `fromcreated` double comment '成立来',
) comment '基金信息' ;
```

### 导入数据

原有文档是通过DDL去创建的数据，由于我们已经将数据保存在CSV文件中，所以我们选择导入方式试一下。

![upload successful](/images/pasted-4.png)


![upload successful](/images/pasted-5.png)


![upload successful](/images/pasted-6.png)


![upload successful](/images/pasted-7.png)

不知道什么原因，下拉菜单选择并不生效，于是我决定将原有CSV无用字段全部删除，便于后续测试。删除字段的时候，发现我获取的数据并不包含近五年的项，但是包含成立以来的数据，所以对字段进行一下修改。上面的SQL是我修改过的。页面好像并没有删除表的功能，所以为了不影响测试，我重新建了一张表来导入数据。

![upload successful](/images/pasted-8.png)

## 关联云计算资源


![upload successful](/images/pasted-13.png)


![upload successful](/images/pasted-14.png)


![upload successful](/images/pasted-16.png)

## 标签管理


![upload successful](/images/pasted-9.png)


![upload successful](/images/pasted-10.png)

我用的主账号的AK/KS竟然提示我权限不足，需要添加这么多信息感觉不是特别方便，都是阿里云的资源感觉没有必要使用AK/KS去通讯吧？另外需要手动填写MaxCompute project这一点也不够友好。
![upload successful](/images/pasted-15.png)


![upload successful](/images/pasted-17.png)





### 关联MaxCompute表

![upload successful](/images/pasted-11.png)

无法看到MaxCompute下的表
![upload successful](/images/pasted-12.png)

![upload successful](/images/pasted-18.png)

![upload successful](/images/pasted-19.png)

![upload successful](/images/pasted-20.png)

字段绑定后无法删除
![upload successful](/images/pasted-21.png)

![upload successful](/images/pasted-22.png)

最开始显示为0，后来又显示出数据总量，但是根据上方提示，MaxCompute是不支持显示的。
![upload successful](/images/pasted-23.png)

![upload successful](/images/pasted-33.png)

![upload successful](/images/pasted-25.png)

## 筛选出优质基金群体

### 同步标签至RDS

![upload successful](/images/pasted-24.png)

![upload successful](/images/pasted-26.png)

![upload successful](/images/pasted-27.png)

![upload successful](/images/pasted-28.png)

![upload successful](/images/pasted-29.png)

![upload successful](/images/pasted-31.png)

![upload successful](/images/pasted-32.png)

### 群体画像

![upload successful](/images/pasted-30.png)

![upload successful](/images/pasted-34.png)

![upload successful](/images/pasted-35.png)

![upload successful](/images/pasted-36.png)

![upload successful](/images/pasted-37.png)

![upload successful](/images/pasted-38.png)

![upload successful](/images/pasted-39.png)

![upload successful](/images/pasted-40.png)