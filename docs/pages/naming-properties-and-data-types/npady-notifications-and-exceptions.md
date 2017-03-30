---
title: 通知和异常
keywords: 代码 命名 基础 通用
last_updated: July 3, 2016
tags:
summary:
sidebar: mydoc_sidebar
permalink: npady-notifications-and-exceptions.html
folder: naming-properties-and-data-types
---


## 3.1 Notifications

Notification的格式

```objective-c
[Name of associated class] + [Did | Will] + [UniquePartOfName] + Notification
```

```objective-c
NSApplicationDidBecomeActiveNotification
NSWindowDidMiniaturizeNotification 
NSTextViewDidChangeSelectionNotification
NSColorPanelColorDidChangeNotification
```

## 3.2 Exceptions

- Exception的格式

```objective-c
[Prefix] + [UniquePartOfName] + Exception
```

```objective-c
NSColorListIOException
NSColorListNotEditableException
NSDraggingException  
NSFontUnavailableException
NSIllegalSelectorException
```





{% include links.html %}
