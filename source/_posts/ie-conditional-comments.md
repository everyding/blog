---
title: IE浏览器的条件注释(Conditional Comments)
date: 2016-05-31 11:47:55
tags: 条件注释
---

条件注释：顾名思义就是如果条件成立，就解析，否则就忽略。但这仅仅在IE浏览器中起作用，那么我们就利用这一特点察言观色，做到“见什么浏览器说什么话”。

## 语法

```
这是标准的注释格式：
<!-- 注释内容  -->

这是条件注释的第一种（推荐）写法：
<!--[if expression]> 注释内容 <![endif]-->

这是条件注释的第二种写法：
<![if expression]> 注释内容 <![endif]>
```

<!--more-->

那么第一种写法和第二种写法有什么区别呢？区别就在于低版本IE（Microsoft Internet Explorer 5 以下版本，不含IE5，因为这些版本不支持条件注释）对待这两种写法的方式。对于第一种写法，低版本IE会视作注释内容而忽略解析，而对于第二种写法，低版本IE则会忽略条件表达式，也就是说条件注释总是被认为条件为真。因此，若要顾及低版本IE感受的话，还是请使用第一种写法为妙。

下边列举一下条件注释的几种常见用法：

```
<!--[if IE]><p>IE浏览器</p><![endif]-->
<!--[if !IE]><p>非IE浏览器</p><![endif]-->
 
<!--[if IE 7]><p>Internet Explorer 7</p><![endif]-->
<!--[if IE 8]><p>Internet Explorer 8</p><![endif]-->
<!--[if !(IE 7)]><p>非Internet Explorer 7</p><![endif]-->
 
<!--[if gte IE 7]><p>IE 7 或者更高版本.</p><![endif]-->
<!--[if (IE 5)]><p>IE 5 (any version).</p><![endif]-->
<!--[if (gte IE 5.5)&(lt IE 7)]><p>IE 5.5 或者 IE 6.</p><![endif]-->
<!--[if lt IE 5.5]><p>低于IE5.5</p><![endif]-->
 
<!--[if true]>您目前使用的浏览器支持条件注释<![endif]-->
<!--[if false]>您目前使用的浏览器不支持条件注释<![endif]-->
```

下面是条件注释表达式中关键词的说明：

```
& 与
| 或
! 非
lt 小于
lte 小于或者等于
gt 大于
gte 大于或者等于
() 子表达式
```

参考资料：https://msdn.microsoft.com/en-us/library/ms537512\(VS.85\).aspx