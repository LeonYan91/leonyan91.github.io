---
layout: post
title:  "cordova教学"
date:   2016-09-17 17:49:00 +0800
categories: Frontend Mobile
tag: JavaCore
---


# Cordova
---
### 什么是Cordova
Cordova是开源手机开发框架，它允许你使用web开发的技术（html,js,css），开发跨平台的App。Cordova应该是包在目标平台的webview中的，可利用调用目标平台的（利用插件）api，来使用更复杂的功能。

### 优势和缺点
Cordova的优点有：
1. 使Web开发人员可以快速转移到移动端开发。
2. 平台无关性，因为是使用web技术，我们使用一套代码就可以在多个平台上开发App，当然必要的时候需要一定的修改。
3. 更快速的开发，有很多插件的存在，模板的存在，我们可以快速的完成App的开发，投放到市场。

Cordova的缺点有：
1. 流畅性没有原生的好，特别是在性能不好的机器上。
2. 底层的功能需要依赖插件。

### 使用Cordova
Cordova是依托在npm，使用简单命令就可以完成项目的创建，管理。

##### 使用cordova前需要安装的程序
* [nodejs](https://nodejs.org) 安装完成后确保环境变量已配置进Path，可以使用npm命令。
* 对应平台的SDK，如android

##### 简单使用
1. `npm install -g cordova` 安装cordova cli,-g为全局安装，不然只会安装到当前目录下
2. `cordova create hello` 创建cordova项目
3. `cordova platform add android` 添加想要开发的平台，目标平台
3. `cordova run android` 运行cordova项目，如果没有连接手机，可以使用emulate模拟



### Cordova构成

##### Cordova app的架构
![cordova app architecture](http://e.hiphotos.baidu.com/image/pic/item/9f2f070828381f302de9f632a1014c086f06f0bd.jpg)

##### WebApp 
这里我们前端代码（js,html,css）和资源存放的位置，也就是app业务代码存放的地方。可以说是cordova app最重要的地方。这些代码执行在我们平台包装的webView中，就像是一个内置的浏览器。

##### Plugins
使用web技术开发的app功能很有限，无法调用到设备的很多功能，如摄像头，定位等。这时我们就需要一个可以在javascript中调用设备接口的方法。插件就是为了这个而存在的，通过插件，我们可以用javascript就调用到设备的功能。cordova官方有很多的核心插件，也有很多第三方的插件，当然也可以自己写。有了插件，可以说webapp和做到和原生app一样。所以插件是webapp中必不可少的一部分之一。

### 插件详解

##### 安装插件
切换到cordova项目根目录，使用命令`cordova plugin add pluginID[@version]|directory|url[#commit-ish][:subdir]` ,可以使用`cordova plugin`查看安装成功的plugin。

##### 使用plugin
以cordova的camera摄像头plugin为例讲一个plugin的用法。使用`cordova plugin add cordova-plugin-camera`安装成功后，在javascript中，就可使用`navigator.camera`对象来使用摄像头功能了。如拍照功能`navigator.camera.getPicture(cameraSuccess, cameraError, cameraOptions)`，我们可以用[API](https://cordova.apache.org/docs/en/latest/reference/cordova-plugin-camera/index.html)上查到我们想要的功能。

##### 如何创建plugin/plugin如何工作的
plugin由三部分组成。前端接口（javascript代码），plugin描述文件`plugin.xml`,以及不同平台的本地实现代码。以android平台为例简单讲解一个plugin的创建
###### 前端接口
在创建plugin前端接口的时候我们可以任意建立自己喜欢的结构和方式，但是必须调用`cordova.exec`来和本地代码通信，调用方式如下：
```javascript
cordova.exec(function(winParam) {},
             function(error) {},
             "service",
             "action",
             ["firstArgument", "secondArgument", 42, false]);
```
exec方法中的参数描述：
* `function(winParam){}`成功回调函数，执行此函数并且将传入本地代码调用传入的值.
* `function(error) {}`错误回调函数，错误时执行.
* `service` 本地代码中的服务名,如android中，为类的名字。
* `action` 本地代码service中的方法名.
* `[/* arguments */]` 传入到本地代码中的参数数组.

