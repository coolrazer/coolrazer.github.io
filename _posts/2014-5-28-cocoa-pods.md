---
layout: post
title: cocoapods
description: "cocoapods 包管理"
date: 2014-05-28
modified: 2014-05-28
category: mobile
tags: [ios]
image:
  feature: texture-feature-05.jpg
  credit: Texture Lovers
  creditlink: http://texturelovers.com
comments: true
share: true
---


### 使用CocoaPods来做iOS程序的包依赖管理

### 安装
{% highlight obj-c %}
$ sudo gem install cocoapods
$ pod setup
{% endhighlight %}

pod setup是Cocoapods在将它的信息下载到 ~/.cocoapods目录下，cd到那个目录，用du -sh *来查看下载进度。

### gems相关
{% highlight sh %}
sudo gem update --system
gem sources --remove https://rubygems.org/
gem sources -a http://ruby.taobao.org/
gem sources -l
{% endhighlight %}

### Podfile

格式

{% highlight obj-c %}
platform :ios
pod 'JSONKit',       '~> 1.4'
pod 'Reachability',  '~> 3.0.0'
pod 'ASIHTTPRequest'
pod 'RegexKitLite'
{% endhighlight %}

### 使用
将编辑好的Podfile文件放到你的项目根目录中，执行如下命令即可：

{% highlight sh %}
pod install
{% endhighlight %}


#### pod search
