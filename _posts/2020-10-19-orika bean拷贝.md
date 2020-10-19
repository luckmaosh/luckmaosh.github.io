---
layout: post
title: Orika 是一个简单、快速的 JavaBean 拷贝框架
date: 2020-10-19
categories: java
tags: java  bean拷贝
---


- Orika 是什么？

Orika 是一个简单、快速的 JavaBean 拷贝框架，它能够递归地将数据从一个 JavaBean 复制到另一个 JavaBean，这在多层应用开发中是非常有用的。

- Orika 的竞品
相信大多数朋友接触过 apache 的 BeanUtils，直到认识了 spring 的 BeanUtils，前者被后者完爆，后来又出现了 Dozer，Orika 等重量级的 Bean 拷贝工具，在性能和特性上都有了很大的提升。

先给结论，众多 Bean 拷贝工具中，今天介绍的 Orika 具有想当大的优势。口说无凭，可参考下面文章中的各个工具的对比：http://tech.dianwoda.com/2017/11/04/gao-xing-neng-te-xing-feng-fu-de-beanying-she-gong-ju-orika/?utm_source=tuicool&utm_medium=referral

简单整理后，如下所示：

- BeanUtils
apache 的 BeanUtils 和 spring 的 BeanUtils 中拷贝方法的原理都是先用 jdk 中 java.beans.Introspector 类的 getBeanInfo() 方法获取对象的属性信息及属性 get/set 方法，接着使用反射（Method 的 invoke(Object obj, Object... args)）方法进行赋值。apache 支持名称相同但类型不同的属性的转换，spring 支持忽略某些属性不进行映射，他们都设置了缓存保存已解析过的 BeanInfo 信息。

- BeanCopier
cglib 的 BeanCopier 采用了不同的方法：它不是利用反射对属性进行赋值，而是直接使用 ASM 的 MethodVisitor 直接编写各属性的 get/set 方法（具体过程可见 BeanCopier 类的 generateClass(ClassVisitor v) 方法）生成 class 文件，然后进行执行。由于是直接生成字节码执行，所以 BeanCopier 的性能较采用反射的 BeanUtils 有较大提高，这一点可在后面的测试中看出。

- Dozer
使用以上类库虽然可以不用手动编写 get/set 方法，但是他们都不能对不同名称的对象属性进行映射。在定制化的属性映射方面做得比较好的有 Dozer，Dozer 支持简单属性映射、复杂类型映射、双向映射、隐式映射以及递归映射。可使用 xml 或者注解进行映射的配置，支持自动类型转换，使用方便。但 Dozer 底层是使用 reflect 包下 Field 类的 set(Object obj, Object value) 方法进行属性赋值，执行速度上不是那么理想。

- Orika
那么有没有特性丰富，速度又快的 Bean 映射工具呢，这就是下面要介绍的 Orika，Orika 是近期在 github 活跃的项目，底层采用了 javassist 类库生成 Bean 映射的字节码，之后直接加载执行生成的字节码文件，因此在速度上比使用反射进行赋值会快很多，下面详细介绍 Orika 的使用方法。