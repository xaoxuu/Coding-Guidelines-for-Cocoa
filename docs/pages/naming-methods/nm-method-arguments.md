---
title: 方法参数
keywords: 代码 命名 基础 通用
last_updated: July 3, 2016
tags:
summary:
sidebar: mydoc_sidebar
permalink: nm-method-arguments.html
folder: naming-methods
---


- 参数名以小写字母开始，之后的单词首字母大写

```objective-c
如：removeObject:(id)anObject
```

- 别使用 ”pointer” 或 ”ptr” 命名

- - 参数类型里就已表明它是否是一个指针

- 避免只有一到二个字母的参数名

- 避免只有几个字母的缩写

```objective-c
...action:(SEL)aSelector
...alignment:(int)mode
...atIndex:(int)index
...content:(NSRect)aRect
...doubleValue:(double)aDouble
...floatValue:(float)aFloat
...font:(NSFont *)fontObj  
...frame:(NSRect)frameRect
...intValue:(int)anInt
...keyEquivalent:(NSString *)charCode
...length:(int)numBytes
...point:(NSPoint)aPoint
...stringValue:(NSString *)aString
...tag:(int)anInt
...target:(id)anObject
...title:(NSString *)aString
```



{% include links.html %}
