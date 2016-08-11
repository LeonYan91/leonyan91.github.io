---
layout: post
title:  "java-动态代理"
date:   2016-08-04 17:00:00 +0800
categories: Java
tag: JavaCore
---

什么是动态代理
======

动态代理(dynamic proxy)是Java提供的一种用于在运行时环境(Runtime)，动态创建代理对象的机制，他和使用一般的代理模式最大的不同是他是动态创建的。
引用Head first design pattern P486 

> The proxy is dynamic
  because its class is created at runtime.
  Think about it: before your code runs
  there is no proxy class; it is created on
  demand from the set of interfaces you
  pass it.
  
之所以动态代理动态，是因为他根据你提供的需要代理的接口，动态创建的，而不是在编码时定义的，这样提供了很强大的灵活性。




