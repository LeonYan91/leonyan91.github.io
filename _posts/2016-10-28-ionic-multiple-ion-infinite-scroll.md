---
layout: post
title:  "ionic1.3.1 multiple ion-infinite-scroll on same page"
date:   2016-10-28 10:23:00 +0800
categories: ionic issue
tag: develop_issue
---


# ionic1.3.1 多个ion-infinite-scroll在同一个页面
---

## 概述
需要实现在相同页面上放上多个ion-infinite-scroll.

## 方案
根据[文档](http://ionicframework.com/docs/api/directive/ionInfiniteScroll/),ion-infinite-scroll必须是`Child of ionContent or ionScroll`，
所以必须包在`ion-content`,或者`ion-scroll`下面，实际上，放在`ion-scroll`下面是存在问题的。

一个页面是可以存在多个`ion-content`，将`ion-infinite-scroll`放在content下面，[国外的一个实现](http://codepen.io/priand/pen/PzYbZG)
