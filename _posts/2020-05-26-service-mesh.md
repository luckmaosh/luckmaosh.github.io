---
layout: post
title: service mesh
# subtitle:
date: 2020-05-27
categories: micro-service
tags: 微服务
cover: /assets/img/service-mesh-1680.png
---



## skywalking探针

skywalking是apache发布的分布式追踪服务，通过安装skywalking探针的方式采集数据。

## 部署方式
1.拷贝skywalking-agent目录到所需位置，探针包含整个目录，请不要改变目录结构
2.增加JVM启动参数，-javaagent:/path/to/skywalking-agent/skywalking-agent.jar。参数值为skywalking-agent.jar的绝对路径。


## service mesh 探针

## 做什么
收集服务网格内的数据

## 工作原理
Service Mesh探针从每个请求中收集遥测数据，因此它知道源，目的地，端点，延迟和状态。通过这些，后端可以通过将这些调用组合为行，并通过它们的传入请求将每个节点的度量组合起来，从而告诉整个拓扑图。后端从解析跟踪数据中请求相同的指标数据。因此，正确的表达是： 服务网格度量是精确的度量，即跟踪解析器生成的度量。他们是一样的。


## Istio 

Istio 作为 Service Mesh 领域的集大成者, 提供了流控, 安全, 遥测等模型, 其功能复杂, 模块众多, 有较高的学习和使用门槛。

Kubernetes（k8s）

Istio和k8s一样，都是作为微服务的服务管理。Kubernetes本身是支持微服务的架构，在Pod中部署微服务很合适，也已经解决了微服务的互访互通问题。但是对服务间访问的管理如服务的熔断、限流、动态路由、调用链追踪等都不在k8s的范围内，这就需要Istio来实现。

所以目前，最完美的答案就是在Kubernetes上叠加Istio这个好帮手。


![](https://tva1.sinaimg.cn/large/007S8ZIlly1gf6tjv4ro2j30x60hkwh8.jpg)


istio系统组件细化到进程级别
![](https://tva1.sinaimg.cn/large/007S8ZIlly1gf5yy7uzfxj318d0u0q80.jpg)


## k8s探针
Istio利用k8s的探针对service进行流量健康检查，有两种探针可供选择，分别是liveness和readiness:

liveness探针用来侦测什么时候需要重启容器。比如说当liveness探针捕获到程序运行时出现的一个死锁，这种情况下重启容器可以让程序更容易可用。

readiness探针用来使容器准备好接收流量。当所有容器都ready时被视为pod此时ready。比如说用这种信号来控制一个后端服务，当pod没有到ready状态时，服务会从负载均衡被移除。