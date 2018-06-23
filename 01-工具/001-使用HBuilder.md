---
title: 使用HBuilder
toc: true
date: 2017-07-26 00:03:21
tags: 工具
categories: 工具
---

HBuilder下载地址：[HBuilder官网](http://www.dcloud.io/)

<!--more-->

HBuilder是DCloud（数字天堂）推出的一款支持HTML5的Web开发IDE。HBuilder的编写用到了Java、C、Web和Ruby。HBuilder本身主体是由Java编写，它基于Eclipse，所以顺其自然地兼容了Eclipse的插件。

## HBuilder设置外部web服务器测试移动Web

### 1.打开开发工具

1. 工具右上角更改开发视图模式为“**边改边看模式**” 

2. 打开设置web服务器

![web服务器](http://ot4r4qnml.bkt.clouddn.com/web%E6%9C%8D%E5%8A%A1%E5%99%A8.png)

### 2.设置外置服务器

1. 选择“外置Web服务器” ☞ 右边“新建”
 
2. 编辑服务配置界面，“名称”随意，“浏览器运行URL”填写本机ip地址

### 3.查看IP地址并配置web服务器

1.地址查看方式：在命令行中输入`ipconfig`，找到`IPv4`的地址

![ipconfig](http://ot4r4qnml.bkt.clouddn.com/ipconfig.png)

2.填写在URL中，如图所示（要在IP地址后面加上HBuilder使用的**端口8020**）：

![web服务器配置](http://ot4r4qnml.bkt.clouddn.com/%E9%85%8D%E7%BD%AE%E6%9C%8D%E5%8A%A1%E5%99%A8.png)

3.使用新建的myWeb外部服务器

![使用服务器](http://ot4r4qnml.bkt.clouddn.com/%E6%9C%8D%E5%8A%A1%E5%99%A8.png)

### 4.扫码测试

在“web浏览器”网址右边有一个**二维码**标志，点击，使用手机扫描测试

***注意：*** 扫码测试需要电脑和手机在同一个局域网下！！！

电脑运行：

![电脑运行结果](http://ot4r4qnml.bkt.clouddn.com/%E8%BF%90%E8%A1%8C1.png)

手机扫码运行：

![手机运行结果](http://ot4r4qnml.bkt.clouddn.com/%E6%89%8B%E6%9C%BA%E8%BF%90%E8%A1%8C.png)


