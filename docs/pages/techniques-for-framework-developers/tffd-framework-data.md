---
title: 框架开发技术
keywords: 代码 命名 基础 通用
last_updated: 2017-04-01
tags:
summary:
sidebar: home_sidebar
permalink: tffd-framework-data.html
folder: techniques-for-framework-developers
---



How you handle framework data has implications for performance, cross-platform compatibility, and other purposes. This section discusses techniques involving framework data.

### Constant Data

For performance reasons, it is good to mark as constant as much framework data as possible because doing so reduces the size of the `__DATA` segment of the Mach-O binary. Global and static data that is not `const` ends up in the `__DATA` section of the `__DATA` segment. This kind of data takes up memory in every running instance of an application that uses the framework. Although an extra 500 bytes (for example) might not seem so bad, it might cause an increment in the number of pages required—an additional four kilobytes per application.

You should mark any data that is constant as `const`. If there are no `char *` pointers in the block, this will cause the data to land in the `__TEXT` segment (which makes it truly constant); otherwise it will stay in the `__DATA` segment but will not be written on (unless prebinding is not done or is violated by having to slide the binary at load time).

You should initialize static variables to ensure that they are merged into the `__data` section of the `__DATA` segment as opposed to the `__bss` section. If there is no obvious value to use for initialization, use 0, `NULL`, 0.0, or whatever is appropriate.

### Bitfields

Using signed values for bitfields, especially one-bit bitfields, can result in undefined behavior if code assumes the value is a boolean. One-bit bitfields should always be unsigned. Because the only values that can be stored in such a bitfield are 0 and -1 (depending on the compiler implementation), comparing this bitfield to 1 is false. For example, if you come across something like this in your code:

| `BOOL isAttachment:1;` |
| ---------------------- |
| `int startTracking:1;` |

You should change the type to `unsigned int`.

Another issue with bitfields is archiving. In general, you shouldn’t write bitfields to disk or archives in the form they are in, as the format might be different when they are read again on another architecture, or on another compiler.

### Memory Allocation

In framework code, the best course is to avoid allocating memory altogether, if you can help it. If you need a temporary buffer for some reason, it’s usually better to use the stack than to allocate a buffer. However, stack is limited in size (usually 512 kilobytes altogether), so the decision to use the stack depends on the function and the size of the buffer you need. Typically if the buffer size is 1000 bytes (or `MAXPATHLEN`) or less, using the stack is acceptable.

One refinement is to start off using the stack, but switch to a `malloc`’ed buffer if the size requirements go beyond the stack buffer size. [Listing 2](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/FrameworkImpl.html#//apple_ref/doc/uid/20001286-1008754-BAJHEFCE) presents a code snippet that does just that:

**Listing 2**  Allocation using both stack and malloc’ed buffer

| `#define STACKBUFSIZE (1000 / sizeof(YourElementType))` |
| ---------------------------------------- |
| ` YourElementType stackBuffer[STACKBUFSIZE];` |
| ` YourElementType *buf = stackBuffer;`   |
| ` int capacity = STACKBUFSIZE;  // In terms of YourElementType` |
| ` int numElements = 0;  // In terms of YourElementType` |
| ` `                                      |
| `while (1) {`                            |
| `    if (numElements > capacity) {  // Need more room` |
| `        int newCapacity = capacity * 2;  // Or whatever your growth algorithm is` |
| `        if (buf == stackBuffer) {  // Previously using stack; switch to allocated memory` |
| `            buf = malloc(newCapacity * sizeof(YourElementType));` |
| `            memmove(buf, stackBuffer, capacity * sizeof(YourElementType));` |
| `        } else {  // Was already using malloc; simply realloc` |
| `            buf = realloc(buf, newCapacity * sizeof(YourElementType));` |
| `        }`                              |
| `        capacity = newCapacity;`        |
| `    }`                                  |
| `    // ... use buf; increment numElements ...` |
| `  }`                                    |
| `  // ...`                               |
| `  if (buf != stackBuffer) free(buf);`   |


{% include links.html %}
