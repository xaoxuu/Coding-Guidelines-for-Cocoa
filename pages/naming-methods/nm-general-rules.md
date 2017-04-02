---
title: 通用原则
keywords: 代码 命名 基础 通用
last_updated: 2017-04-01
tags:
summary:
sidebar: home_sidebar
permalink: nm-general-rules.html
folder: naming-methods
---


- 以小写字母开始，之后单词的首字母大写

- - 以众所周知的缩写开始可以大写，如TIFF、PDF
  - 私有方法可以加前缀                

- 如果方法代表对象接收的动作，以动词开始

- - 不要使用 do 或 does 作为名字的一部分，因为助动词在这里很少有实际意义
  - 同样的，也别在动词之前使用副词和形容词

 ```objective-c
  - (void)invokeWithTarget:(id)target;
  - (void)selectTabViewItem:(NSTabViewItem *)tabViewItem
  ```

- ​


- 如果方法返回接收者的属性，以 接收者 + 接收的属性 命名

- - 除非间接返回多个值，否则不要使用 get 单词（为了与accessor methods区分） 

![1441510342242240](assets/1441510342242240.png)



在所有参数之前使用关键字



![1441510350190909](assets/1441510350190909.png)



确保参数之前的关键字充分描述了参数



![1441510357744281](assets/1441510357744281.png)



创建自定义 init 方法时，记得指明关联的元素



![1441510364456110](assets/1441510364456110.png)



不要使用 and 来连接作为接收者属性的关键字

- 虽然下面的例子使用 and 看似不错，但是一旦参数非常多时就容易出现问题

![1441510376939244](assets/1441510376939244.png)



除非方法描述了两个独立的操作，才使用 and 来连接它们



![1441510386160791](assets/1441510386160791.png)


{% include links.html %}
