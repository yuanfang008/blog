title: WebViewJavascriptBridge实战与原理探究
date: 2015-11-18 16:25:11
categories: iOS
tags: iOS, WebViewJavascriptBridge
keywords: OS, WebViewJavascriptBridge
description: 本文将讲诉WebViewJavascriptBridge实战与原理探究。告诉你iOS的webview中，JS与OC的相互调用。并试着探究该框架原理。
---
#### 原生应用中总有那么一些需求是要跨平台的，这个时候响应式网页就派上用场了。那么问题来了，网页中如果想调用原生的东西，该怎么做呢？

#### 水果OS7以后，开放`JavaScriptCore`库，供开发人员进行JS与OC混编交互。但是对于WebView中直接使用这货，还是有点不方便。自己再封装也很麻烦。不过不要捉急，`WebViewJavascriptBridge`将带给你完美的解决方案。

![WebViewJavascriptBridge-OC-Coding](http://i5.tietuku.com/1ffc6b019c986226.png)
![WebViewJavascriptBridge-JS-Coding](http://i5.tietuku.com/a1582b160d0e4147.png)

#### 以上分别展示了OC与JS中使用`WebViewJavascriptBridge`的方法。但请注意：`网页中其实不需要再引入其他的JS库`
	
	PS：鄙人之前协助前端开发这块时，就把他带错路 :)
	
#### 下边来扒拉一下该框架源码，研究下其大概的原理，看看为什么网页不需要引入另外的JS库就可以调用JS方法

![WebViewJavascriptBridge-OBJC-SRC](http://i5.tietuku.com/c47a7f0a662280dc.png)

#### 你看到了，OC的源码中其实已经引入这个JS库了，所以网页中不需要再引入。而该框架本身，我猜也是基于`JavaScriptCore `封装实现的。