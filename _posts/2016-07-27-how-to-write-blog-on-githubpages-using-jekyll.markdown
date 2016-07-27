---
layout: post
title:  "怎么用jekyll在githubPages上写自己的Blog"
date:   2016-07-23 14:40:33 +0800
categories: other
tag: instruction
---
前言
======
我们肯定听过很多的大牛说过，一定要写自己的博客，总结自己的经验，拿出来分享，对自己的成长很重要。

我之前一直想写一个博客，但是没有找到一个好的平台，又不想在csdn这些简易的博客上写，但是搭建自己的博客网站又需要维护网站。
所以最后找到了[GitHubPages]，而它的内部又使用[jekyll]，所有用这样的方式建了一个博客。顺便分享一下怎么用[jekyll]在[GitHubPages]
上搭建博客的方法，减少各位探索的道路。


那么开始吧
======
> 下面的操作都是建立使用**windows64**系统的基础上

### 一、创建[GitHubPages]简单页面
1. 如果没有[GitHub]账号，请先创建账号。
2. 创建一个repository，命名为 **用户名.github.io**，必须这样命名。
3. 在repository下创建一个`index.html`写点内容,提交，然后就可以直接在浏览器中使用 **用户名.github.io** 访问了。

> 更专业详细的教程请参考[GitHubPages]


### 二、使用[jekyll]创建页面

#### *使用jekyll前的必要程序安装*
因为jekyll是由`ruby`实现的，使用jekyll前需要装上必要的程序。这个都是基于*jekyll3*基础上的，项目安装教程见[这里](https://jekyllrb.com/docs/installation/)

> Ruby的下载可能会很慢，可以使用中国的镜像，如[淘宝的](https://ruby.taobao.org/)

* 下载Ruby,[windows64位 Ruby2.3.1版下载](http://dl.bintray.com/oneclick/rubyinstaller/rubyinstaller-2.3.1.exe)，或者选择其他版本[rubyinstaller](http://rubyinstaller.org/downloads/)下载,
你也可以根据你的系统在[这里](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller)选择适合的。现在完成后安装，就可以使用`ruby`命令。

* 安装[RubyGems](https://rubygems.org/pages/download)，因为ruby2.3 版本都已经自带了gem了，但是我们还是需要更新gem到2.6版本才好，查看版本`gem -v`，不然可能会有些问题。
升级直接敲命令就可以了`gem update`，如果提示无法更新就输入`gem install rubygems-update`然后`update_rubygems `。

* 安装[NodeJS](https://nodejs.org/en/)

所有安装都完成后使用 `gem install jekyll` 安装jekyll，下载特别慢的话使用可以使用`gem sources --add https://ruby.taobao.org/ --remove https://rubygems.org/`
来指定下载源之所以要remove掉之前的sources是为了保证只有一个sources同时存在最好，使用`gem sources`查看正在使用的sources。

#### *所有安装都完成*




[GitHubPages]: https://pages.github.com/
[jekyll]: https://jekyllrb.com/
[GitHub]: https://github.com/
[RubyDownload]: https://www.ruby-lang.org/en/downloads/


