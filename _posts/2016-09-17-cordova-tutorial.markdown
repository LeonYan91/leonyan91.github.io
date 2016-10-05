---
layout: post
title:  "cordova教学"
date:   2016-09-17 17:49:00 +0800
categories: Frontend Mobile
tag: Mobile
---


# CORDOVA
---
### 什么是Cordova
Cordova是开源手机开发框架，它允许你使用web开发的技术（html,js,css），实现跨平台开发。Cordova是包在目标平台的Webview中的，可利用调用目标平台的（利用插件）api，来实现更复杂的功能。

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
* 对应平台的SDK，[查看文档](https://cordova.apache.org/docs/en/latest/guide/cli/index.html#install-pre-requisites-for-building)

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

### Cordova目录结构

```
myapp/
|-- config.xml
|-- hooks/
|-- merges/
| | |-- android/
| | |-- windows/
| | |-- ios/
|-- www/
|-- platforms/
| |-- android/
| |-- windows/
| |-- ios/
|-- plugins/
  |--cordova-plugin-camera/
```

##### config.xml
你的Cordova项目描述文件，配置整个项目的行为。

##### www/
放置Cordova项目web资源的地方（html,js,css...），Cordova项目的开发基本都是在此目录下开展的。`www/`目录的资源会在build项目的时候，拷贝到各自`platform/`平台下，如`platforms/ios/www`或`platforms/android/assets/www`。因为cli总会从源目录www下拷贝资源，所以我们应该只编辑`www/`目录，而不要去动`platforms/`下面的www文件。

##### platforms/
包含所有添加到此Cordova项目的平台，平台的源代码，脚本文件等。
> 不要去编辑此目录下文件，除非你知道你在干什么。此目录文件在cli build项目经常重写。

##### plugins/
添加的插件

##### hooks/
自定义的脚本行为，当你想要自定义cordova-cli 命令时。所有你添加到目录下的脚本，如果你执行的命令名和目录名相匹配，那么会在命令执行之前或后执行。如有`before_build`,`before_build`，对于的脚本会在执行`build`命令时执行。查看[Hooks文档](http://cordova.apache.org/docs/en/latest/guide/appdev/hooks/index.html)。

##### merges/
平台指定的资源(js,html,css...)，存放在此目录对应平台目录下，在`build`项目时，对应平台会采用merges下的资源覆盖www的资源。
举个简单的例子，假设我们项目有次目录结构：
```
merges/
|-- ios/
| -- app.js
|-- android/
| -- android.js
www/
-- app.js
```
在build项目后，android平台会有`app.js`,`android.js`，ios平台只会有`app.js`，但是这会是`marges/ios/`下的，而不是`www/`下的。


目录结构讲解官方文档 [documentation](https://cordova.apache.org/docs/en/latest/reference/cordova-cli/index.html#directory-structure)

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

###### plugin描述文件
先来看个简单的plugin.xml文件
```xml
<?xml version="1.0" encoding="UTF-8"?>
<plugin xmlns="http://apache.org/cordova/ns/plugins/1.0"
        id="cordova-plugin-echo" version="0.0.1">
    <name>echo</name>
    <description>Echo Plugin</description>
    <license>Apache 2.0</license>
    <keywords>cordova,echo</keywords>
    <js-module src="www/echo.js" name="echo">
        <clobbers target="echo" />
    </js-module>
    <platform name="android">
        <config-file target="config.xml" parent="/*">
            <feature name="Echo">
                <param name="android-package" value="org.apache.cordova.plugin.Echo"/>
            </feature>
        </config-file>

        <source-file src="src/android/Echo.java" target-dir="src/org/apache/cordova/plugin" />
    </platform>
</plugin>
```
描述文件中包含了`name`,`id`,`version`等描述插件身份的。而标签`<js-module>`和`<platform>`才是插件关键的地方。

TODO android plugin java代码讲解






