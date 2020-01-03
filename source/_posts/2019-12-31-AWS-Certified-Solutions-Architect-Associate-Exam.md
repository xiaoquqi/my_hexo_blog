---
title: AWS Certified Solutions Architect - Associate Exam
date: 2019-12-31 09:11:55
tags: [AWS, ACA Exam]
---

参考链接：https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-associate/view/

由于备考AWS ACA考试，所以从网上看到这套模拟试题，在学习过程中对试题进行系统性分析和记录。发现有很多问题答案并非十分准确，所以也尝试做出分析和更正。

<!-- more -->

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

## A company is launching an application that it expects to be very popular. The company needs a database that can scale with the rest of the application. The schema will change frequently. The application cannot afford any downtime for database changes. Which AWS service allows the company to achieve these objectives?

A. Amazon Redshift
B. Amazon DynamoDB
C. Amazon RDS MySQL
D. Amazon Aurora

Answer: B

* 分析：原网站给出的答案是A，但是经过分析觉得有些问题，这道题的几个关键词：scale with the rest of the application, schema will change frequently, cannot afford any downtime for database changes. 首先，schema总是变更，所以这里需要的非关系型数据库，排除C和D。Redshift是数据仓库，其实也是数据仓库，从第一点上就可以排除。另外从这个链接（http://braindump2go.hatenablog.com/entry/2019/11/05/123057）分析上，还有一点除了DynamoDB可以真正做到scale时候zero downtime，其他的都不行。所以原网站给出的答案是错误的。

## A Solution Architect is designing a disaster recovery solution for a 5 TB Amazon Redshift cluster. The recovery site must be at least 500 miles (805 kilometers) from the live site. How should the Architect meet these requirements?

A. Use AWS CloudFormation to deploy the cluster in a second region.
B. Take a snapshot of the cluster and copy it to another Availability Zone.
C. Modify the Redshift cluster to span two regions.
D. Enable cross-region snapshots to a different region.

Answer: D

* 参考链接：https://aws.amazon.com/cn/blogs/aws/automated-cross-region-snapshot-copy-for-amazon-redshift/

## A customer has written an application that uses Amazon S3 exclusively as a data store. The application works well until the customer increases the rate at which the application is updating information. The customer now reports that outdated data occasionally appears when the application accesses objects in Amazon S3. What could be the problem, given that the application logic is otherwise correct?

A. The application is reading parts of objects from Amazon S3 using a range header.
B. The application is reading objects from Amazon S3 using parallel object requests.
C. The application is updating records by writing new objects with unique keys.
D. The application is updating records by overwriting existing objects with the same keys.

Answer: D

* 分析：这道题也是争论很大的一道题，原网站答案为A。问题简单描述为客户端访问不到最新的数据，发生的时间点在于应用上传信息时候速率提高导致的，所以问题应该出现在写入的时候，这样排除A和B读取的问题。因为S3同一object永远是覆盖，所以最有可能的问题是在same key的情况下，所以选择D。

## A Solutions Architect is designing a new social media application. The application must provide a secure method for uploading profile photos. Each user should be able to upload a profile photo into a shared storage location for one week after their profile is created. Which approach will meet all of these requirements?

A. Use Amazon Kinesis with AWS CloudTrail for auditing the specific times when profile photos are uploaded.
B. Use Amazon EBS volumes with IAM policies restricting user access to specific time periods.
C. Use Amazon S3 with the default private access policy and generate pre-signed URLs each time a new site profile is created.
D. Use Amazon CloudFront with AWS CloudTrail for auditing the specific times when profile photos are uploaded.

Answer: C

## An application requires block storage for file updates. The data is 500 GB and must continuously sustain 100 MiB/s of aggregate read/write operations. Which storage option is appropriate for this application?

A. Amazon S3
B. Amazon EFS
C. Amazon EBS
D. Amazon Glacier

Answer: C

* 分析：没想到这道题原网站给出的答案是B，争议比较大，但是从题目描述需要Block Storage角度来看，选择C才是最合理的。这道题还需要进一步确认一下。

## A mobile application serves scientific articles from individual files in an Amazon S3 bucket. Articles older than 30 days are rarely read. Articles older than 60 days no longer need to be available through the application, but the application owner would like to keep them for historical purposes. Which cost-effective solution BEST meets these requirements?

A. Create a Lambda function to move files older than 30 days to Amazon EBS and move files older than 60 days to Amazon Glacier.
B. Create a Lambda function to move files older than 30 days to Amazon Glacier and move files older than 60 days to Amazon EBS.
C. Create lifecycle rules to move files older than 30 days to Amazon S3 Standard Infrequent Access and move files older than 60 days to Amazon Glacier.
D. Create lifecycle rules to move files older than 30 days to Amazon Glacier and move files older than 60 days to Amazon S3 Standard Infrequent Access.

Answer: C

* 分析：很明显的排除A和B，S3可以自定义规则，那么问题就是30天后和60天后需要哪种存储的问题了，根据题目C是明显正确的。

## An organization is currently hosting a large amount of frequently accessed data consisting of key-value pairs and semi-structured documents in their data center. They are planning to move this data to AWS. Which of one of the following services MOST effectively meets their needs?

A. Amazon Redshift
B. Amazon RDS
C. Amazon DynamoDB
D. Amazon Aurora

Answer: C

## A Lambda function must execute a query against an Amazon RDS database in a private subnet. Which steps are required to allow the Lambda function to access the Amazon RDS database? (Select two.)

A. Create a VPC Endpoint for Amazon RDS.
B. Create the Lambda function within the Amazon RDS VPC.
C. Change the ingress rules of Lambda security group, allowing the Amazon RDS security group.
D. Change the ingress rules of the Amazon RDS security group, allowing the Lambda security group.
E. Add an Internet Gateway (IGW) to the VPC, route the private subnet to the IGW.

Answer: BD

* 分析：又是原网站一道错题，原网站答案为AD。D选项是允许Lambda服务访问RDS，所以在进方向允许。
* 目前VPC支持Endpoint的服务：https://docs.aws.amazon.com/zh_cn/vpc/latest/userguide/vpc-endpoints.html

> Amazon API Gateway
> Amazon AppStream 2.0
> AWS App Mesh
> Amazon Athena
> AWS CloudFormation
> AWS CloudTrail
> Amazon CloudWatch
> Amazon CloudWatch Events
> Amazon CloudWatch Logs
> AWS CodeBuild
> AWS CodeCommit
> AWS CodePipeline
> AWS Config
> AWS DataSync
> Amazon EC2 API
> Elastic Load Balancing
> Amazon Elastic Container Registry
> Amazon Elastic Container Service
> AWS Glue
> AWS Key Management Service
> Amazon Kinesis Data Firehose
> Amazon Kinesis Data Streams
> Amazon Rekognition
> Amazon SageMaker 和 Amazon SageMaker 运行时
> Amazon SageMaker 笔记本
> AWS Secrets Manager
> AWS Security Token Service
> AWS Service Catalog
> Amazon SNS
> Amazon SQS
> AWS Systems Manager
> AWS Storage Gateway
> AWS Transfer for SFTP
> 其他 AWS 账户托管的终端节点服务
> 
> 网关终端节点是一个网关，作为您在路由表中指定的路由的目标，用于发往受支持的 AWS 服务的流量。支持以下 AWS 服务：
> Amazon S3
> DynamoDB

## (待实际环境验证)A Solutions Architect needs to build a resilient data warehouse using Amazon Redshift. The Architect needs to rebuild the Redshift cluster in another region. Which approach can the Architect take to address this requirement?

A. Modify the Redshift cluster and configure cross-region snapshots to the other region.
B. Modify the Redshift cluster to take snapshots of the Amazon EBS volumes each day, sharing those snapshots with the other region.
C. Modify the Redshift cluster and configure the backup and specify the Amazon S3 bucket in the other region.
D. Modify the Redshift cluster to use AWS Snowball in export mode with data delivered to the other region.

Answer: A

* 分析：又是一道错题，Redhift备份是通过S3实现的, 所以不存在B的情况，我个人有点倾向于C，但是A确实是Redshift在快照时默认的格式，可能是更容易恢复吧，这道题需要在实际环境进行一下验证。另外国际版本的Redshift和国内的应该比国内的高很多。

> 问：Amazon Redshift 如何备份数据？ 如何从备份中还原我的集群？
> 
> 在加载数据时，Amazon Redshift 会复制数据仓库集群内的所有数据并将其连续备份至 S3。Amazon Redshift 始终尝试维持至少三份数据（计算节点上的正本数据、副本数据和 Amazon S3 上的备份数据）。Redshift 还能将您的快照异步复制到另一个区域的 S3 中进行灾难恢复。
> 
> 默认情况下，Amazon Redshift 以一天的保留期启用数据仓库群集的自动化备份。您可将其配置为 35 天之久。
> 
> 免费备份存储受限于数据仓库群集中节点上的总存储大小，并仅适用于已激活的数据仓库群集。例如，如果您有 8TB 的数据仓库总存储大小，那么我们将提供最多 8TB 的备份存储而不另外收费。如果您想将备份保留期延长为超过一天，那么您可以使用 AWS 管理控制台或 Amazon Redshift API 来实现这一目的。有关自动快照的更多信息，请参阅《Amazon Redshift 管理指南》。Amazon Redshift 仅备份已更改的数据，因此大多数快照仅占用少量的免费备份存储。
> 
> 如果您需要还原备份，则可以在备份保留期内访问所有自动备份。在您选择某个要还原的备份后，我们将预置一个新的数据仓库集群并将数据还原至此集群中。

## A popular e-commerce application runs on AWS. The application encounters performance issues. The database is unable to handle the amount of queries and load during peak times. The database is running on the RDS Aurora engine on the largest instance size available. What should an administrator do to improve performance?

A. Convert the database to Amazon Redshift.
B. Create a CloudFront distribution.
C. Convert the database to use EBS Provisioned IOPS.
D. Create one or more read replicas.

Answer: C

* 分析：这道题我最开始选择的是D，但是评论区的一种解释有一定的道理：这个网站应用类型为电商，原题中没有很清楚说明queris and load的压力有多大，很可能我们建立了read replicas只能临时性解决问题，并不是一劳永逸的方式。并且根据https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Replication.html

> 因此，所有 Aurora 副本均返回相同的查询结果数据，且副本滞后时间非常短 - 通常远远少于主实例写入更新后的 100 毫秒。副本滞后因数据库更改速率而异。也就是说，在对数据库执行大量写入操作期间，您可能发现副本滞后时间变长。

如果读副本在这个延时上，很可能对业务系统造成很大的影响。

## A Solutions Architect is designing the architecture for a new three-tier web-based e-commerce site that must be available 24/7. Requests are expected to range from 100 to 10,000 each minute. Usage can vary depending on time of day, holidays, and promotions. The design should be able to handle these volumes, with the ability to handle higher volumes if necessary. How should the Architect design the architecture to ensure the web tier is cost-optimized and can handle the expected traffic? (Select two.)

A. Launch Amazon EC2 instances in an Auto Scaling group behind an ELB.
B. Store all static files in a multi-AZ Amazon Aurora database.
C. Create an CloudFront distribution pointing to static content in Amazon S3.
D. Use Amazon Route 53 to route traffic to the correct region.
E. Use Amazon S3 multi-part uploads to improve upload times.

Answer: AC

* 分析：A是很明显的，弹性伸缩，节约成本，其他几项和题干没有太多关系，所以选的C。

## A Solution Architect is designing a three-tier web application. The Architect wants to restrict access to the database tier to accept traffic from the application servers only. However, these application servers are in an Auto Scaling group and may vary in quantity. How should the Architect configure the database servers to meet the requirements?

A. Configure the database security group to allow database traffic from the application server IP addresses.
B. Configure the database security group to allow database traffic from the application server security group.
C. Configure the database subnet network ACL to deny all inbound non-database traffic from the application-tier subnet.
D. Configure the database subnet network ACL to allow inbound database traffic from the application-tier subnet.

Answer: B

* 分析：这好像又是一道错题，原给出的答案是C。首先要明确的一点是SG是工作在instance级别，NACL是在子网级别，SG默认全部Deny，NACL默认全部Allow。A不对的原因是insance在Auto Scaling里，IP地址是不固定的。D不对的原因是NACL默认全都是Allow的。其实本质上考察的是如何选择安全组还是网络防火墙的问题。不选择C的原因是因为配置NACL规则至少需要阻止和允许，而通过安全组只需要配置一条即可。但是也有一种声音认为题目中关键词restrict意味着需要deny流量。

> 问：VPC 中的安全组和 VPC 中的网络 ACL 有什么区别？
> 
> VPC 中的安全组指定允许传入或传出 Amazon EC2 实例的流量。网络 ACL 则在子网级别上运作，评估进出某个子网的流量。网络 ACL 可通过设置允许和拒绝规则来进行使用。Network ACL 不能筛选同一子网中实例之间的流量。此外，网络 ACL 执行无状态筛选，而安全组则执行有状态筛选。

## An Internet-facing multi-tier web application must be highly available. An ELB Classic Load Balancer is deployed in front of the web tier. Amazon EC2 instances at the web application tier are deployed evenly across two Availability Zones. The database is deployed using RDS Multi-AZ. A NAT instance is launched for Amazon EC2 instances and database resources to access the Internet. These instances are not assigned with public IP addresses. Which component poses a potential single point of failure in this architecture?

A. Amazon EC2
B. NAT instance
C. ELB Classic Load Balancer
D. Amazon RDS

Answer: B

* 分析：这道题竟然给出了C的答案，很意外。

> https://aws.amazon.com/articles/high-availability-for-amazon-vpc-nat-instances-an-example/
>
> Instances in a private subnet can access the Internet without exposing their private IP address by routing their traffic through a Network Address Translation (NAT) instance in a public subnet. A NAT instance, however, can introduce a single point of failure to your VPC's outbound traffic. This situation is depicted in the diagram below.

## A call center application consists of a three-tier application using Auto Scaling groups to automatically scale resources as needed. Users report that every morning at 9:00 AM the system becomes very slow for about 15 minutes. A Solution Architect determines that a large percentage of the call center staff starts work at 9:00 AM, so Auto Scaling does not have enough time to scale out to meet demand. How can the Architect fix the problem?

A. Change the Auto Scaling group's scale out event to scale based on network utilization.
B. Create an Auto Scaling scheduled action to scale out the necessary resources at 8:30 AM every morning.
C. Use Reserved Instances to ensure the system has reserved the right amount of capacity for the scale-up events.
D. Permanently keep a steady state of instances that is needed at 9:00 AM to guarantee available resources, but leverage Spot Instances.

Answer: B

* 分析：竟然又是一道错题，记得在AWS听过这道题的分析。原答案是A，但是可能并不是由于网络引起的访问缓慢。

## An e-commerce application is hosted in AWS. The last time a new product was launched, the application experienced a performance issue due to an enormous spike in traffic. Management decided that capacity must be doubled the week after the product is launched. Which is the MOST efficient way for management to ensure that capacity requirements are met?

A. Add a Step Scaling policy.
B. Add a Dynamic Scaling policy.
C. Add a Scheduled Scaling action.
D. Add Amazon EC2 Spot Instances.

Answer: B

* 分析：又是一道争议比较大的题目，争议最大的是C选项，因为题目中有几个词在暗示时间，但是又不明确。既然现有性能上无法应对高峰访问，那么从这个角度还是通过Dynamic配置一个规则进行动态规则最为有效。所以还是选择B。

## A customer owns a simple API for their website that receives about 1,000 requests each day and has an average response time of 50 ms. It is currently hosted on one c4.large instance. Which changes to the architecture will provide high availability at the LOWEST cost?

A. Create an Auto Scaling group with a minimum of one instance and a maximum of two instances, then use an Application Load Balancer to balance the traffic.
B. Recreate the API using Amazon API Gateway and use AWS Lambda as the service backend.
C. Create an Auto Scaling group with a maximum of two instances, then use an Application Load Balancer to balance the traffic.
D. Recreate the API using Amazon API Gateway and integrate the new API with the existing backend service.

Answer: A

* 分析：这道题有个陷阱，Simple API，确实如果在不考虑开发的前提下B确实是最佳选项，但是重构也是要花成本的。所以我坚持选A。

## A Solution Architect is designing an application that uses Amazon EBS volumes. The volumes must be backed up to a different region. How should the Architect meet this requirement?

A. Create EBS snapshots directly from one region to another.
B. Move the data to an Amazon S3 bucket and enable cross-region replication.
C. Create EBS snapshots and then copy them to the desired region.
D. Use a script to copy data from the current Amazon EBS volume to the destination Amazon EBS volume.

Answer: C

## A company is using an Amazon S3 bucket located in us-west-2 to serve videos to their customers. Their customers are located all around the world and the videos are requested a lot during peak hours. Customers in Europe complain about experiencing slow downloaded speeds, and during peak hours, customers in all locations report experiencing HTTP 500 errors. What can a Solutions Architect do to address these issues?

A. Place an elastic load balancer in front of the Amazon S3 bucket to distribute the load during peak hours.
B. Cache the web content with Amazon CloudFront and use all Edge locations for content delivery.
C. Replicate the bucket in eu-west-1 and use an Amazon Route 53 failover routing policy to determine which bucket it should serve the request to.
D. Use an Amazon Route 53 weighted routing policy for the CloudFront domain name to distribute the GET request between CloudFront and the Amazon S3 bucket directly.

Answer: B

* 分析：网站给出的答案竟然是D，但是B很明显是正确的。

## A Solutions Architect is designing a solution that includes a managed VPN connection. To monitor whether the VPN connection is up or down, the Architect should use:

A. an external service to ping the VPN endpoint from outside the VPC.
B. AWS CloudTrail to monitor the endpoint.
C. the CloudWatch TunnelState Metric.
D. an AWS Lambda function that parses the VPN connection logs.

Answer: C

> Monitoring VPN Tunnels Using Amazon CloudWatch(https://docs.aws.amazon.com/vpn/latest/s2svpn/monitoring-cloudwatch-vpn.html)

## A social networking portal experiences latency and throughput issues due to an increased number of users. Application servers use very large datasets from an Amazon RDS database, which creates a performance bottleneck on the database. Which AWS service should be used to improve performance?

A. Auto Scaling
B. Amazon SQS
C. Amazon ElastiCache
D. ELB Application Load Balancer

Answer: C

## A Solutions Architect is designing network architecture for an application that has compliance requirements. The application will be hosted on Amazon EC2 instances in a private subnet and will be using Amazon S3 for storing data. The compliance requirements mandate that the data cannot traverse the public Internet. What is the MOST secure way to satisfy this requirement?

A. Use a NAT Instance.
B. Use a NAT Gateway.
C. Use a VPC endpoint.
D. Use a Virtual Private Gateway.

Answer: C

> New – VPC Endpoint for Amazon S3(https://aws.amazon.com/cn/blogs/aws/new-vpc-endpoint-for-amazon-s3/)

## Developers are creating a new online transaction processing (OLTP) application for a small database that is very read-write intensive. A single table in the database is updated continuously throughout the day, and the developers want to ensure that the database performance is consistent. Which Amazon EBS storage option will achieve the MOST consistent performance to help maintain application performance?

A. Provisioned IOPS SSD
B. General Purpose SSD
C. Cold HDD
D. Throughput Optimized HDD

Answer: A

## A Solutions Architect is designing a log-processing solution that requires storage that supports up to 500 MB/s throughput. The data is sequentially accessed by an Amazon EC2 instance. Which Amazon storage type satisfies these requirements?

A. EBS Provisioned IOPS SSD (io1)
B. EBS General Purpose SSD (gp2)
C. EBS Throughput Optimized HDD (st1)
D. EBS Cold HDD (sc1)

Answer: C
