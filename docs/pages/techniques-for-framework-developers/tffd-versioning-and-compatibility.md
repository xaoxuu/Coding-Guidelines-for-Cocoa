---
title: 框架开发技术
keywords: 代码 命名 基础 通用
last_updated: 2017-04-01
tags:
summary:
sidebar: home_sidebar
permalink: tffd-versioning-and-compatibility.html
folder: techniques-for-framework-developers
---



When you add new classes or methods to your [framework](undefined), it is not usually necessary to specify new version numbers for each new feature group. Developers typically perform (or should perform) [Objective-C](undefined) runtime checks such as `respondsToSelector:` to determine if a feature is available on a given system. These runtime tests are the preferred and most dynamic way to check for new features.

However, you can employ several techniques to make sure each new version of your framework are properly marked and made as compatible as possible with earlier versions.

### Framework Version

When the presence of a new feature or bug fix isn’t easily detectable with runtime tests, you should provide developers with some way to check for the change. One way to achieve this is to store the exact version number of the framework and make this number accessible to developers:

- Document the change (in a release note, for instance) under a version number.
- Set the current version number of your framework and provide some way to make it globally accessible. You might store the version number in your framework’s information[property list](undefined) (`Info.plist`) and access it from there.

### Keyed Archiving

If the objects of your framework need to be written to [nib file](undefined), they must be able to archive themselves. You also need to archive any documents that use the archiving mechanisms to store document data.

You should consider the following issues about archiving:

- If a key is missing in an archive, asking for its value will return `nil`, `NULL`, `NO`, 0, or 0.0, depending on the type being asked for. Test for this return value to reduce the data that you write out. In addition, you can find out whether a key was written to the archive.
- Both the encode and decode methods can do things to ensure backwards compatibility. For instance, the encode method of a new version of a class might write new values using keys but can still write out older fields so that older versions of the class can still understand the object. In addition, decode methods might want to deal with missing values in some reasonable way to maintain some flexibility for future versions.
- A recommended naming [convention](undefined) for archive keys for framework classes is to begin with the prefix used for other API elements of the framework and then use the name of the instance variable. Just make sure that names cannot conflict with the names of any superclass or subclass.
- If you have a utility function that writes out a basic data type (in other words, a value that isn’t an object), be sure to use a unique key. For example, an “archiveRect” routine that archives a rectangle should take a key argument and either use the given key or, if it writes out multiple values (for instance, four floats), it should append its own unique bits to the provided key.
- Archiving bitfields as-is can be dangerous due to compiler and endianness dependencies. You should archive them only when, for performance reasons, a lot of bits need to be written out, many times. See [Bitfields](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/FrameworkImpl.html#//apple_ref/doc/uid/20001286-1005950) for a suggestion.

{% include links.html %}
