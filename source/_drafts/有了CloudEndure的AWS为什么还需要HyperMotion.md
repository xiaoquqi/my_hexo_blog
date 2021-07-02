title: 有了CloudEndure的AWS为什么还需要HyperMotion云迁移
author: 孙琦(Ray)
date: 2021-03-26 08:50:33
tags:
---
2021年3月，国内自主研发的云原生迁移软件HyperMotion正式登陆AWS中国区Marketplace。众所周知，在2019年初，AWS击败Google的竞争，斥资2.5亿美金完成对以色列云原生迁移与容灾公司CloudEndure的收购，使其成为AWS全资子公司，专注于用户Re-Host方式迁移至AWS。2020年，AWS逐步将CloudEndure引入中国，帮助中国用户能够更好的使用AWS中国区域节点。HyperMotion是一款由万博智云自主研发的云原生迁移工具，其理念与CloudEndure基本一致，通过与云原生能力的高度对接（包括API与资源使用方式），实现了全自动化迁移编排能力。那么为什么在有了强大的CloudEndure后，HyperMotion仍然能够以完整版本入选AWS Marketplace呢？本文就为您从技术角度全面解密CloudEndure和HyperMotion之前的共性和差异。

<!-- more -->

![upload successful](/images/pasted-269.png)

# 共性分析

## 软件架构

我们首先通过公开资料分析一下CloudEndure的软件架构，CloudEndure采用了传统容灾使用的CDP技术，让用户的I/O持续的复制到云侧。不同于传统容灾软件，CloudEndure核心的控制层是在控制端而非Agent侧，这就大大的提升了在数据流转过程中控制流程的灵活度。Agent只负责数据的读出和发送，而对数据如何利用完全在服务端控制，降低Agent设计的复杂程度。

在云上区域内，CloudEndure有一片临时区域，称为Staging Area，用于进行实际的数据接收，这里使用了一些轻量级的EC2主机，并且支持横向扩展。从图上我们不难发现，这台云主机背后挂载了多个EBS卷。本质上这些EC2充当了存储网关的角色，将云内资源和云外资源巧妙的结合在一起。与传统迁移软件还有一点区别在于，这些数据在数据传输过程中，并不需要1：1的预置EC2实例，而是通过EBS进行存储。这样设计的优势在于，用户的业务系统在正式接管或者验证前，并不需要为云主机资源买单，大幅度降低迁移或容灾的成本。

![upload successful](/images/pasted-270.png)

最后在真正进行迁移时，利用云上的编排能力，将卷生成为云主机，实现最终的业务系统上云过程，实现高度自动化的操作体验。


# 差异分析

## 操作体验

## 无代理模式

## 多云



