---
layout: post
title: ios开发路线图
description: "ios development roadmap"
date: 2013-11-11
modified: 2013-11-11
category: mobile
tags: [ios]
image:
  feature: texture-feature-03.jpg
  credit: Texture Lovers
  creditlink: http://texturelovers.com
comments: true
share: true
---

<section id="table-of-contents" class="toc">
  <header>
    <h3>目录</h3>
  </header>
<div id="drawer" markdown="1">
*  Auto generated table of contents
{:toc}
</div>
</section><!-- /#table-of-contents -->

[马上着手开发 iOS 应用程序](https://developer.apple.com/library/ios/referencelibrary/GettingStarted/RoadMapiOSCh/chapters/Introduction.html)

### 第一个应用

[首个 iOS 应用程序](https://developer.apple.com/library/ios/referencelibrary/GettingStarted/RoadMapiOSCh/chapters/RM_YourFirstApp_iOS/Articles/00_Introduction.html)

工具 Tool 技术 Technologies 技巧 Techniques

#### 程序启动

main函数

{% highlight objc %}
int main(int argc, char * argv[])
{
    @autoreleasepool {
        return UIApplicationMain(argc, argv, nil, NSStringFromClass([HelloWorldAppDelegate class]));
    }
}
{% endhighlight%}

- @autoreleasepool 支持自动引用计数(ARC)
- UIApplicationMain 创建一个UIApplication类的实例和一个应用程序委托的实例, 扫扫描Info.plist文件

串联图

- 包括场景和过渡
- 场景代表视图控制器, 过渡表示两个场景之间的转换
- 初始场景指示器, 标识出应用程序启动首先载入的场景

视图控制器

- 第一响应占位符对象(橙色立方体), 动态占位符, 第一个接受各种事件的对象.
- Exit的占位符对象, 用于展开序列. 默认情况下子场景消失时,该场景的视图控制器展开或返回父场景, 不过通过exit对象可是使视图展开任意场景
- XXXViewController对象(黄色球体内的浅色矩形) 串联图载入一个场景会创建一个视图控制器的实例来管理该场景
- 一个视图(View)

### object-c代码

c语言的超集

- 定义新的类
- 类和实例方法
- 方法调用(发消息)
- 属性声明(自动合成存取方法)
- 静态和动态类型化
- 块block, 已封装的, 可以在任何时候执行的多段代码
- 基本语言的扩展, 例如协议和类别

#### 类和对象

类: 封装数据, 定义对数据执行的操作

对象: 类的运行时实例, 包含自己的实例变量(由类声明)的内存副本, 以及类的方法的指针, 可以采用两步法(分配, 初始化)创建对象

- .h 头文件, 包含类\类型\函数\常量的声明
- .m 实现文件, 可同时包含obj-c和c代码
- .mm 实现文件, 可同时包含obj-c,c,c++代码

导入(#import指令)
{% highlight objc %}
#import <Gizmo/Gizmo.h>
{% endhighlight%}

类声明

- 类的声明以@interface开始, @end结束
- 类后面(冒号分隔)时父类名称, 一个类只能有一个父类
- 在@interface开始和@end之间编写属性和方法声明, 组成类的公共接口, 用分号标记每个属性和方法的结尾
- 类具有于公共接口相关的自定函数\常量\数据类型, 将他们的声明放到@interface...@end之外

类实现

- 类的实现以@implement开始, @end结束, 中间是方法实现
- 函数实现应在@implement...@end之外
- 一个实现应该总是将导入它的接口文件作为代码第一行

包含对象的变量, obj-c支持动态类型化和静态类型化

- 动态类型化, 给对象使用类型id
- 静态类型化, 变量名称前放置一个*号

在objc中执行对象引用的只能是指针, id类型意味着一个指针

#### 方法和发消息

方法声明: 方法类型标识符(实例方法: - 类方法: +), 返回类型, 一个或多个签名关键字(包括冒号字符在内的所有签名关键字的串联, 冒号表示有参数存在), 参数类型及名称信息

调用方法通过给实施该方法的对象发送一则消息实现, 消息表达式使用[]将消息本身及参数括起来, 可以使用点记语法调用存取方法, 点记法表达式中不能使用对动态类型化的对象(类型为id)的引用

类方法:接受消息的对象时类

#### 声明的属性和存取方法

@property指令

#### 块

{% highlight objc %}
int (^myblock)(int) = ^(int num){return num * num;};
{% endhighlight%}

块共享局部词法作用范围内的数据, 如方法的局部变脸, 参数(包括堆栈变量), 函数及全局变量. 访问时只读的, 除非使用__block修饰声明变量

即使包含块的方法或函数已经返回, 并且其局部作用范围已销毁, 但是只要存在对该块的引用, 局部变量仍作为块对象的一部分继续存在

块可作为方法或函数的参数用作回调

#### 协议和类别

#### 已定义的类型和编码策略

|类型|描述和字面常量|
|:---:|:---:|:------:|:------------:|
|id| 动态对象类型。动态类型化的对象和静态类型化的对象的否定字面常量，都是 nil。 |
|class| 动态类类型。其否定字面常量是 Nil。 |
|SEL| .选择器的数据类型 (typedef)；此数据类型表示运行时的方法签名。其否定字面常量是 NULL|
|BOOL| Boolean 类型。字面常量值是 YES 和 NO。|
|:---:|:---:|:------:|:------------:|
{: rules="groups"}

self 可以在消息实现内使用的局部变量, 引用当前对象

super

### 基本编程技能

Foundation 框架

- 根类及相关协议。根类 NSObject 及其同名协议指定了所有 Objective-C对象的基本接口和行为。还有一些协议可以由类采用，以便客户端可以拷贝类的实例并对其状态进行编码。
- 值类。值类产生的实例称为值对象，是一种面向对象的包装器(wrapper)，用于基本的数据类型（如字符串、数字、日期或二进制数据）。同一值类的实例，如果具有相同的封装值，则视为是相等的。
- 集 (collection) 类。集类的实例（称为集）管理一组的对象。区分特定集类型的关键，在于它让您如何使用所包含的对象。集 (collection)中的项通常是值对象。

#### 根类NSObject

NSObject类及相关协议的方法, 用于创建对象, 导航继承连, 询问对象的特征和功能, 比较对象, 拷贝对象, 对对象编码

#### 创建对象

分配+初始化

- 发送alloc消息给对象的类获取一个原始实例
- 初始化, 将一个对象的初始状态设定为合理的值,然后返回对象

通过类的工厂方法创建对象

#### 强引用 弱引用

在变量名前使用__weak限定符, 标记为弱

委托, 未引用顶级对象的Outlet, 目标, 块内对self的引用 应该都标记为弱引用

#### 值对象

表示标量值

#### 创建和使用集

#### 运行时验证对象

内省

- 是否特定类或其子类的实例, isKindOfClass:, 将类型为Class的对象作为参数, 在类符号上调用class方法
- 是否响应消息, respondsToSelector:, 将选择器作为器参数, 选择器是obj-c的数据类型, 用于方法的运行时标识符(runtime identifiers), 使用@selector编译器指令指定选择器
- 是否遵守协议, conformsToProtocol:, 将协议的运行时标示符视为参数, 使用@protocol指定此标示符

#### 比较对象

isEqual, 不同于对象相同 == 测试两个变量是否指向同一个实例

Foundation框架的值和集类, 声明的比较方法为isEqualToType:, 如isEqualToString: 和 isEqualToDictionary:

#### 拷贝对象

copy 对象必须遵守NSCopying协议

### 框架

ios应用程序基于Doundation和UIKit框架

Foundation 为所有应用程序提供基本的系统服务

- 创建和管理集, 如数组和字典
- 访问存储在应用程序的中的图像和其他资源
- 创建和管理字符窜
- 发布和观察通知
- 创建日期和时间对象
- 自动发现IP网络上的设备
- 操控URL流
- 异步执行代码

UIKit创建基于触摸的用户界面

- 创建和管理用户界面
- 处理基于触摸和运动的事件
- 显示文本和网页内容
- 优化应用程序以实现多任务
- 创建自定用户界面元素

Core Data管理应用程序数据模型, 内建sqlite

- 存储对象和从储存处取回对象
- 支持基本的销毁/重做
- 自动验证属性值
- 对内存数据进行过滤\分组和整理
- 使用NSFetchedResultsController管理表格中的视图
- 支持基于文稿的应用程序

Core Graphics创建图形, 又称作Quartz

- 制作基于路径的绘图
- 使用边缘模糊化渲染
- 添加渐变\图像和颜色
- 使用坐标空间变换
- 创建\显示和解析pdf文稿

Core Animation制作高级动画和视觉效果

- 创建自定动画
- 给图形添加时序功能
- 支持关键帧动画
- 指定图形布局约束
- 将多层更改分组为原子更新

OpenGL ES提供2D和3D绘图工具

- 创建2D和3D图形
- 制作更复杂的图形, 如数据可视化\飞行模拟或视频游戏
- 访问底层图形硬件

### 设计模式

MVC

委托: 代表另一个对象

协议: 不相关的对象之间能通过继承进行通信

通知中心: 通知观察者

目标-操作: 事件发生时封装待发送的消息

键值观察: 允许对象观察另一个对象的属性, 属性值改变时通知观察对象

视图层次: 允许应用程序将单个视图和合成视图同等对待

响应链

视图控制器

前台

类别

### 用户界面设计

从用户角度设计

设计原则

- 美学集成度(aesthetic integrity) 不是衡量应用程序有多好看；而是看应用程序的外观和它的功能融合得有多紧密。
- 一致性。让用户把对一个应用程序的知识和技巧，应用到另一个应用程序。理想情况下，应用程序应与 iOS 标准、其本身及较早版本相一致。
- 直接操控。当用户直接操控屏幕上的对象（而不是透过别的控制），他们会更加专注于任务，并且更容易理解操作的结果。
- 反馈。通过反馈来确认用户的操作，并让他们确信处理正在进行。例如，当用户操作控制时，他们期望得到即时的反馈；进行长时间的操作时，则希望看到状态的更新。
- 隐喻。如果应用程序中的虚拟对象和操作，隐喻着现实世界中的对象和操作，用户会迅速理解如何使用应用程序。最适当的隐喻，会启发一种用法和体验，而不是把所基于的现实世界对象或行动的限制强加实施。
- 用户控制。虽然应用程序可以建议一系列操作，或者对危险的后果提出警告，但是如果不给用户做决定，则通常是错误的。最好的应用程序，会在给予用户所需的功能和帮助他们避免危险的结果之间，找到正确的平衡。

用户体验指南

- 聚焦于主要任务。
- 让用法简单和明确。
- 使用以用户为中心的术语。
- 制作指尖大小的目标。
- 不强调设置。
- 一致地使用用户界面 (UI) 元素。
- 使用令人会意的动画来沟通。
- 仅在必要时要求用户进行存储。

ios技术指南

- 简单清晰地支持 iCloud 储存。
- 做好与多任务相关的中断和恢复准备。
- 处理本地通知和推送通知时，遵循用户的“通知中心”设置。
- 提供叙述信息，以便 VoiceOver 用户操作应用程序。
- 依赖系统提供的打印 UI，为用户带来满意的打印体验。
- 确保声音在各种情形下，都满足用户的期望。

UI元素使用指南

- 确保导航栏中的返回按钮，显示上一个屏幕的标题。
- 当标签功能不可用时，不要将标签从标签栏移除。
- 避免提供“隐藏弹出式窗口”按钮。
- 当用户选择表格视图所列出的项目时，要提供反馈。
- 在 iPad 上，仅在弹出式窗口内显示挑选器。
- 使用系统提供的按钮和图标时，遵从它们定义好的含义。
- 设计自定图标和图像时，使用所有用户都理解的通用图像，避免复制 Apple 的 UI 元素或产品。

设计策略

- 提炼功能列表
- 为设备而设计
- 适当的定制
- 原型和迭代

### 应用程序设计

#### 应用程序核心对象

<img src="/images/post/core_objects_2x.png">

对象角色

|对象|说明|
|:---:|:---|
|UIApplication 对象| 管理应用程序事件循环，并协调其他高级的应用程序行为.定制的应用程序级的逻辑，存在于应用程序的委托对象中，并与此对象紧密合作 |
|:---:|:---|
|应用程序委托对象| 是在应用程序启动时，创建的一个自定对象，通常由 UIApplicationMain函数创建。主要用于处理应用程序内部的状态转换。在 iOS 5 和更高版本中，您可以使用应用程序委托，来处理其他与应用程序相关的事件。Xcode 项目模板将应用程序委托声明为 UIResponder 的子类。如果UIApplication 对象不处理事件，它会将事件分派给应用程序的委托，以进行处理。|
|:---:|:---|
|文稿和数据模型对象| 数据模型对象储存应用程序的内容, 文稿对象（UIDocument 的自定子类），来管理其数据模型对象中的一部分或全部|
|:---:|:---|
|视图控制器对象|管理应用程序内容在屏幕上的呈现。视图控制器管理单个视图及其分视图。呈现时，视图控制器将视图安装到应用程序的窗口中，使它们显示出来, UIViewController类是所有视图控制器对象的基础类。它提供了一些默认功能，用于载入视图、呈现视图和旋转视图，以响应设备的旋转以及几个其他标准的系统行为。UIKit 和其他框架定义附加的视图控制器类，来实现标准系统界面|
|:---:|:---|
|UIWindow 对象|协调一个或多个视图在屏幕上的呈现。大多数应用程序只有一个窗口，用于在主屏幕上呈现内容，但应用程序可能会有另外一个窗口，将内容显示在外接显示器上。要更改您的应用程序的内容，需使用视图控制器，来更改在对应窗口中显示的视图。您不会把窗口本身替换。除了充当视图的宿主以外，窗口还配合 UIApplication 对象工作，将事件传送到视图和视图控制器。|
|:---:|:---|
视图、控制和层对象|视图和控制将应用程序的内容直观地呈现出来。视图是一种对象，将内容绘制在指定的矩形区域内，并响应该区域的事件。控制是一类专门的视图，负责实施常见的界面对象，如按钮、文本栏和切换开关。UIKit 框架提供标准的视图，用于呈现许多类型的内容。通过直接将 UIView（或它的子类）子类化，您还可以定义自己的自定视图。除了包括视图和控制以外，应用程序还可以将 Core Animation层并入其视图和控制分层结构中。层对象实际是代表视觉内容的数据对象。视图在幕后大量使用层对象，来渲染其内容。您还可以将自定的层对象，添加到界面，以实施复杂的动画和其他类型的复杂视觉效果。 |
{: rules="groups"}

#### 国际化

使用Base Internationalization

Localizable.string

### 进阶

[iOS 技术概述](https://developer.apple.com/library/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007898) 介绍可在 iOS 应用程序中使用的框架和其他技术。
[iOS 用户界面指南](https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/MobileHIG/index.html#//apple_ref/doc/uid/TP40006556) 教您如何让您的应用程序符合 iOS 用户界面规范。
[应用程序分发指南](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40012582) 逐步完成这些过程：开发应用程序，预备测试设备，提交应用程序到 App Store。
[使用 Objective-C 编程](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/Introduction/Introduction.html#//apple_ref/doc/uid/TP40011210) 描述如何使用 Objective-C 程序设计语言定义类、发送消息、封装数据，以及完成各种其他任务。
[iOS 应用程序编程指南](https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007072)讲解在开发 iOS 应用程序时，您必须要了解并做到的基本事情。
