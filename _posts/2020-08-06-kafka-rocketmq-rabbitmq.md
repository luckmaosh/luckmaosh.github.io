---
layout: post
title: 消息中间件对比
date: 2020-08-06
categories: java
tags: rabbitmq kafka rocketmq
---

# 消息队列对比

## 优点
- 解耦
- 削峰

## 缺点
- 降低可用性
- 增加系统复杂度


应用场景
那么,消息中间件性能究竟哪家强?

带着这个疑问,我们中间件测试组对常见的三类消息产品(Kafka、RabbitMQ、RocketMQ)做了性能比较。

Kafka

Kafka是LinkedIn开源的分布式发布-订阅消息系统，目前归属于Apache顶级项目。Kafka主要特点是基于Pull的模式来处理消息消费，追求高吞吐量，一开始的目的就是用于日志收集和传输。0.8版本开始支持复制，不支持事务，对消息的重复、丢失、错误没有严格要求，适合产生大量数据的互联网服务的数据收集业务。

RabbitMQ

RabbitMQ是使用Erlang语言开发的开源消息队列系统，基于AMQP协议来实现。AMQP的主要特征是面向消息、队列、路由（包括点对点和发布/订阅）、可靠性、安全。AMQP协议更多用在企业系统内，对数据一致性、稳定性和可靠性要求很高的场景，对性能和吞吐量的要求还在其次。

RocketMQ

RocketMQ是阿里开源的消息中间件，它是纯Java开发，具有高吞吐量、高可用性、适合大规模分布式系统应用的特点。RocketMQ思路起源于Kafka，但并不是Kafka的一个Copy，它对消息的可靠传输及事务性做了优化，目前在阿里集团被广泛应用于交易、充值、流计算、消息推送、日志流式处理、binglog分发等场景。

测试目的

对比Kafka、RabbitMQ、RocketMQ发送小消息(124字节)的性能。这次压测我们只关注服务端的性能指标,所以压测的标准是:

不断增加发送端的压力,直到系统吞吐量不再上升,而响应时间拉长。这时服务端已出现性能瓶颈,可以获得相应的系统最佳吞吐量。

测试场景

在同步发送场景中，三个消息中间件的表现区分明显：

Kafka

Kafka的吞吐量高达17.3w/s，不愧是高吞吐量消息中间件的行业老大。这主要取决于它的队列模式保证了写磁盘的过程是线性IO。此时broker磁盘IO已达瓶颈。

RocketMQ

RocketMQ也表现不俗，吞吐量在11.6w/s，磁盘IO %util已接近100%。RocketMQ的消息写入内存后即返回ack，由单独的线程专门做刷盘的操作，所有的消息均是顺序写文件。

RabbitMQ
RabbitMQ的吞吐量5.95w/s，CPU资源消耗较高。它支持AMQP协议，实现非常重量级，为了保证消息的可靠性在吞吐量上做了取舍。我们还做了RabbitMQ在消息持久化场景下的性能测试，吞吐量在2.6w/s左右。

测试结论

![](https://tva1.sinaimg.cn/large/007S8ZIlly1ghh31jyk16j30j50bcmxk.jpg)

在服务端处理同步发送的性能上，Kafka>RocketMQ>RabbitMQ。


## kafka topic的队列分布
![](https://tva1.sinaimg.cn/large/007S8ZIlly1ghh3nnnw7sj30hs093gmn.jpg)
