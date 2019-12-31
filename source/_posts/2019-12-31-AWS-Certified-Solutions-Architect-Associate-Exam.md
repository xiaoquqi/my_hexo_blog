---
title: AWS Certified Solutions Architect - Associate Exam
date: 2019-12-31 09:11:55
tags: [AWS, ACA Exam]
---

参考链接：https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-associate/view/

由于备考AWS ACA考试，所以从网上看到这套模拟试题，在学习过程中对试题进行系统性分析和记录。发现有很多问题答案并非十分准确，所以也尝试做出分析和更正。

<!- more -->

## A Solutions Architect is designing an application that will encrypt all data in an Amazon Redshift cluster. Which action will encrypt the data at rest?

A. Place the Redshift cluster in a private subnet.
B. Use the AWS KMS Default Customer master key.
C. Encrypt the Amazon EBS volumes.
D. Encrypt the data using SSL/TLS.

Answer: B

* 参考链接：https://docs.aws.amazon.com/redshift/latest/mgmt/working-with-db-encryption.html
* 分析：Amazon Redshift 使用加密密钥层次结构来加密数据库。您可以使用 AWS Key Management Service (AWS KMS) 或硬件安全模块 (HSM) 来管理该层次结构中的顶级加密密钥。Amazon Redshift 用于加密的流程因您管理密钥的方式而异。Amazon Redshift 自动与 AWS KMS 集成，而不与 HSM 集成。当您使用 HSM 时，必须使用客户端和服务器证书在 Amazon Redshift 和 HSM 之间配置受信任的连接。

## A website experiences unpredictable traffic. During peak traffic times, the database is unable to keep up with the write request. Which AWS service will help decouple the web application from the database?

A. Amazon SQS
B. Amazon EFS
C. Amazon S3
D. AWS Lambda

Answer: A

* 参考链接：https://aws.amazon.com/cn/sqs/faqs/
* 分析：关键词是unpredictable traffic, keep up with write request, decouple the web application, 所以通过消息队列服务可以让写入请求排队，从而实现前端应用和后端数据库的解耦。

## A legacy application needs to interact with local storage using iSCSI. A team needs to design a reliable storage solution to provision all new storage on AWS. Which storage solution meets the legacy application requirements?

A. AWS Snowball storage for the legacy application until the application can be re-architected.
B. AWS Storage Gateway in cached mode for the legacy application storage to write data to Amazon S3.
C. AWS Storage Gateway in stored mode for the legacy application storage to write data to Amazon S3.
D. An Amazon S3 volume mounted on the legacy application server locally using the File Gateway service.

Answer: C

* 分析：关键词是local stroage with iSCSI, 并且需要将所有新的存储用AWS提供，所以排除A选项；因为用到了iSCSI协议，所以S3使用文件网关方式也不适用，排除D；剩下的B和C区别在于存储模式，因为需要本地应用请求，所以需要使用存储模式，而不能用缓存模式，所以最终选择C。

## A Solutions Architect is designing an architecture for a mobile gaming application. The application is expected to be very popular. The Architect needs to prevent the Amazon RDS MySQL database from becoming a bottleneck due to frequently accessed queries. Which service or feature should the Architect add to prevent a bottleneck?

A. Multi-AZ feature on the RDS MySQL Database
B. ELB Classic Load Balancer in front of the web application tier
C. Amazon SQS in front of RDS MySQL Database
D. Amazon ElastiCache in front of the RDS MySQL Database

Answer: D

* 分析：该问题的关键在于bottleneck due to frequently accessed queries，查询变成瓶颈，可以使用ElastiCache服务作为缓存，降低读取频率解决问题。
