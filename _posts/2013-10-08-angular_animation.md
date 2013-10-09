---
layout: post
title: AngularJs动画(1.2)
description: "学习AngularJs 1.2版本中的动画特性"
date: 2013-10-08
modified: 2013-10-08
category: web
tags: [angular]
image:
  feature: texture-feature-02.jpg
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

参考[animation in angularjs 1.2](http://www.yearofmoo.com/2013/08/remastered-animation-in-angularjs-1-2.html)

### 介绍

1.引用的ngAnimate模块

{% highlight html %}
<script src="angular-animate.min.js"></script>
<script>
    angular.module('yo', [
        'ngAnimate'
    ]);
</script>
{% endhighlight%}

2.ngAnimate提供的指令

	ngRepeate + CSS3 Transition
	ngView + CSS3 Keyframes
	ngClass + Animate.css

3.自定义指令

	$animate 

### 创建动画

#### CSS Transitions

|事件/动作|开始 CSS类|结束 CSS类|触发指令|
|:---:|:---:|:------:|:------------:|
|enter|.ng-enter|.ng-enter-active|ngRepeat, ngInclude, ngIf, ngView |
|leave|.ng-leave|.ng-leave-active|ngRepeat, ngInclude, ngIf, ngView |
|move|.ng-move|.ng-move-active|ngRepeat|
|:---:|:---:|:------:|:------------:|
|隐藏元素|.ng-hide-add|.ng-hide-add-active|ngShow, ngHide|
|显示元素|.ng-hide-remove|.ng-hide-remove-active|ngShow, ngHide|
|增加class|.CLASS-add|.CLASS-add-active|ngClass and class=""|
|删除class|.CLASS-remove|.CLASS-remove-active|ngClass and class=""|
|:---:|:---:|:------:|:------------:|
{: rules="groups"}

{% highlight css %}
.my-special-animation.ng-enter {
  -webkit-transition:0.5s linear all;
  -moz-transition:0.5s linear all;
  -o-transition:0.5s linear all;
  transition:0.5s linear all;

  background:red;
}

/* destination animations */
.my-special-animation.ng-enter.ng-enter-active {
  background:blue;
}
{% endhighlight%}

#### CSS Keyframes Animation

	CSS动画完全由'@keyframe'管理, 不需要定义-active类

{% highlight css %}
/* starting animations */
.my-special-animation.ng-enter {
  -webkit-animation:0.5s red-to-blue;
  -moz-animation:0.5s red-to-blue;
  -o-animation:0.5s red-to-blue;
  animation:0.5s red-to-blue;
}

@keyframes red-to-blue {
  from { background:red; }
  to { background:blue; }
}

@-webkit-keyframes red-to-blue {
  from { background:red; }
  to { background:blue; }
}

@-moz-keyframes red-to-blue {
  from { background:red; }
  to { background:blue; }
}

@-o-keyframes red-to-blue {
  from { background:red; }
  to { background:blue; }
}
{% endhighlight%}

####	JavaScript Animation

{% highlight javascript %}
myApp.animation('.my-special-animation', function() {
  return {
    enter : function(element, done) {
      jQuery(element).css({
        color:'#FF0000'
      });
      jQuery(element).animate({
        color:'#0000FF'
      }, done);

      return function(cancelled) {
        /* this (optional) function is called when the animation is complete
           or when the animation has been cancelled (which is when
           another animation is started on the same element while the
           current animation is still in progress). */
        if(cancelled) {
          jQuery(element).stop();
        }
      }
    },

    leave : function(element, done) { done(); },
    move : function(element, done) { done(); },
    addClass : function(element, className, done) { done(); },
    removeClass : function(element, className, done) { done(); }
  };
});
{% endhighlight%}

### 指令

1.ngRepeat

	插入, 删除, 移动列表元素触发enter leave move事件

2.ngInclude, ngView, ngIf

	插入, 删除容器元素触发enter leave事件

3.ngSwitch

4.ngClass

	新的class触发add, 旧的class触发remove
	CSS中使用新的 .CLASS-add .CSS-remove

5.ngShow, ngHide

	元素隐藏ng-hide-add 元素显示ng-hide-remove

#### 自定义指令

在自定义指令中中注入 $animate服务, 然后触发适当的事件函数

|事件|函数声明|描述|
|:---:|:---:|:------:|
|enter|$animate.enter(element, parent, after, callback)|添加元素|
|leave|$animate.leave(element, callback)|从DOM中删除元素|
|move|$animate.move(element, parent, after, callback)|移动|
|addClass|$animate.addClass(element, className, callback)||
|removeClass|$animate.removeClass(element, className, callback)||
|:---:|:---:|:------:|:------------:|
{: rules="groups"}

### 测试

### 第三方CSS/JS库

[Animate.css](https://github.com/yearofmoo/ngAnimate-animate.css)
[Effeckt.css](http://h5bp.github.io/Effeckt.css/dist/)