---
layout: post
title:  "使用css,在文字第二行开始截取字段"
date:   2016-11-03 10:23:00 +0800
categories: css issue
tag: develop_issue text_issue
---


# 使用css,在文字第二行开始截取字段
---

##概述
css支持文字多长使用`text-overflow:break-word`来截取过长字符，而我的需求是过长后，换行，从第二行尾部过长的部位才开始截取。

##方案
css目前不支持这样的功能，貌似css3有`text-lines:2`这个属性？但是我没有找到。

stackOverflow上面有很多的解决方案，我找到的一个最好的解决方案([stackOverflow上的帖子]())，是使用webkit的属性，所有有些浏览器无法使用，
不过针对我这个项目OK，因为我们ionic使用了浏览器插件，在不同的设备上面浏览器不会有差异。

[原贴地址](http://stackoverflow.com/questions/5269713/css-ellipsis-on-second-line)
`css
    overflow: hidden;
    text-overflow: ellipsis;
    -webkit-line-clamp: 2;
    display: -webkit-box;
    -webkit-box-orient: vertical;
`

其他有用的帖子
 * [http://stackoverflow.com/questions/15909489/text-overflow-ellipsis-on-two-lines]
 * [http://codepen.io/martinwolf/pen/qlFdp]
