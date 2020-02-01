---
title: 'AWS Certified Solutions Architecture Associate Practice'
date: 2020-01-30 21:35:00
tags: [AWS, ACA Practice]
---

该模拟题出自AWS Practice，是付费后的模拟题，一共25道题，相对来说答案比较准确，答题正确率在76%，看中文的命题相对来说对理解题目内容更简单。

<!-- more -->

# 您在us-west-2中运行一个应用程序，它需要始终运行6个EC2实例。
该区域有三个可用区（us-west-2a，us-west-2b和us-west-2c)可以使用，如果us-west-2中的任何可用区变得不可用，以下哪种部署可以提供容错功能？（选择两顶◊)
A. 在us-west-2a中有2个 EC2实例，在us-west-2b中有2个 EC2实例，在us-west-2c中有2个 EC2实例
B. 在 us- west- 2 a中有3个 EC2实例，在us-west-2b中有3个 EC2实例，在us-west-2c中没有EC2实例
C. 在us-west-2a中有4个 EC2实例，在us-west-2b中有2个 EC2实例，在us-west-2c中有2个 EC2实例
D. 在 us- west- 2 a中有6个 EC2实例，在us-west-2b中有6个 EC2实例，在us-west-2c中没有EC2实例
E. 在us-west-2a中有3个 EC2实例，在us-west-2b中有3个 EC2实例，在us-west-2c中有3个 EC2实例

Answer: AB

# 一家咨询公司反复使用来自很多AMS服务（包括IAM，Amazon EC2, Amazon RDS，DynamoDB和Amazon VPC)的AMS资源为客户构建大型标准化架构。顾问们有每个架构的架构图，但让他们感到沮丧的是，无法使用这些架构图自动创建资源。 哪种服务会立即为组织带来好处?
A. Elastic Beanstalk
B. CloudFormation
C. AMS CodeBuild
D. AMS CodeDeploy

Answer: B

# (待确认)解决方案架构师正在设计一种解决方案以存储和存档公司文档，并确定Amazon Glacier是正确的解决方案。必须在发出检索请求后的10分钟内提供数据。
Amazon Glacier中的哪种功能可以帮助满足该要求？
A. 文件库锁定
B. 加速检索
c. 批量检索
D. 标准检索

Answer: B

# (待确认)一个组织的安全策略要求应用程序在写入到磁盘之前加密数据。
该组织应使用哪种解决方案以满足该要求？
A. AMS KMS API
B. AMS Certificate Manager
C. 具有 STS 的 API Gateway
D. IAM访问密钥

Answer: A

# (待确认)一家零售商每天将其交易数据库中的数据导出到S3存储捅中。该零售商的数据仓库团队希望将这些数据导入到VPC中的现有Amazon Redshift群集◊公司安全策略规定只能在VPC中传输这些数据。
以下哪种步骤组合满足安全策略要求？（选择两顶)
A. 启用 Amazon Redshift 增强 VPC 路由。
B. 创建集群安全组以允许Amazon Redshift集群访问Amazon S3
C. 在公有子网中创建NAT网关以允许Amazon Redshift集群访问Amazon S3
D. 创建并配置Amazon S3 VPC终端节点
E. 在私有子网中设置NAT网关以允许Amazon Redshift集群访问AmazonS3

Answer: CD

# 一家公司正在生成包含数百万行的大型数据集，必须能按列对这些数据集进行汇总◊将使用现有的商业智能工具生成日常报告。
哪种存储服务可满足这些要求？
A. Amazon Redshift
B. Amazon RDS
C. ElastiCache
D. DynamoDB

Answer: A

# (待确认)解决方案架构师正在设计一个活动注册网页；每次用户注册活动时，需要使用一个托管服务向用户发送文本消息。
架构师应使用哪种MS服务来实现该目的？
A. Amazon STS
B. Amazon SQS
C. Lambda
D. Amazon SNS

Answer: D

# (待确认)解决方案架构师正在设计一个共享服务，以便在Amazon ECS上托管来自很多客户的容器。这些容器将使用很多MS服务◊一个客户的容器无法访问其他客户的数据。
架构师应使用哪种解决方案以满足这些要求？
A. 任务的IAM角色
B. EC2实例的 IAM角色
C. EC2实例的 IAM实例配置文件
D. 安全组规则

Answer: B

# (待确认)一家公司正在将本地10 TB MySQL数据库迁移到MS◊该公司预计数据库大小将增加3倍，业务要求是副本的滯后时间必须保持在100毫秒以内。
哪种Amazon RDS引擎满足这些要求？
A. MySQL
B. Microsoft SQL Server
C. Oracle
D. Amazon Aurora

Answer: D

# 管理员在AMS中运行一个高可用应用程序◊管理员需要使用一个文件存储层，它可以在实例之间共享并能更轻松地扩展该应用平台。
哪种AMS服务可以执行该操作？
A. Amazon EBS
B. Amazon EFS
C. Amazon S3
D. Amazon EC2实例存储

Answer: B

# (待确认)一家公司托管一个流行的Web应用程序，它连接到在私有VPC子网中运行的Amazon RDS MySQL数据库实例，该子网是使用默认ACL设置创建的。仅允许使用SSL连接的客户访问Web服务器◊仅公有子网中的Web服务器可以访问该数据库。
哪种解决方案可满足这些要求而不会影响其他运行的应用程序？（选择两顶)
A. 在Web服务器的子网上创建一个网络ACL，允许HTTPS端口 443入站流量，并将源指定为0.0. 0.0/0。
B. 创建一个允许来自Anywhere (0.0.0.0/0)的 HTTPS端口 443入站流量的Web服务器安全组，并将其应用于Web服务器。
C. 创建一个允许MySQL端口 3306入站流量的数据库服务器安全组，并将源指定为一个Web服务器安全组。
D. 在数据库子网上创建一个网络ACL，允许Web服务器的MySQL端口 3306入站流量，并拒绝所有出站流量。
E. 创建一个允许HTTPS端口 443入站流量的数据库服务器安全组，并将源指定为一个Web服务器安全组。

Answer: BC

# (待确认)一个应用程序当前在Amazon EBS卷上存储所有数据。必须在多个可用区中永久备份所有EBS卷。
备份这些卷的最灵活方法是什么？
A. 定期创建EBS快照。
B. 启用EBS卷加密。
C. 创建脚本以将数据复制到EC2实例存储。
D. 在两个EBS卷之间镜像数据。

Answer: A

# 解决方案架构师正在开发一个文档共享应用程序，并需要使用一个存储层。该存储应提供自动版本控制支持，以便用户可以轻松回滚到以前的版本或恢复删除的文档。
哪种AMS服务可满足这些要求？
A. Amazon S3
B. Amazon EBS
C. Amazon EFS
D. Amazon Storage Gateway VTL

Answer: A

# (待确认)AWS中的一个数据处理应用程序必须从Internet服务中提取数据。解决方案架构师必须设计一种高可用解决方案以访问数据，并且不会对应用程序流量施加带宽限制。
哪种解决方案能满足这些要求？
A. 启动一个NAT网关并为0.0.0.0/0添加路由
B. 附加一个VPC终端节点并为0. 0. 0. 0/0添加路由
C. 附加一个Internet网关并为0.0.0.0/0添加路由
D. 在公有子网中部署NAT实例并为0. 0. 0. 0/0添加路由

Answer: C

# (待确认)在审查您的应用程序的Auto Scaling事件时，您注意到应用程序在同一小时内扩展和缩减多次。
您可以选择哪种设计选顶以在保持弹性的同时优化成本？（选择两顶)
A. 修改Auto Scaling组终止策略以先终止最老的实例。
B. 修改Auto Scaling组终止策略以先终止最新的实例。
C. 修改Auto Scaling组冷却计时器。
D. 修改Auto Scaling策略以使用计划的缩放操作。
E. 修改触发Auto Scaling缩减策略的CloudWatch警报周期。

Answer: BC

# (待确认)对于以下哪种工作负载，解决方案架构师应考虑使用Elastic Beanstalk?(选择两顶)
A. 使用Amazon RDS的Web应用程序
B. 企业数据仓库
C. 长时间运行的工作进程
D. 静态网站
E. 每晚运行一次的管理任务

Answer: AD

# (待确认)一家公司在AMS上运行一个服务，以便为笔记本电脑和手机上的图像提供异地备份。该解决方案必须支持数百万个客户，每个客户有数千张图像，很少会检索这些图像，但必须可以立即检索这些图像。
哪种是满足这些要求的最经济高效的存储选顶？
A. 具有加速检索的Amazon Glacier
B. Amazon S3标准-低频率访问
C. Amazon EFS
D. Amazon S3 标准

Answer: B

# (待确认)一个带有150 GB大小的关系数据库的应用程序在EC2实例上运行。该应用程序很少使用，但在早上和晚上会出现很小的高峰。
最经济高效的存储类型是什么？
A. Amazon EBS 预置 IOPS SSD
B. Amazon EBS吞吐量优化HDD
C. Amazon EBS 通用型 SSD
D. Amazon EFS

Answer: C

# 一个应用程序允许生产站点上传文件。然后，处理每个3 GB大小的文件以提取元数据，处理每个文件需要几秒钟的时间◊更新频率是无法预铡的-可能几小时内没有更新，然后同时上传几个文件。
哪种架构能以最经济高效的方式处理该工作负载？
A. 使用Kinesis数据传输流存储文件，并使用Uirtoda进行处理。
B. 使用SQS队列存储文件，然后，一组EC2实例访问该文件。
C. 将文件存储在EBS卷中，然后，其他EC2实例可以访问该文件以进行处理。
D. 将文件存储在S3存储捅中，并使用Amazon S3事件通知调用Lambda函数以处理该文件。

Answer: D

# 一家网站在ELB应用程序负载均衡器后面的多个EC2实例上运行。这些实例在跨多个可用区的Auto Scaling组中运行◊这些实例提供一些很大的文件（图像，PDF等)，这些文件存储在共享的Amazon EFS文件系统上。每次用户请求这些数字资产时，该公司需要避免从EC2实例中提供这些文件。
该公司应釆取哪些措施以改进网站的用户体验？
A. 将数字资产移到到Amazon Glacier中。
B. 使用CloudFront缓存静态内容。
C. 调整图像以使其变小。
D. 使用保留的EC2实例。

Answer: B

# 您正在Amazon EC2上部署一个应用程序，它必须调用AMS API。
应使用哪种方法可将凭证安全地传送到该应用程序？
A. 使用实例用户数据将API凭证传送到实例。
B. 将API凭证作为对象存储在Amazon S3中。
C. 将API凭证嵌入到JAR文件中。
D. 将IAM角色分配给EC2实例。

Answer: D

# (待确认)—个组织在MS上托管着一个多语言网站◊该网站是使用CloudFront提供服务的◊语言是在HTTP请求中指定的:
• http://dllllllabcdef8.cloudfront.net/main.html?language=de
• http://dllllllabcdef8.cloudfront.net/main.html?language=en
• http://dllllllabcdef8.cloudfront.net/main.html?language=es
应如何配置CloudFront以使用正确的语言提供缓存的数据？
A. 将Cookie转发到原始地址。
B. 基于查询字符串参数。
C. 在原始地址中缓存对象。
D. 提供动态内容。

Answer: B

# 解决方案架构师正在设计一个可高度扩展的系统以跟踪记录。记录必须保留三个月以便可立即下载，然后必须删除记录。
最适合该使用案例的决策是什么？
A. 将文件存储在Amazon EBS上，并创建一个生命周期策略以在三个月后删除这些文件。
B. 将文件存储在Amazon S3中，并创建一个生命周期策略以在三个月后删除这些文件。
C. 将文件存储在Amazon Glacier中，并创建一个生命周期策略以在三个月后删除这些文件。
D. 将文件存储在Amazon EFS上，并创建一个生命周期策略以在三个月后删除这些文件。

Answer: B

# 一个团队正在创建一个应用程序，它必须在高可用的数据存储中永久保存JSON文件并编制索引。尽管应用程序流量很高，但数据访问延迟必须保持一致。
该团队应该选择哪种服务？
A. Amazon EFS
B. Amazon RedShift
C. DynamoDB
D. AWS CloudFormation

Answer: C

# (待确认)一个应用程序在S3存储桶中读取和写入小对象。在完全部署该应用程序后，读取/写入流量会非常高。
架构师应如何最大限度地提高Amazon S3性能？
A. 在每个对象名称前面添加随机字符串。
B. 使用STANDARD_IA存储类
C. 在每个对象名称前面添加当前日期。
D. 在S3存储桶上启用版本控制。

Answer: A
