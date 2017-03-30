---
title: 代理方法
keywords: 代码 命名 基础 通用
last_updated: July 3, 2016
tags:
summary:
sidebar: home_sidebar
permalink: nm-delegate-methods.html
folder: naming-methods
---

以发送消息的对象开始

省略了前缀的类名和首字母小写

```objective-c
- (BOOL)tableView:(NSTableView *)tableView shouldSelectRow:(int)row;
- (BOOL)application:(NSApplication *)sender openFile:(NSString *)filename;
```

以发送消息的对象开始的规则不适用下列两种情况

只有一个sender参数的方法

```objective-c
- (BOOL)applicationOpenUntitledFile:(NSApplication *)sender;
```

响应notification的方法（方法的唯一参数就是notification）

```objective-c
- (void)windowDidChangeScreen:(NSNotification *)notification;
```

使用单词 did 和 will 来通知delegate

- did 表示某些事已发生
- will 表示某些事将要发生

```objective-c
- (void)browserDidScroll:(NSBrowser *)sender;
- (NSUndoManager *)windowWillReturnUndoManager:(NSWindow *)window;
```

询问delegate是否可以执行某个行为时可以使用 did 或 will，不过 should 更完美  

```objective-c
- (BOOL)windowShouldClose:(id)sender;
```




{% include links.html %}
