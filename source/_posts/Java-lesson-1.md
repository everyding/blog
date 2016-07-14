---
title: 第一讲，Java 基础
date: 2016-07-13 22:20:04
tags: Java
---

## Java语言发展史

[詹姆斯·高斯林（James Gosling）](http://baike.baidu.com/link?url=Z42ipSYLdzC8CE0O-fS7wfQtftO3hipMn49Z9Zd-AHYyVofjissxlgtf75NUHUHFizS_oKBj3JHK6uO0hd3zjK)1977年获得了加拿大卡尔加里大学计算机科学学士学位，1983年获得了美国卡内基梅隆大学计算机科学博士学位，毕业后到IBM工作，设计IBM第一代工作站NeWS系统，但不受重视。后来转至Sun（**S**tanford **U**niversity **N**etwork——斯坦福大学校园网）公司，1990年，与Patrick，Naughton和Mike Sheridan等人合作“绿色计划”，后来发展一套语言叫做“Oak”，后改名为Java。

<!--more-->

![詹姆斯·高斯林](james_gosling.png)

## Java语言发展史

Java Development Kit

> 1.0.2
> 1.1.1 -> 1.1.6 -> 1.1.7 -> 1.1.8
> 1.2.1

Java 2 SDK

> 1.2.2
> 1.3.0 -> 1.3.1
> 1.4.0 -> 1.4.1 -> 1.4.2 -> 1.5.0(5.0) -> 1.6.0(6.0) -> 1.7.0(7.0)
> jdk8

## Java语言平台版本

**J2SE（Java 2 Platform Standard Edition）标准版**
> 是为开发普通桌面和商务应用程序提供的解决方案
> 该技术体系是其他两者的基础，可以完成一些桌面应用程序的开发

**J2ME（Java 2 Platform Micro Edition）小型版**
> 是为开发电子消费产品和嵌入式设备提供的解决方案

**J2EE（Java 2 Platform Enterprise Edition）企业版**
> 是为开发企业环境下的应用程序提供的一套解决方案
> 该技术体系中包含的技术如 Servlet、Jsp等，主要针对于Web应用程序开发

## Java语言特点

简单性、解释性、面向对象、高性能、分布式处理、多线程、健壮性、动态、结构中立、安全性、开源、**跨平台**

**跨平台**

`什么是跨平台性？`通过Java语言编写的应用程序在不同的系统平台上都可以运行。`原理是什么？`只要在需要运行java应用程序的操作系统上，先安一个Java虚拟机(JVM Java Virtual Machine)即可。由JVM来负责Java程序在该系统中的运行。

![Java跨平台原理](allplatform.png)

**JDK与JRE**

`JDK`（**J**ava **D**evelopment **K**it）——Java开发工具包
> `JDK`是提供给Java开发人员使用的，其中包含了Java的开发工具，也包括了`JRE`。所以安装了`JDK`，就不用在单独安装`JRE`了。其中的开发工具：编译工具(javac.exe)  打包工具(jar.exe)等

`JRE`（**J**ava **R**untime **E**nvironment）——Java运行环境
> 包括Java虚拟机(JVM **J**ava **V**irtual **M**achine)和Java程序所需的核心类库等，如果想要运行一个开发好的Java程序，计算机中只需要安装`JRE`即可。

`简单而言：使用JDK开发完成的Java程序，交给JRE去运行。`

![JDK与JRE的关系](jdk_jre.png)

