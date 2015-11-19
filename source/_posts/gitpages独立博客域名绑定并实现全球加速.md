title: gitpages独立博客域名绑定并实现全球加速
date: 2015-11-06 11:16:52
timestamp: 1446779812
catAlias: site
categories: 建站
tags: 建站
keywords: 建站，域名绑定
description: 申请了二级域名，怎么绑定我的gitcafe/github pages博客？表急，本文将告诉你git pages服务下的独立博客域名绑定并实现全球加速。
---

> 尽管这个话题百度谷歌都可以找到一大把答案。但为了照顾来自本站朋友的困惑，我还是再写一遍。贴个图给各位说明下。

![gitcafe域名绑定配置](http://i13.tietuku.com/b32a396930ac6eec.png)

![dnspod域名解析配置](http://i13.tietuku.com/ca4ec744e698648b.png)

#### 至于`github`上，你需要建立一个`CNAME`文件，名字就叫`CNAME`，没有后缀。然后把它放到根目录下即可。

### 第二张图，展示了我实现`全球加速`方法的配置。即：大陆以内指向`gitcafe`，大陆以外指向`github`。:)
