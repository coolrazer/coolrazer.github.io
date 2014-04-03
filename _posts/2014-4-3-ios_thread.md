---
layout: post
title: ios多线程
description: "ios thread，runloop"
date: 2014-04-02
modified: 2014-04-02
category: mobile
tags: [ios]
image:
  feature: texture-feature-02.jpg
  credit: Texture Lovers
  creditlink: http://texturelovers.com
comments: true
share: true
---

#### 主线程

- 其他线程的父线程
- 只有主线程有直接修改UI的能力
- 主线程的堆栈大小是1M，其他线程开始都是512KB

#### 创建线程

提供一个函数或方法作为线程入口

##### 使用NSThread创建

1. 创建NSThread对象，调用start方法
2. 创建一个继承自NSThread类的子类，实现其main方法，然后直接创建这个子类的对象
3. 使用 detachNewThreadSelector:ToTarget:withObject: 类方法创建，直接使用目标对象的方法作为线程启动入口

##### 使用NSObject

    performSelectorInBackground:withObject:

##### 使用POSIX Thread

    pthread_create

#### NSOperation和NSOperationQueue

NSOperation封装操作，放到NSOperationQueue中，NSOperationQueue启动新线程执行队列中操作，有序执行


    设置NSOperationQueue并发度：setMaxConcurrentOperationCount:

{% highlight obj-c %}
// 下载网页的功能
1. 用NSInvocationOperation建立一个后台线程，放到NSOperationQueue中，后台执行download
2. download方法下载，完成后调用performSelectorOnMainThread执行download_complete方法
3. download_complete执行clearup工作
{% endhighlight%}

#### GCD

    多核编程的解决方案，blocks

##### dispath queues

可以接受任务，先到先执行。可以并发或串行

类型

1. the main queue：与主线程功能相同，提交至main queue的任务会在主线程中执行，通过dispatch_get_main_queue()获得，串行队列
2. Global queue：全局队列，并发队列，整个进程共享。三个全局队列：高、中（默认）、低三个优先级队列，通过dispatch_get_global_queue传入优先级来访问队列
3. 用户队列。由dispatch_queue_create创建。串行的，可以用来完成同步机制，不再需要使用锁

向队列提交job

- 调用dispatch_asyn函数，传入一个队列和一个block，dispatch_asyn函数立即返回，block在后台执行
- dispatch_sync。等待block执行完成

##### dispatch sources

GCD 10.6支持的事件

1. Mach port send right state changes.
1. Mach port receive right state changes.
1. External process state change.
1. File descriptor ready for read.
1. File descriptor ready for write.
1. Filesystem node event.
1. POSIX signal.
1. Custom timer.
1. Custom event. 调用dispatch_source_merge_data发出信号，DISPATCH_SOURCE_TYPE_DATA_ADD 和 DISPATCH_SOURCE_TYPE_DATA_OR.

##### 使用
{% highlight obj-c %}
// 原代码块一 
self.indicator.hidden = NO; 
[self.indicator startAnimating]; 
dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{ 
    // 原代码块二 
    NSURL * url = [NSURL URLWithString:@"http://www.youdao.com"]; 
    NSError * error; 
    NSString * data = [NSString stringWithContentsOfURL:url encoding:NSUTF8StringEncoding error:&error]; 
    if (data != nil) { 
        // 原代码块三 
        dispatch_async(dispatch_get_main_queue(), ^{ 
            [self.indicator stopAnimating]; 
            self.indicator.hidden = YES; 
            self.content.text = data; 
        }); 
    } else { 
        NSLog(@"error when download:%@", error); 
    } 
}); 
{% endhighlight%}

    GCD定义 类似函数指针，使用 ^定义block

系统提供的方法

{% highlight obj-c %}
//  后台执行： 
 dispatch_async(dispatch_get_global_queue(0, 0), ^{ 
      // something 
 }); 
 // 主线程执行： 
 dispatch_async(dispatch_get_main_queue(), ^{ 
      // something 
 }); 
 // 一次性执行： 
 static dispatch_once_t onceToken; 
 dispatch_once(&onceToken, ^{ 
     // code to be executed once 
 }); 
 // 延迟2秒执行： 
 double delayInSeconds = 2.0; 
 dispatch_time_t popTime = dispatch_time(DISPATCH_TIME_NOW, delayInSeconds * NSEC_PER_SEC); 
 dispatch_after(popTime, dispatch_get_main_queue(), ^(void){ 
     // code to be executed on the main queue after delay 
 }); 
{% endhighlight%}

自定义 dispatch_queue_t
{% highlight obj-c %}
dispatch_queue_t urls_queue = dispatch_queue_create("blog.devtang.com", NULL); 
dispatch_async(urls_queue, ^{ 
     // your code 
}); 
dispatch_release(urls_queue); 
{% endhighlight%}

GCD还有一些高级用法

例如让后台2个线程并行执行，然后等2个线程都结束后，再汇总执行结果。这个可以用dispatch_group, dispatch_group_async 和 dispatch_group_notify

{% highlight obj-c %}
dispatch_group_t group = dispatch_group_create(); 
dispatch_group_async(group, dispatch_get_global_queue(0,0), ^{ 
      // 并行执行的线程一 
 }); 
 dispatch_group_async(group, dispatch_get_global_queue(0,0), ^{ 
      // 并行执行的线程二 
 }); 
 dispatch_group_notify(group, dispatch_get_global_queue(0,0), ^{ 
      // 汇总结果 
 }); 
{% endhighlight%}

默认情况下，在程序块中访问的外部变量是复制过去的，即写操作不对原变量生效。但是你可以加上__block来让其写操作生效

后台运行

    GCD的另一个用处是可以让程序在后台较长久的运行。
    在没有使用GCD时，当app被按home键退出后，app仅有最多5秒钟的时候做一些保存或清理资源的工作。
    使用GCD后，app最多有10分钟的时间在后台长久运行。这个时间可以用来做清理本地缓存，发送统计数据等工作。

#### 线程间通信

##### performSelect

非主线程之间通信，可以将自己的当前线程对象注册到某个全局对象中，这项可以获取对方的线程对象。在主线程中执行 performSelectorOnMainThread:withObject:waitUntilDone

##### Mach Port

父线程创建一个NSMatchPort对象，创建子线程时传递给子线程，子线程可以通过这个MatchPort对象向父线程传递消息。如果父线程要向子线程通信，需要子线程创建另一个NSMachPort对象传递给父线程

[实例](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/Multithreading/RunLoopManagement/RunLoopManagement.html#//apple_ref/doc/uid/10000057i-CH16-SW1)

#### RunLoop

- 处理输入源
    1. performSelector源
    2. 基于端口MachPort源
    3. 自定义源
- 处理定时器

加入事件源 scheduleInRunLoop:forMode:

    每个线程都有对应的RunLoop，但是默认非主线程的Runloop没有运行，需要为RunLoop添加至少一个事件源，然后run
    一般没有必要弃用线程RunLoop，除非要在单独线程中长久检测某个事件

