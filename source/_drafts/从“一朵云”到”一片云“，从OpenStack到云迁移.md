title: 创业之路
author: 孙琦(Ray)
date: 2020-07-22 13:52:22
tags:
---
# 结“云”之路

2008年底，我还在摩托罗拉的手机事业部，受经济危机影响，摩托罗拉这家老牌的外企一蹶不振，卖楼的卖楼，裁员的裁员，最终新上任的CEO痛下屠刀，一刀砍下去，All in Anrdoid。后来的故事大家比较熟悉，虽然Android让摩托迎来了短暂的复兴之路，但是最终还是仍然卖身于Google，为了Android专利提供了强大的保护伞。

在发布安卓手机的同时，为了顺应当时的社交热，摩托还发布了一款Blur服务，简单来说就是社交聚合平台，因为那个时候APP还没有像今天这么成熟，所以用户可以通过Blur服务将自己多个社交账号绑定，在Blur上及时关注自己社交媒体的动态。当时为了支撑中国区的服务，特意在联通北土城的机房托管了几百台服务器。当时云的概念还没有这么普及，但从形态上说，Blur服务是一种很典型的SaaS服务，这也是我第一次和云来了一次亲密接触。

![upload successful](/images/pasted-51.png)

# 从PaaS到IaaS

2011年，我正式开始了云开发之旅，接触的第一个项目就是CloudFoundry，那时候的CloudFoundry还是归属于VMware，直到2013年的时候才成立的Pivotal。CloudFoundry是一个PaaS平台，提供了基于开发语言的平台。你只要根据开发规范进行简单的修改，就可以把你的应用运行在CloudFoundry上，同时CloudFoundry提供了服务的概念，你可以使用MySQL、MongoDB、Redis等。

虽然CloudFoundry提供了非常大的便利性，但是在当时仍然有很多问题困扰着我：

1、CloudFoundry提供的语言不少，像Java、Ruby、Python、PHP等，但是相较于实际情况来说又存在很大的局限性。例如当时我们的公司有一些JBOSS的项目，就无法运行在CloudFoundry上。另外对于那些没有提供的支持的语言，想运行在CloudFoundry上就更难了。
2、服务的稳定性谁来保障？就拿MySQL来说，这个服务是属于CloudFoundry之外的，数据库的稳定性、高可靠性完全需要在外部去维护，CloudFoundry自身只是分配和调度。

由此可见，在当时还处于早期的中国云计算市场来说，CloudFoundry的概念还是超前了一些，在早些年也能听到一些金主对CloudFoundry的部署案例，但是终究在当年没有像后来的OpenStack一样大红大紫起来。

# 