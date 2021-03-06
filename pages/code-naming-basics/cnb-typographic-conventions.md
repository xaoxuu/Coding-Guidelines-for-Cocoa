---
title: 书写约定
keywords: 代码 命名 基础 通用 前缀
last_updated: 2017-04-01
tags:
summary:
sidebar: home_sidebar
permalink: cnb-typographic-conventions.html
folder: code-naming-basics
---


在命名API元素时， 使用驼峰命名法（如runTheWordsTogether），并注意以下书写约定：

## 方法名

* 小写第一个字母，大写之后所有单词的首字母，不使用前缀
* 如果方法名以一个众所周知的大写缩略词开始，该规则不适用

如TIFFRepresentation \(NSImage\)

```objective-c
fileExistsAtPath:isDirectory:
```

## 函数及常量名

* 使用与其关联类相同的前缀，并大写首字母

```objective-c
NSRunAlertPanel
NSCellDisabled
```

## 标点符号

* 由多个单词组成的名称，别使用标点符号作为名称的一部分

* * 分隔符（下划线、破折号等）也不能使用
* 避免使用下划线作为私有方法的前缀，Apple保留这一方式的使用

* * 强行使用可能会导致命名冲突，即Apple已有的方法被覆盖，这会导致灾难性后果
  * 实例变量使用下划线作为前缀还是允许的


{% include links.html %}
