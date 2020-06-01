---
layout: post
title: 激活函数：ReLU
date: 2020-05-28
categories: AI
tags: AI 人工智能
---

激活函数：ReLU

函数形式f(x)=max(0,x)f(x)=max(0,x)f(x)=max(0,x)
加入ReLu激活函数的神经元被称为整流线性单元




![](https://tva1.sinaimg.cn/large/007S8ZIlly1gf99llfl3kj306r05oglq.jpg)


相比sigmod函数与Relu函数，Relu函数有以下优缺点
优点
1)克服梯度消失的问题
2)加快训练速度(克服了梯度消失问题，训练才会快)
3)一阶导数处处相等为1，二阶导数处处为0
4）单侧抑制
缺点：
1)若输入负数，则完全不激活，ReLU函数没用。
2)ReLU函数输出要么是0，要么是正数，也就是ReLU函数不是以0为中心的函数。