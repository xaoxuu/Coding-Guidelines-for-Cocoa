---
title: Property的声明和实例变量
keywords: 代码 命名 基础 通用
last_updated: 2017-04-01
tags:
summary:
sidebar: home_sidebar
permalink: npady-declared-properties-and-instance-variables.html
folder: naming-properties-and-data-types
---

## 1.1 Property

Property命名规则与第二章accessor methods一样（因为两者紧密联系）

如果property表示为一个名词或动词，格式如下

@property (…) 类型 名词/动词 ;

```objective-c
@property (strong) NSString *title;
@property (assign) BOOL showsAlpha;
```

如果property表示为一个形容词

- 可省略 ”is” 前缀
- 但要指定getter方法的惯用名称

```objective-c
@property (assign, getter=isEditable) BOOL editable;
```

## 1.2 实例变量

通常不应该直接访问实例变量

init、dealloc、accessor methods等方法内部例外

实例变量以下划线 “_” 开始

确保实例变量描述了所存储的属性

```objective-c
@implementation MyClass {
   BOOL _showsTitle;
}
```

如果想要修改property的实例变量名，使用 @synthesize语句

```objective-c
@implementation MyClass
@synthesize showsTitle=_showsTitle;
```

为一个class添加实例变量时，有几点需要注意：

- 避免声明公有实例变量

- - 开发者关注的应该是对象接口，而不是其数据细节
  - 你可以通过使用property来避免声明实例变量

- 如果需要声明实例变量，指定关键字@private 或 @protected

- - 如果你希望子类可以直接访问某个实例变量，使用 @protected 关键字

- 如果一个实例变量是某个类可访问的属性，确保写了accessor methods

- - 如果有可能，还是使用property





{% include links.html %}
