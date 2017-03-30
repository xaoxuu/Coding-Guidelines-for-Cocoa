---
title: 框架开发技术
keywords: 代码 命名 基础 通用
last_updated: July 3, 2016
tags:
summary:
sidebar: home_sidebar
permalink: tffd-object-comparison.html
folder: techniques-for-framework-developers
---



You should be aware of an important difference between the generic [object-comparison](undefined) method `isEqual:` and the comparison methods that are associated with an object type, such as `isEqualToString:`. The `isEqual:` method allows you to pass arbitrary objects as arguments and returns `NO` if the objects aren’t of the same class. Methods such as `isEqualToString:` and `isEqualToArray:` usually assume the argument is of the specified type (which is that of the receiver). They therefore do not perform type-checking and consequently they are faster but not as safe. For values retrieved from external sources, such as an application’s information [property list](undefined) (`Info.plist`) or preferences, the use of `isEqual:` is preferred because it is safer; when the types are known, use `isEqualToString:` instead.

A further point about `isEqual:` is its connection to the `hash` method. One basic invariant for objects that are put in a hash-based Cocoa [collection](undefined) such as an `NSDictionary` or `NSSet` is that if `[A isEqual:B] == YES`, then `[A hash] == [B hash]`. So if you override `isEqual:` in your class, you should also override `hash` to preserve this invariant. By default `isEqual:` looks for pointer equality of each object’s address, and `hash` returns a hash value based on each object’s address, so this invariant holds.

{% include links.html %}
