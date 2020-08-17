---
layout: post
title: service mesh
# subtitle:
date: 2020-05-27
categories: micro-service
tags: 微服务
cover: /assets/img/service-mesh.png
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

Kubernetes（k8s）的主要概念包括：node（物理节点）、pod（一个pod里面有多个container）、container、service、process，更多时候它的名字会和docker联系在一起。也就是微服务部署，容器管理，进程管理，资源调度的功能。如果遇到资源不够的时候，k8s可以提供便利的伸缩扩容服务。

k8s也有service机制，像spring cloud的服务一样，可以做到服务发现，服务注册，负载均衡，通过服务名访问到服务实例。

K8s和微服务的关系，首先k8s不是微服务，微服务是一种架构，k8s是一个容器管理工具。其次，k8s支持微服务架构。

Kubernetes的Service基于每个节点的Kube-proxy从Kube-apiserver上获取Service和Endpoint的信息，并将对Service的请求经过负载均衡转发到对应的 Endpoint 上。但Kubernetes只提供了4层负载均衡能力，无法基于应用层的信息进行负载均衡，更不会提供应用层的流量管理，在服务运行管理上也只提供了基本的探针机制，并不提供服务访问指标和调用链追踪这种应用的服务运行诊断能力。

Istio和k8s一样，都是作为微服务的服务管理。Kubernetes本身是支持微服务的架构，在Pod中部署微服务很合适，也已经解决了微服务的互访互通问题。但是对服务间访问的管理如服务的熔断、限流、动态路由、调用链追踪等都不在k8s的范围内，这就需要Istio来实现。

所以目前，最完美的答案就是在Kubernetes上叠加Istio这个好帮手。K8s主外，Istio主内


![](https://tva1.sinaimg.cn/large/007S8ZIlly1gf6tjv4ro2j30x60hkwh8.jpg)


istio系统组件细化到进程级别
![](https://tva1.sinaimg.cn/large/007S8ZIlly1gf5yy7uzfxj318d0u0q80.jpg)

## Istio 基于K8s
### 统一服务发现

基于k8s的域名访问机制构建而成，自己不需要搭建Eureka了

## 

## k8s探针
Istio利用k8s的探针对service进行流量健康检查，有两种探针可供选择，分别是liveness和readiness:

liveness探针用来侦测什么时候需要重启容器。比如说当liveness探针捕获到程序运行时出现的一个死锁，这种情况下重启容器可以让程序更容易可用。

readiness探针用来使容器准备好接收流量。当所有容器都ready时被视为pod此时ready。比如说用这种信号来控制一个后端服务，当pod没有到ready状态时，服务会从负载均衡被移除。

## service mesh 服务网格

处理服务间的通信

微服务的架构，业务服务需要部署到非常多的服务节点，形成网格。Service Mesh会接管整个网络，在服务之间转发所有的请求，业务服务只关心业务逻辑，而不需要关心服务间的通信。服务间通讯的环节就从服务里面剥离出来，呈现出一个抽象的基础设施层。对应的服务间通讯相关的治理功能，如流量路由（根据权重或参数分流、负载均衡、黑白名单）、流量治理（熔断、限流、容错）、请求认证鉴权、调用拓扑等均在下沉的Service Mesh层实现，微服务研发者专注于业务研发本身即可。

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gf7599cdsyj30hs0bgq4u.jpg)


## Service Mesh核心价值
对于通常的业务微服务而言， Service Mesh所带来的核心价值可以总结为：

微服务基础设施下沉 —— 微服务架构支撑、网络通信、治理等相关能力下沉到基础设施层，业务部门无需投入专人开发与维护，可以有效降低微服务架构下研发与维护成本；
降低升级成本 —— Sidecar支持热升级，降低中间件和技术框架客户端、SDK升级成本；
语言无关 —— 提供多语言服务治理能力；
降低复杂测试、演练成本 —— 降低全链路压测、故障演练成本和业务侵入性。

从功能上讲，以Google、IBM主推的Istio框架为例，其对Service Mesh核心功能表述如下所示：
![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gf759v8a0ij322j0u0woy.jpg)

[参考](https://sq.163yun.com/blog/article/375816037999161344)


## sidecar
轻量级网络代理（Sidecar)

[文档](https://yq.aliyun.com/articles/707679)