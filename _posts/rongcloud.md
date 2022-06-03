
语音聊天： IM ，app聊天；技术点实时音视频


聊天室：
专为直播产品提供，满足各类直播互动场景需求，打造良好的直播聊天互动体验，完美融入你的直播业务。


RTCLib：
音视频依赖的库


IMLib: IM 通信能力库，不含 UI，适用于对 UI 有较高订制需求的 IM 开发者

IMKit: IM 通信组件，包含 UI，适用于快速集成，对 UI 定制需求交少的开发者，IMKit 依赖 IMLib



直播：
需要 客户端（PC，Android、iOS），服务端（融云）来一起完成，我们要做的是客户端的开发，就是把融云提供的sdk集成到我们的客户端里面就可以使用，其他音视频通信由SDK和融云服务器来完成。

客户端的作用只管接受数据流和上传数据流。

主播和观众是不是一样的，我感觉是一样的，他们地位是平等的，甚至有时候他们的关系是可以互换。


## 客户端和web两个版本

客户端基于flutter开发

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gfbg3w4yx6j30u00vgjuo.jpg)


flutter源码：git@github.com:rongcloud/rongcloud-rtc-flutter-sdk.git 

web： https://docs.rongcloud.cn/v3/views/rtc/meeting/guide/quick/web.html


## RTCLib
客户端通过集成 融云 RTCLib 可快速实现主播推流，观众拉流，连麦互动等功能。


https://docs.rongcloud.cn/v3/views/rtc/livevideo/intro/ability.html
