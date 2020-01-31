---
layout: post
title: unix内核源码
date: 2020-01-20
categories: unix
tags: 内核 unix
---

- Version 5 Unix这个版本，AT&T公司只授权给学术机构使用。

- unix  v6：由贝尔实验室于1975年5月释出的UNIX操作系统，是第一个对外公开的UNIX版本，主要运行在DEC PDP-11系列的小型计算机（Minicomputer）家族

- 1979，贝尔实验室在发布UNIX V6之后，于1979年又发布了UNIX第7版（Seventh Edition Unix，UNIX V7）
- 1978，加州大学伯克利分校于1978年发布了以UNIX V6为基础的BSD的首个版本。


总线是用来做什么的？计算机运行的原理：

- 所有数据加载到内存
- cpu 读入指令，执行指令
- 数据只和寄存器和内存产生读写
- 寄存器、硬盘、io都会通过数据总线连接到内存，都有地址
- 通过地址找到对应的数据
- 处理器模式的切换 伴随着虚拟地址对 应的物理内存区域 的切换。用 户模式时的虚拟地址空间称为用户空间，内核模式时的虚拟地址空间称为内核空间


概念

- PSW，processor status word, 处理器状态字
- MMU 内存管理单元
- TSS time share system
- 中断：是指用来实现下述处理的机制：当周边设备发出请求时，暂停执行中的进程，转 而执行与请求相对应的处理。

## 进程的内存结构
代码段，用来存程序指令，只读。

数据段用来存放程序执行的变量存储。下图是数据段：
![](https://tva1.sinaimg.cn/large/006tNbRwly1gb2v20rh8zj31c00mgq68.jpg)

每个进程都拥有独立的虚拟地址空间
![](https://tva1.sinaimg.cn/large/006tNbRwly1gb2v9yhk2cj313w0u0dl5.jpg)

### proc结构体

### user结构体

