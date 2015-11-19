title: 一条命令延长Reveal试用期
date: 2015-10-28 22:01:31
timestamp: 1446040891
catAlias: tools
categories: 工具
tags: Reveal,工具
keywords: Reveal,工具
description: Reveal试用期过了怎么办？今天来教你一招：一条命令延长Reveal试用期。
---
​
> 写在前面：当然最简单的办法就是修改本机时间。你要是受得了，那就改吧。今天分享另一种延长方法：

### 1、进入系统偏好设置：

  /Users/shuoit/Library/Preferences

### 2、找到Reaveal的配置文件，并删除：
  ➜  Preferences  ls com.ittybittyapps.Reveal.plist<br/>
  com.ittybittyapps.Reveal.plist<br/>
  ➜  Preferences  open .<br/>
  ➜  Preferences  rm com.ittybittyapps.Reveal.plist

### 3、重新打开试试，是不是又延长了30天
