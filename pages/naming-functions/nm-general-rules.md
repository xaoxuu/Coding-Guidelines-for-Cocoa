---
title: 通用原则
keywords: 代码 命名 基础 通用
last_updated: 2017-04-01
tags:
summary:
sidebar: home_sidebar
permalink: nf-general-rules.html
folder: naming-functions
---


函数的命名类似方法，但有两点要注意

- 你使用的类和常量拥有相同的前缀
- 前缀后的首字母大写

许多函数名以描述其作用的动词开始

```objective-c
NSHighlightRect
NSDeallocateObject
```

查询属性的函数有进一步的命名规则

如果函数返回首个参数的属性，省略动词

```objective-c
unsigned int NSEventMaskFromType(NSEventType type)
float NSHeight(NSRect aRect)
```

如果通过reference返回了值，使用 “Get”

```objective-c
const char *NSGetSizeAndAlignment(const char *typePtr, unsigned int *sizep, unsigned int *alignp)
```

如果返回的是boolean值，应该灵活使用动词 

```objective-c
BOOL NSDecimalIsNotANumber(const NSDecimal *decimal)
```




{% include links.html %}
