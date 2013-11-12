---
layout: post
title: ios技术
description: "ios technology"
date: 2013-11-12
modified: 2013-11-12
category: mobile
tags: [ios]
image:
  feature: texture-feature-04.jpg
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

[iOS Technology Overview](https://developer.apple.com/library/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007898)

### Cocoa Touch

#### - 高级功能

**AirDrop**

    附近设备之间分享照片, 文档, URL和其他数据.

- 发送文件 [UIActivityViewController](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIActivityViewController_Class/Reference/Reference.html#//apple_ref/occ/cl/UIActivityViewController)

- 接收文件
  1. 在Xcode(Inof.plist)中声明支持相关的文档类型
  2. 在app delegate中实现[application:openURL:sourceApplication:annotation:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIApplicationDelegate_Protocol/Reference/Reference.html#//apple_ref/occ/intfm/UIApplicationDelegate/application:openURL:sourceApplication:annotation:)
  3. 接受文件默认保存在apDocuments/Inbox目录中

**文本**

    处理文本和排版, 可以将格式文本布局到段落, 列, 页面中, 文字环绕, 管理多字体.

- [NSAttributedString](https://developer.apple.com/library/ios/documentation/UIKit/Reference/NSAttributedString_UIKit_Additions/Reference/Reference.html#//apple_ref/occ/cl/NSAttributedString)支持新属性
- [NSLayoutManager](https://developer.apple.com/library/ios/documentation/UIKit/Reference/NSLayoutManager_Class_TextKit/Reference/Reference.html#//apple_ref/occ/cl/NSLayoutManager)生成自行并布局
- [NSTextContainer](https://developer.apple.com/library/ios/documentation/UIKit/Reference/NSTextContainer_Class_TextKit/Reference/Reference.html#//apple_ref/occ/cl/NSTextContainer)定义文字布局的区域
- [NSTextStorage](https://developer.apple.com/library/ios/documentation/UIKit/Reference/NSTextStorage_Class_TextKit/Reference/Reference.html#//apple_ref/occ/cl/NSTextStorage)管理基于文字的内容的基础接口

- [文本开发指南](https://developer.apple.com/library/ios/documentation/StringsTextFonts/Conceptual/TextAndWebiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009542)

**[UIKit动态](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIKit_Framework/_index.html#//apple_ref/doc/uid/TP40006955)**

    指定UIView对象和符合UIDynamicItem协议的对象的动态行为, 动态行为在添加到动画对象(UIDynamicAnimator的实例)后激活, 支持如下行为

- [UIAttachmentBehavior](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIAttachmentBehavior_Class/Reference/Reference.html#//apple_ref/occ/cl/UIAttachmentBehavior)指定两个动态物体或一个物体和一个点之间的连接, 当一个物体(或点)移动, 另外一个关联物体同时移动
- [UICollisionBehavior](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UICollisionBehavior_Class/Reference/Reference.html#//apple_ref/occ/cl/UICollisionBehavior)动态物体参与其他物体或边界碰撞
- [UIGravityBehavior](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIGravityBehavior_Class/Reference/Reference.html#//apple_ref/occ/cl/UIGravityBehavior)指定重力矢量, 动态物体沿指定方向加速直到碰撞到相关物体或边界
- [UIPushBehavior](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIPushBehavior_Class/Reference/Reference.html#//apple_ref/occ/cl/UIPushBehavior)指定连续或瞬时力矢量
- [UISnapBehavior](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UISnapBehavior_Class/Reference/Reference.html#//apple_ref/occ/cl/UISnapBehavior) 指定快照点, 物体在这个点获得指定效果
 
**多任务**

    后台执行 

- 应用能请求有限的时间来完成重要的工作
- 支持特殊服务(如音频播放), 能请求时间提供此服务
- 在特定事件使用本地通知来生成用户alerts, 无论app是否运行
- 定期从网络上下载内容
- 响应推送通知时下载内容

- [ios开发指南](https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007072)

**自动布局**

    帮助创建动态UI, 使用规则来描述布局元素.
    constraints    

- 通过单独替换字符串支持本地化
- 对右->左的语言(如Hebre和Arabic)提供UI镜像
- 更好的分离视图和控制器

- [自动布局指南](https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/AutolayoutPG/Introduction/Introduction.html#//apple_ref/doc/uid/TP40010853)

**[Storyboards](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIStoryboard_Class/Reference/Reference.html#//apple_ref/doc/uid/TP40010909)**

    设计UI

- [Xcode概述](https://developer.apple.com/library/ios/documentation/ToolsLanguages/Conceptual/Xcode_Overview/About_Xcode/about.html#//apple_ref/doc/uid/TP40010215)

**UI状态保存**

    app从前台调到后台将保存视图和视图控制器的状态, 在下次启动循环可以使用保存信息恢复视图和视图控制器

- [ios开发指南](https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007072)

**推送服务**

    提示用户新信息, 甚至app没有在运行
    可以推送文字通知, app的图像徽章, 或者声音警告, 或者无声通知来知会app有新的内容下载    

- app需要请求通知的分发, 并在通知分发后处理通知数据 
- 提供服务器测的处理来生成通知

- [本地及推送通知开发指南](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Introduction.html#//apple_ref/doc/uid/TP40008194)

**本地通知**

    本地推送通知

- [本地及推送通知开发指南](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Introduction.html#//apple_ref/doc/uid/TP40008194)

**[手势识别](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIGestureRecognizer_Class/Reference/Reference.html#//apple_ref/occ/cl/UIGestureRecognizer)**

    手势识别检测常用的手势类型, UIKit提供标准的手势识别子类来检测点击, 滑动, 缩放, 旋转

- [事件处理指南](https://developer.apple.com/library/ios/documentation/EventHandling/Conceptual/EventHandlingiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009541)

**标准系统视图控制器**

    尽可能使用提供的视图控制器, 而不是创建一个

- 地址簿UI --  显示/编辑联系人信息
- 事件UI --  创建/编辑日历事件
- 消息UI --  构成email或短信消息
- UIKit [UIDocumentInteractionController](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIDocumentInteractionController_class/Reference/Reference.html#//apple_ref/occ/cl/UIDocumentInteractionController) --  打开或预览文件内容
- UIKit [UIImagePickerController](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIImagePickerController_Class/UIImagePickerController/UIImagePickerController.html#//apple_ref/occ/cl/UIImagePickerController) -- 打开图片或选择照片
- UIKit  [UIImagePickerController](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIImagePickerController_Class/UIImagePickerController/UIImagePickerController.html#//apple_ref/occ/cl/UIImagePickerController) -- 视频剪切

- [视图控制器开发指南](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007457)
- [视图控制器目录](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewControllerCatalog/Introduction.html#//apple_ref/doc/uid/TP40011313)

#### - Cocoa Touch 框架

**[地址簿](https://developer.apple.com/library/ios/documentation/AddressBookUI/Reference/AddressBookUI_Framework/_index.html#//apple_ref/doc/uid/TP40007082)**

    AddressBookUI.framework - 创建, 修改, 选择联系人

  - [地址簿开发指南](https://developer.apple.com/library/ios/documentation/ContactData/Conceptual/AddressBookProgrammingGuideforiPhone/Introduction.html#//apple_ref/doc/uid/TP40007744)

**[事件](https://developer.apple.com/library/ios/documentation/EventKitUI/Reference/EventKitUIFrameworkRef/_index.html#//apple_ref/doc/uid/TP40009663)**

     EventKitUI.framework - 提供视图控制器呈现标准系统接口以查看或编辑日历相关事件

**[游戏中心](https://developer.apple.com/library/ios/documentation/GameKit/Reference/GameKit_Collection/_index.html#//apple_ref/doc/uid/TP40008303)**

    GameKit.framework - 游戏中心, 用户分享游戏相关内容

- 创建在线人物, 和其他用户交流
- 排行榜
- 对接其他用户, 在线多人游戏
- 成就, 记录用户的最高记录
- 挑战, 允许用户向朋友挑战一个记录或分数
- 回合制游戏, 配对

- [游戏中心开发指南](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/GameKit_Guide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40008304)

**[iAd](https://developer.apple.com/library/ios/documentation/UserExperience/Reference/iAd_ReferenceCollection/_index.html#//apple_ref/doc/uid/TP40009705)**

    iAd.framework - 广告条

- [iAd开发指南](https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/iAd_Guide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009881)

**[地图](https://developer.apple.com/library/ios/documentation/MapKit/Reference/MapKit_Framework_Reference/_index.html#//apple_ref/doc/uid/TP40008210)**

    MapKit.framework - 带滚动条的地图, 可合并到app的UI中, 通过framework接口定制地图内容, 和apple的地图服务器交互

- [位置和地图开发指南](https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/LocationAwarenessPG/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009497)    

**[消息](https://developer.apple.com/library/ios/documentation/MessageUI/Reference/MessageUI_Framework_Reference/_index.html#//apple_ref/doc/uid/TP40008274)**

    MessageUI.framework - 构成email或SMS消息

- [ios系统消息开发指南](https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/SystemMessaging_TopicsForIOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40010404)

**Twitter**

    Social.framework - 生成tweets和登录到Twitter服务器

**[UIKit](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIKit_Framework/_index.html#//apple_ref/doc/uid/TP40006955)**

    UIKit.framework - ios应用的关键基础组件

- 基本的app管理和基础组件, 包括app的主事件循环
- UI管理, 包括storyboards和nib文件支持
- 一个包装了用户接口内容的视图控制器模型
- 代表标准系统视图和控制器的对象
- 点击和移动事件处理
- 文档模型, 支持iCloud交互, 参考[基于文档的应用开发指南](https://developer.apple.com/library/ios/documentation/DataManagement/Conceptual/DocumentBasedAppPGiOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40011149)
- 图形和窗口支持, 包括支持额外的显示, 参考[视图开发指南](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009503)
- 多任务支持
- 打印支持, 参考[ios绘画和打印指南](https://developer.apple.com/library/ios/documentation/2DDrawing/Conceptual/DrawingPrintingiOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40010156)
- 定制标准UIKit控件外形
- 文本和web内容
- 剪切, 拷贝和粘贴
- 用户接口内容动画
- 通过URL和framework接口和其他应用交互
- 访问控制
- apple推送通知服务
- 本地通知调度分发
- PDF生成
- 使用定制的类似系统键盘的输入视图
- 创建定制的可与系统键盘交互的文本视图
- 通过email, Twitter, Facebook其他服务分享内容

- 摄像头
- 用户照片库
- 设备名字和模型
- 电池
- 传感器
- 连接耳机的远程控制信息

### 媒体层

#### - 图像

- UIKit图像

    画图 画贝兹路径 视图内容动画
    
- 核心图形框架, Quartz

    ios应用的原生画图引擎, 提供2D 矢量和基于图形的渲染

- 核心动画 Quartz核心框架的一部分

    UIKit视图使用核心动画提供视图层的动画支持

- 核心图形

    操作视频并无损的静止图像

- OpenGL ES和GLKit

    OpenGL ES使用硬件加速接口渲染2D和3D
    
    GLKit为OpenGL ES提供面向对象的接口
    
- 文本Kit和核心文本
    
- 图形IO

    支持更多图片格式

- 资产库

    使用用户的照片, 视频, 媒体文件

#### - 音频

- Media Player
- AV Foundation
- OpenAL
- 核心Audio

#### - 视频

- [UIImagePickerController](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIImagePickerController_Class/UIImagePickerController/UIImagePickerController.html#//apple_ref/occ/cl/UIImagePickerController)

     选择用户的媒体文件, 参考[摄像头开发指南](https://developer.apple.com/library/ios/documentation/AudioVideo/Conceptual/CameraAndPhotoLib_TopicsForIOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40010400)

- Media Player
- AV Foundation     
- 核心Media

#### - AirPlay


### 核心服务

#### 高层功能

点对点服务

iCloud存储

自动应用技术

块对象

数据保护

文件共享支持

中央调度

app内支付

sqlite

xml支持

### 核心OS层

