---
title: 通用原则
keywords: 代码 命名 基础 通用
last_updated: July 3, 2016
tags:
summary:
sidebar: mydoc_sidebar
permalink: cnb-common.html
folder: code-naming-basics
---


## 1. 清晰

尽量清晰又简洁，无法两全时清晰更重要


![](assets/1441509819955470.png)

通常不应缩写名称，即使方法名很长也应完整拼写

你可能认为某个缩写众所周知，但其实未必，特别是你周围的开发者语言文化背景不同时  
有一些历史悠久的缩写还是可以使用的，详见[第五章](chapter5.md)

![](assets/1441509896749042.png)

API命名避免歧义，例如一个方法名有多种理解

![](assets/1441509905881130.png)

## 2. 一致

尽力保持Cocoa编程接口命名一致

如果有疑惑，请浏览当前头文件或者参考文档  
当某个类的方法使用了多态时，一致性尤其重要

不同类里，功能相同的方法命名也应相同

![](assets/1441509959926816.png)

## 3. 避免自引用（self Reference）

命名不应自引用

这里的自引用指的是在词尾引用自身

![](assets/1441509975783777.png)

Mask与Notification忽略此规则

![](assets/1441509984966357.png)



{% include links.html %}
