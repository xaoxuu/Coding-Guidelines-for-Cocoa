## 四、Property及其他

### 1. Property与实例变量

#### 1.1 Property

Property命名规则与第二章accessor methods一样（因为两者紧密联系）

如果property表示为一个名词或动词，格式如下

@property (…) 类型 名词/动词 ;

```objective-c
@property (strong) NSString *title;
@property (assign) BOOL showsAlpha;
```

如果property表示为一个形容词

- 可省略 ”is” 前缀
- 但要指定getter方法的惯用名称

```objective-c
@property (assign, getter=isEditable) BOOL editable;
```

#### 1.2 实例变量

通常不应该直接访问实例变量

init、dealloc、accessor methods等方法内部例外

实例变量以下划线 “_” 开始

确保实例变量描述了所存储的属性

```objective-c
@implementation MyClass {
   BOOL _showsTitle;
}
```

如果想要修改property的实例变量名，使用 @synthesize语句

```objective-c
@implementation MyClass
@synthesize showsTitle=_showsTitle;
```

为一个class添加实例变量时，有几点需要注意：

- 避免声明公有实例变量

- - 开发者关注的应该是对象接口，而不是其数据细节
  - 你可以通过使用property来避免声明实例变量

- 如果需要声明实例变量，指定关键字@private 或 @protected

- - 如果你希望子类可以直接访问某个实例变量，使用 @protected 关键字

- 如果一个实例变量是某个类可访问的属性，确保写了accessor methods

- - 如果有可能，还是使用property



### 2.常量

#### 2.1 枚举常量

使用枚举来关联一组integer常量  

枚举常量和typedef遵循函数的命名规范，下面的例子是 NSMatrix.h

```objective-c
typedef enum _NSMatrixMode {
    NSRadioModeMatrix            = 0,
    NSHighlightModeMatrix       = 1,           
    NSListModeMatrix            = 2, 
    NSTrackModeMatrix           = 3
} NSMatrixMode;
```

你可以为bit masks之类的东西创建一个匿名枚举 

```objective-c
enum { 
    NSBorderlessWindowMask       = 0, 
    NSTitledWindowMask           = 1 << 0,
    NSClosableWindowMask         = 1 << 1,
    NSMiniaturizableWindowMask   = 1 << 2, 
    NSResizableWindowMask         = 1 << 3
};
```

**2.2 使用const关键字的常量 **

使用const关键字来创建一个float常量

你可以使用const关键字来创建一个与其他常量不相关的integer常量，否则，使用枚举

使用const关键字的常量也遵循函数的命名规则 

```objective-c
const float NSLightGray;
```



#### 2.3 其他常量类型

- 通常不应使用 #define 预编译指令来创建常量

- - integer常量，使用枚举
  - float常量，使用 const 修饰符

- 对 #define 预编译指令，大写所有字母

- - 比如 DEBUG 判断

- ```objective-c
  #ifdef DEBUG
  ```

- ​


- 注意宏命令的字首和字尾都有双下划线 

```objective-c
__MACH__
```



- 定义NSString常量来作为Notification和Key值

- - 这样做可以有效防止拼写错误

```objective-c
APPKIT_EXTERN NSString *NSPrintCopies;
```





### 3. Notifications与Exceptions

#### 3.1 Notifications

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

#### 3.2 Exceptions

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

