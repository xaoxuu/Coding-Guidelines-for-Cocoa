---
title: 集合方法
keywords: 代码 命名 基础 通用
last_updated: 2017-04-01
tags:
summary:
sidebar: home_sidebar
permalink: nm-collection-methods.html
folder: naming-methods
---


为了管理集合中的元素，集合应该有这几个方法

- \- (void)addElement:(elementType)anObj;
- \- (void)removeElement:(elementType)anObj;
- \- (NSArray *)elements;

```objective-c
- (void)addLayoutManager:(NSLayoutManager *)obj;
- (void)removeLayoutManager:(NSLayoutManager *)obj;
- (NSArray *)layoutManagers;
```

如果集合是无序的，返回一个NSSet比NSarray更好

如果需要在集合中的特定位置插入元素，使用类似下面的方法

```objective-c
- (void)insertLayoutManager:(NSLayoutManager *)obj atIndex:(int)index;
- (void)removeLayoutManagerAtIndex:(int)index;
```

其他集合方法示例

```objective-c
- (void)addChildWindow:(NSWindow *)childWin ordered:(NSWindowOrderingMode)place;
- (void)removeChildWindow:(NSWindow *)childWin;
- (NSArray *)childWindows;
- (NSWindow *)parentWindow;
- (void)setParentWindow:(NSWindow *)window;
```




{% include links.html %}
