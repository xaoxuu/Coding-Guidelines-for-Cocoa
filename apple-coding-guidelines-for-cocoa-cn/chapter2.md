## 二、方法

### 1. 通用原则

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



### 2. getter和setter方法（Accessor Methods）

如果property表示为名词，格式如下

- \- (type)noun;
- \- (void)setNoun:(type)aNoun;  
- \- (BOOL)isAdjective;

```objective-c
- (NSString *)title;
- (void)setTitle:(NSString *)aTitle;
```

如果property表示为形容词，格式如下

- \- (BOOL)isAdjective;
- \- (void)setAdjective:(BOOL)flag;  

```objective-c
- (BOOL)isEditable;
- (void)setEditable:(BOOL)flag;
```

如果property表示为动词，格式如下（动词用一般现在时）

- \- (BOOL)verbObject;
- \- (void)setVerbObject:(BOOL)flag;  

```objective-c
- (BOOL)showsAlpha;
- (void)setShowsAlpha:(BOOL)flag;
```

不要把动词的过去分词形式当作形容词使用  

![1441510445810397](assets/1441510445810397.png)

你可能使用情态动词（can、should、will等）来增加可读性，不过不要使用 do或 does

![1441510455806266](assets/1441510455806266.png)

只有方法需要间接返回多个值的情况下才使用 get

像这种接收多个参数的方法应该能够传入nil，因为调用者未必对每个参数都感兴趣

![1441510465224919](assets/1441510465224919.png)



### 3. Delegate方法

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



### 4. 集合方法



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



### 5. 方法参数



- 参数名以小写字母开始，之后的单词首字母大写

```objective-c
如：removeObject:(id)anObject
```

- 别使用 ”pointer” 或 ”ptr” 命名

- - 参数类型里就已表明它是否是一个指针

- 避免只有一到二个字母的参数名

- 避免只有几个字母的缩写

```objective-c
...action:(SEL)aSelector
...alignment:(int)mode
...atIndex:(int)index
...content:(NSRect)aRect
...doubleValue:(double)aDouble
...floatValue:(float)aFloat
...font:(NSFont *)fontObj  
...frame:(NSRect)frameRect
...intValue:(int)anInt
...keyEquivalent:(NSString *)charCode
...length:(int)numBytes
...point:(NSPoint)aPoint
...stringValue:(NSString *)aString
...tag:(int)anInt
...target:(id)anObject
...title:(NSString *)aString
```



### 6. 私有方法

不要使用下划线作为私有方法的前缀，Apple保留这一使用方式

因为若是你的私有方法名已被Apple使用，覆盖它将会产生极难追踪的BUG

如果继承自大型Cocoa框架（如UIView），请确保子类的私有方法名与父类不一样

可以为私有方法加一个前缀，如公司名或项目名：XX_

例如你的项目叫做Byte Flogger，那么前缀可能是：BF_addObject

总之，为子类的私有方法添加前缀是为了不覆盖其父类的私有方法