# 云原生的理解


## 如何理解云原生？
第一个话题：如何理解“云原生”？之所以将这个话题放在前面，是因为，这是对云原生概念的最基本的理解，而这会直接影响到后续的所有认知。

每个人对云原生的理解都可能不同，就如莎士比亚所说：一千个人眼中有一千个哈姆雷特。


CNCF（云原生基金会）2015年建立
他在2015年提出了这样的观点：

 -  应用容器化
 -  面向为微服务架构
 -  支持容器的编排调度

 2018年更新，除了之前的东西还新增：
 
 - 服务网格（我理解就是服务编排）
 - 不可变基础设施
 - 声明式API （）
 
 这边引用网上关于云原生所需要的能力和特征总结，如下图。
![](https://tva1.sinaimg.cn/large/006tNbRwly1gax157n2qfj30zk0n70w2.jpg)


 cncf的云生态大图
 ![](https://tva1.sinaimg.cn/large/006tNbRwly1gax0scsgf4j30zk0k0gt5.jpg)
 
 
PIVOTAL：毕威拓是一家位于美国加州的计算机软件公司。

阿里巴巴

云生态家族产品
![产品](https://tva1.sinaimg.cn/large/006tNbRwly1gawzqdufzgj30k00b6wfb.jpg)
感觉更多是在展示阿里云自家的产品中间件都在云上，涵盖底层基础设施、数据智能、分布式应用等

## 技术进化之路
- 虚拟化
- 基于虚拟化的云计算
- 容器的兴起和编排大战（2013年docker、2017年底k8s胜出）


云的形态变化
![infoq](https://tva1.sinaimg.cn/large/006tNbRwly1gawc67i6grj30qo0f0ae6.jpg)
可以看到，云给我们做的事情越来越多，越底层的东西越容易被云替换。到FAAS阶段，开发只需要关心一个个Function就能完成业务的开发。




参考文档：[云原生应用应该是什么样子？](https://www.infoq.cn/article/fA42rfjV*dYGAvRANFqE)

