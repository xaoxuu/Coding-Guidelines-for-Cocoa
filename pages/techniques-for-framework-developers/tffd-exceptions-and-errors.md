---
title: 异常和错误
keywords: 代码 命名 基础 通用
last_updated: 2017-04-01
tags:
summary:
sidebar: home_sidebar
permalink: tffd-exceptions-and-errors.html
folder: techniques-for-framework-developers
---


Most [Cocoa](undefined) framework methods do not force developers to catch and handle [exceptions](undefined). That is because exceptions are not raised as a normal part of execution, and are not typically used to communicate expected runtime or user errors. Examples of these errors include:

- File not found
- No such user
- Attempt to open a wrong type of document in an application
- Error in converting a string to a specified encoding

However, Cocoa does raise exceptions to indicate programming or logic errors such as the following:

- Array index out of bounds
- Attempt to mutate immutable objects
- Bad argument type

The expectation is that the developer will catch these kinds of errors during testing and address them before shipping the application; thus the application should not need to handle the exceptions at runtime. If an exception is raised and no part of the application catches it, the top-level default handler typically catches and reports the exception and execution then continues. Developers can choose to replace this default exception-catcher with one that gives more detail about what went wrong and offers the option to save data and quit the application.

Errors are another area where Cocoa frameworks differ from some other software libraries. Cocoa methods generally do not return error codes. In cases where there is one reasonable or likely reason for an error, the methods rely on a simple test of a boolean or object (`nil`/non-`nil`) returned value; the reasons for a `NO` or `nil` returned value are documented. You should not use error codes to indicate programming errors to be handled at runtime, but instead raise exceptions or in some cases simply log the error without raising an exception.

For instance, `NSDictionary`’s `objectForKey:` method either returns the found object or `nil` if it can’t find the object. `NSArray`’s `objectAtIndex:` method can never return `nil`(except for the overriding general language convention that any message to `nil` results in a `nil `return), because an `NSArray` object cannot store `nil` values, and by definition any out-of-bounds access is a programming error that should result in an exception. Many `init` methods return `nil` when the object cannot be initialized with the parameters supplied.

In the small number of cases where a method has a valid need for multiple distinct error codes, it should specify them in a by-reference argument that returns either an error code, a localized error string, or some other information describing the error. For example, you might want to return the error as an `NSError` object; look at the `NSError.h` header file in Foundation for details. This argument might be in addition to a simpler `BOOL` or `nil` that is directly returned. The method should also observe the convention that all by-reference arguments are optional and thus allow the sender to pass `NULL` for the error-code argument if they do not wish to know about the error.


{% include links.html %}
