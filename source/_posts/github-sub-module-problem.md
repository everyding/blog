---
title: github中子模块问题
date: 2016-04-12 13:47:47
tags: git 子模块
---

## 序

在我们开发项目的时候，可能需要加载第三方资源，那么这个时候就需要添加子模块，诸如我们的hexo博客，我们可能需要引用不同的主题，那么怎么添加子模块呢？

## 添加子模块

我们就拿本博客引用[jane](https://github.com/Alex-fun/hexo-theme-jane/)这个主题，其实这个主题就是一个第三方模块，我们应该怎么配置呢？我们打开这个页面它提示这样配置子模块：

```cmd
git submodule add https://github.com/Alex-fun/hexo-theme-jane.git themes/jane
```

<!--more-->

我们发现执行这条命令没有改变，后来Google发现，理论上它会生成一个.gitmodules文件，但是我发现并没有生成该文件，于是我自行创建了.gitmodules文件，并且配置如下内容：

```text
[submodule "jane"]
    path = themes/jane
    url = https://github.com/Alex-fun/hexo-theme-jane.git
```

当我们手动创建并且添加该配置信息后，我们用SourceTree能够正常拉取到这个仓库，否则会报拉取失败

![SourceTree](1.png)

## 总结

不知道是我这个版本的Git Shell配置有问题，最终通过手动方式解决了该问题。

![往运行服务器上直接上传文件时程序员的样子](2.gif)




