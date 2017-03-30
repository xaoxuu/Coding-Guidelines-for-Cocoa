---
title: 框架开发技术
keywords: 代码 命名 基础 通用
last_updated: July 3, 2016
tags:
summary:
sidebar: mydoc_sidebar
permalink: tffd-initialization.html
folder: techniques-for-framework-developers
---


Developers of [frameworks](undefined) have to be more careful than other developers in how they write their code. Many client applications could link in their framework and, because of this wide exposure, any deficiencies in the framework might be magnified throughout a system. The following items discuss programming techniques you can adopt to ensure the efficiency and integrity of your framework.

**Note:** Some of these techniques are not limited to frameworks. You can productively apply them in application development.

## Initialization

The following suggestions and recommendations cover framework initialization.

### Class Initialization

The `initialize`  [class method](undefined) gives you a place to have some code executed once, lazily, before any other method of the class is invoked. It is typically used to set the version numbers of classes (see [Versioning and Compatibility](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/FrameworkImpl.html#//apple_ref/doc/uid/20001286-1001777)).

The runtime sends `initialize` to each class in an inheritance chain, even if it hasn’t implemented it; thus it might invoke a class’s `initialize` method more than once (if, for example, a subclass hasn’t implemented it). Typically you want the initialization code to be executed only once. One way to ensure this happens is to use `dispatch_once()`:

| `+ (void)initialize {`                   |
| ---------------------------------------- |
| `    static dispatch_once_t onceToken = 0;` |
| `    dispatch_once(&onceToken, ^{`       |
| `        // the initializing code`       |
| `    }`                                  |
| `}`                                      |
| ` `                                      |

**Note:** Because the runtime sends initialize to every class, it's possible that `initialize` will be called in the context of a subclass—if the subclass doesn't implement `initialize`, then the invocation will fall through to the superclass. If you specifically need to perform initialization within the context of the relevant class, you can perform the following check rather than using `dispatch_once()`:`if (self == [NSFoo class]) {``    // the initializing code``}`

You should never invoke the `initialize` method explicitly. If you need to trigger the initialization, invoke some harmless method, for example:

### Designated Initializers

A designated initializer is an `init` method of a class that invokes an `init` method of the superclass. (Other initializers invoke the `init` methods defined by the class.) Every public class should have one or more designated initializers. As examples of designated initializers there is `NSView`’s `initWithFrame:` and `NSResponder`’s `init` method. Where `init`methods are not meant to be [overridden](undefined), as is the case with `NSString` and other abstract classes fronting [class clusters](undefined), the subclass is expected to implement its own.

Designated initializers should be clearly identified because this information is important to those who want to subclass your class. A subclass can just override the designated initializer and all other initializers will work as designed.

When you implement a class of a framework, you often have to implement its [archiving](undefined) methods as well: `initWithCoder:` and `encodeWithCoder:`. Be careful not to do things in the initialization code path that doesn’t happen when the object is unarchived. A good way to achieve this is to call a common routine from your designated initializers and `initWithCoder:` (which is a designated initializer itself) if your class implements archiving.

### Error Detection During Initialization

A well-designed initialization method should complete the following steps to ensure the proper detection and propagation of errors:

1. Reassign self by invoking `super`’s [designated initializer](undefined).
2. Check the returned value for `nil`, which indicates that some error occurred in the superclass initialization.
3. If an error occurs while initializing the current class, release the object and return `nil`.

[Listing 1](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/FrameworkImpl.html#//apple_ref/doc/uid/20001286-1004028-BAJBJCIA) illustrates how you might do this.

**Listing 1**  Error detection during initialization

| `- (id)init {`                           |
| ---------------------------------------- |
| `    self = [super init];  // Call a designated initializer here.` |
| `    if (self != nil) {`                 |
| `        // Initialize object  ...`      |
| `        if (someError) {`               |
| `            [self release];`            |
| `            self = nil;`                |
| `        }`                              |
| `    }`                                  |
| `    return self;`                       |
| `}`                                      |




{% include links.html %}
