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

产品使用流程

发起人流程

- 选择联系人
- 点击共享屏幕，调用浏览器的接口，截取屏幕
- 选择要共享的窗口，确定共享

接收人流程

- 收到共享消息，点击确认
- 看到共享的屏幕


##  后续

看了很多网页，发现自己的前端知识太差，需要充电🔋，赶紧刷一下vue，nodejs