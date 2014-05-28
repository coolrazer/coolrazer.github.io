---
layout: post
title: lldb调试
description: "LLDB调试器"
date: 2014-05-28
modified: 2014-05-28
category: mobile
tags: [ios]
image:
  feature: texture-feature-04.jpg
  credit: Texture Lovers
  creditlink: http://texturelovers.com
comments: true
share: true
---


#### p 输出基本类型
#### po 输出 Objective-C 对象

#### 查询历史记录 $[0-9]+
po $1

#### expr 动态执行表达式
	常用于修改变量值
	声明新变量对象，对象名前要加$

#### call 调用
	po p也有调用功能，一般在不需要显示输出，或是方法无返回值时使用call。

#### bt 打印调用堆栈
加all可打印所有thread的堆栈

#### image
image 命令可用于寻址，有多个组合命令。比较实用的用法是用于寻找栈地址对应的代码位置。
image lookup --address 0x0000000100004af8