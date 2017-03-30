---
title: 私有方法
keywords: 代码 命名 基础 通用
last_updated: July 3, 2016
tags:
summary:
sidebar: mydoc_sidebar
permalink: nm-private-methods.html
folder: naming-methods
---


不要使用下划线作为私有方法的前缀，Apple保留这一使用方式

因为若是你的私有方法名已被Apple使用，覆盖它将会产生极难追踪的BUG

如果继承自大型Cocoa框架（如UIView），请确保子类的私有方法名与父类不一样

可以为私有方法加一个前缀，如公司名或项目名：XX_

例如你的项目叫做Byte Flogger，那么前缀可能是：BF_addObject

总之，为子类的私有方法添加前缀是为了不覆盖其父类的私有方法


{% include links.html %}
