---
title: getter setter 方法
keywords: 代码 命名 基础 通用
last_updated: July 3, 2016
tags:
summary:
sidebar: home_sidebar
permalink: nm-accessor-methods.html
folder: naming-methods
---


如果property表示为名词，格式如下

- (type)noun;
- (void)setNoun:(type)aNoun;  
- (BOOL)isAdjective;

```objective-c
- (NSString *)title;
- (void)setTitle:(NSString *)aTitle;
```

如果property表示为形容词，格式如下

- (BOOL)isAdjective;
- (void)setAdjective:(BOOL)flag;  

```objective-c
- (BOOL)isEditable;
- (void)setEditable:(BOOL)flag;
```

如果property表示为动词，格式如下（动词用一般现在时）

- (BOOL)verbObject;
- (void)setVerbObject:(BOOL)flag;  

```objective-c
- (BOOL)showsAlpha;
- (void)setShowsAlpha:(BOOL)flag;
```

不要把动词的过去分词形式当作形容词使用  

![1441510445810397](assets/1441510445810397.png)

你可能使用情态动词（can、should、will等）来增加可读性，不过不要使用 do或 does

![1441510455806266](assets/1441510455806266.png)

只有方法需要间接返回多个值的情况下才使用 get

像这种接收多个参数的方法应该能够传入nil，因为调用者未必对每个参数都感兴趣

![1441510465224919](assets/1441510465224919.png)




{% include links.html %}
