---
layout: post
title: 我们要做一个融合IM和直播的东西
date: 2020-03-24
categories: IM 
tags: alive
---

## 思考

我们想要这样一个功能，学生在线学编程课的时候，可以通过im工具随时和老师交流，也可以通过视频方式把屏幕分享给老师，让老师帮助指导学习。老师也可以分享屏幕给所有人，讲解课程内容。

## 技术方案

我之前没有做过这样的系统，现在只好硬着头皮上，先去找资料。


终于找到了一些资料

** 涉及技术：vue、electron、ffmpeg、node **
关于录屏和摄像对比了两种方法


-  使用HTML5的api实现
 - 摄像：mediaDevices（获取设备）+ getUserMedia（获取流） + MediaRecorder（存储）
 - 录屏：getDisplayMedia（获取流） + MediaRecorder（存储）


ffmpeg + node：FFmpeg是一套非常强大的音视频处理的开源工具，不多介绍，而Electron基于node和chromium，它允许使用node的API以及几乎所有的node模块，这意味这着我们可以调用cmd命令来操作ffmpeg实现录屏和摄像录制，当然ffmpeg功能绝不止这点

## 思路

点击视频按钮，浏览器的nodejs里面获取屏幕内容的字节流，然后再把字节流推送给求助者。

找了半天，最终发现这个demo比较好，点击start record，就可以选择窗口或者浏览器页面录制视频，播放器里面就可以实时看到内容。

https://blog.goonxh.com/demo/screenRecord

博客地址：

https://blog.csdn.net/blueXh/article/details/88955821?depth_1-utm_source=distribute.pc_relevant.none-task

```javascript

<script type="text/javascript">
navigator.mediaDevices.getDisplayMedia({ video: true })
 .then(stream => {
    //we have a stream, attach it to a feedback video element
    videoElement.srcObject = stream;
  }, error => {
    console.log("Unable to acquire screen capture", error);
  });
</script>	

```

产品使用流程

发起人流程

- 选择联系人
- 点击共享屏幕，调用浏览器的接口，截取屏幕
- 选择要共享的窗口，确定共享

接收人流程

- 收到共享消息，点击确认
- 看到共享的屏幕

### IM的基本概念

我理解的im系统，应该包含几个基本的模型：用户、聊天会话、消息记录、群组

一般来说，一个用户加入一个聊天组之后，只能查看之后的消息记录（微信），或者只能查看最近100条记录（钉钉）。用户在任何地方登陆自己的账号，都可以看到过去的消息。还有一个问题，就是用户是单点登陆还是多点登陆，多点登陆意味着，服务器要把同一条消息推送到这个人登陆中的多个客户端，这个实现起来比较复杂。

##  后续

看了很多网页，发现自己的前端知识太差，需要充电🔋，赶紧刷一下vue，nodejs。

另外，我找的这些都是开源方案，虽然免费，但是自己去搭建需要花费大量的人力成本，稳定性也不好。所以，如果是企业级的应用，最好的方法是直接找这方面比较有经验的服务提供商，他们会提供更专业的解决方案，当下这个科技发展飞速发展的社会，应该每个领域都会成熟的方案解决商。

明天我还要考察一个数据分析、数据埋点的技术方案，可能会优先去学习一些服务提供商的产品，这样有助于我快速找到关键点。