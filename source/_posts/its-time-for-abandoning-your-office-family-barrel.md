title: 是时候抛弃你的OFFICE全家桶了
author: 唐先森
avatar: /images/favicon.png
authorLink: 'https://www.tangkunyin.com'
authorAbout: 'https://about.tangkunyin.com'
authorDesc: 一个写代码的「伪文人」
categories: 资源
date: 2017-09-06 18:00:52
tags:
	- 黑科技
	- js大法
keywords: nodeppt,ppt
description: 今天来说一个三年前的项目，于我而言算是是黑科技，给小伙伴们分享下使用心得。同时友情提示你，是时候抛弃office全家桶套餐了，这个更有营养。
photos:
	- /img/2017/blackTech.png
---

![blackTech](/img/2017/blackTech.png)

### 今天要说的是一个很炫的东西，叫做**NodePPT**

你是否有这种场景，辛苦做好一份`PPT`，然后发文件给其他人，奈何人家用的`macOS`且没有装微软全家桶，如果有`Keynote`还算好。想表达的意思就是通过这样的`Native`端办公软件，在跨平台协作上，难免会「丢真」。而今天的主角，将以极客化的方式为你继续`PPT`之路，让你越来越喜欢装逼......

#### 项目地址

> let's look look...  [demo](http://js8.in/nodeppt/)

源码：[nodeppt](https://github.com/ksky521/nodeppt)

#### 安装使用啥的，官方文档说的很清楚，以下为我使用笔记

1. 升级版本：

> npm update -g nodeppt

2. 创建一个文档：

```
// a. 执行如下命令
nodeppt create hello

// b. 交互式信息补充
please input：
title (slide title) Hello
subtitle world
speaker (speaker) Thomas Tang
Success：hello.md, please write your slide content

// c. 使用MWeb之类的MD工具开始愉快的编写ppt吧~
```



