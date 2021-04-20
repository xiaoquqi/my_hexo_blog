title: 利用Docker快速搭建Gitlab平台
author: 孙琦(Ray)
date: 2021-04-13 14:24:39
tags:
---
因为之前的开源项目经验，所以一直延续使用了Gerrit项目，最早是在Android中，后来是在OpenStack中。但是随着时间发展，越来越多人开始投身于github流程中，Gitlab就是这方面开源项目的代表，所以为了让团队更加适应新形势的发展，所以搭建了一套Gitlab让团队进行体验。

# 基于Docker快速构建

如果是在本地使用Docker，我现在更愿意都写成docker-compose文件，这样方便以后重用。Gitlab使用容器化部署特别简便，