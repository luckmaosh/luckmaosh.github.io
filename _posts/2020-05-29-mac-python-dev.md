---
layout: post
title: mac python 环境
date: 2020-05-29
categories: python
tags: mac  python
---


## python3.7


pip包的安装路径

```
/usr/local/lib/python3.7/site-packages


```


##pipenv工具安装

Pipenv 是 Python 项目的依赖管理器。如果您熟悉 Node.js 的 npm 或 Ruby 的 bundler，那么它们在思路上与这些工具类似。尽管 pip 可以安装 Python 包， 但仍推荐使用 Pipenv，因为它是一种更高级的工具，可简化依赖关系管理的常见使用情况。

使用 pip 来安装 Pipenv：
```
$ pip install --user pipenv
```

## 安装wxpython
这是一款python的GUI库，非常牛逼，用来做客户端编程

```
brew install wxpython
//然后，耐心的等待，总之漫长的下载安装过程
//查看信息
brew info wxpython

//建立软连接到我们的site-package就可以了
ln -s /usr/local/Cellar/wxpython/3.0.2.0/lib/python2.7/site-packages/wx-3.0-osx_cocoa/wx   /usr/local/lib/python3.7/site-packages/wx

```

## 安装bs4
```
pip install beautifulsoup4
```
这个时候会出现错误，装到了系统自带的python2.7中

 

把bs4装到Python3的方法：
```
pip3 install beautifulsoup4
```




解决因macOS High Sierra更新Ruby到2.3造成的Jekyll不能启动的问题

zsh: /usr/local/bin/jekyll: bad interpreter: /System/Library/Frameworks/Ruby.framework/Versions/2.0/usr/bin: no such file or directory

修改jekyll文件的行首，把路径改成#!/System/Library/Frameworks/Ruby.framework/Versions/2.3/usr/bin/ruby
  


ruby版本
```
ruby -v
```

rvm ruby的版本管理工具
```
rvm install 2.3
```

gem 
```
gem sources --remove https://rubygems.org/
gem sources -a https://gems.ruby-china.org/
```


bundle 是gem的一个插件
```
 gem install bundle
```