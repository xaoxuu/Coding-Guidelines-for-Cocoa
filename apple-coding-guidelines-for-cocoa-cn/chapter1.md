## 一、代码命名基础

### 1. 通用原则

#### 1.1 清晰

尽量清晰又简洁，无法两全时清晰更重要


![](assets/1441509819955470.png)

通常不应缩写名称，即使方法名很长也应完整拼写

你可能认为某个缩写众所周知，但其实未必，特别是你周围的开发者语言文化背景不同时  
有一些历史悠久的缩写还是可以使用的，详见[第五章](chapter5.md)

![](assets/1441509896749042.png)

API命名避免歧义，例如一个方法名有多种理解

![](assets/1441509905881130.png)

#### 1.2 一致

尽力保持Cocoa编程接口命名一致

如果有疑惑，请浏览当前头文件或者参考文档  
当某个类的方法使用了多态时，一致性尤其重要

不同类里，功能相同的方法命名也应相同

![](assets/1441509959926816.png)

#### 1.3 避免自引用（self Reference）

命名不应自引用

这里的自引用指的是在词尾引用自身

![](assets/1441509975783777.png)

Mask与Notification忽略此规则

![](assets/1441509984966357.png)

### 2. 前缀

前缀是编程接口命名的重要部分，它们区分了软件的不同功能区域：

* 前缀可以防止第三方开发者与Apple的命名冲突

* * 同样可以防止Apple内部的命名冲突
* 前缀有指定格式

* * 它由二到三个大写字母组成，不使用下划线和子前缀
* 命名类、协议、函数、常量和typedef结构体时使用前缀

* * 方法名不使用前缀（因为它存在于特定类的命名空间中）
  * 结构体字段不使用前缀

![1441510038800340](assets/1441510038800340.png)

### 3. 书写约定

在命名API元素时， 使用驼峰命名法（如runTheWordsTogether），并注意以下书写约定：

**方法名**

* 小写第一个字母，大写之后所有单词的首字母，不使用前缀
* 如果方法名以一个众所周知的大写缩略词开始，该规则不适用

如TIFFRepresentation \(NSImage\)

```objective-c
fileExistsAtPath:isDirectory:
```

**函数及常量名**

* 使用与其关联类相同的前缀，并大写首字母

```objective-c
NSRunAlertPanel
NSCellDisabled
```

**标点符号**

* 由多个单词组成的名称，别使用标点符号作为名称的一部分

* * 分隔符（下划线、破折号等）也不能使用
* 避免使用下划线作为私有方法的前缀，Apple保留这一方式的使用

* * 强行使用可能会导致命名冲突，即Apple已有的方法被覆盖，这会导致灾难性后果
  * 实例变量使用下划线作为前缀还是允许的

### 4. class与protocol命名

**class**

* class的名称应该包含一个名词，用以表明这个类是什么（或者做了什么），并拥有合适的前缀
* 如NSString、NSDate、NSScanner、UIApplication、UIButton

**不关联class的protocol**

* 大多数protocol聚集了一堆相关方法，并不关联class

* 这种protocol使用ing形式以和class区分开来

  ​

  ![1441510247983445](assets/1441510247983445.png)

**关联class的protocol**

* 一些protoco聚集了一堆无关方法，并试图与某个class关联在一起，由这个class来主导

* * 这种protocol与class同名

  * * 如NSObject protocol

### 5. 头文件

头文件的命名极其重要，因为它可以指出头文件包含的内容：

* 声明一个孤立的class或protocol

* * 将声明放入单独的文件
  * 使头文件名与声明的class/protocol相同
* ![1441510258390459](assets/1441510258390459.png)

* 声明关联的class或protocol

* * 将关联的声明（class/category/protocol）放入同一个头文件
  * 头文件名与主要的class/category/protocol相同
* ![1441510278719846](assets/1441510278719846.png)

* Framework头文件

* * 每个framework都应该有一个同名头文件
  * Include了框架内其他所有头文件
* ![1441510294801244](assets/1441510294801244.png)

* 添加API到另一个framework

* * 如果要在一个framework中为另一个framework的class catetgory添加方法，加上单词“Additions”

  * * 如Application Kit的NSBundleAdditions.h 文件
* 关联的函数、数据类型

* * 如果你有一组关联的函数、常量、结构体或其他数据类型，将它们放到一个名字合适的头文件中

  * * 如Application Kit的NSGraphics.h