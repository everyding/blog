---
title: 前端学习资源整理
date: 2016-04-09 11:24:05
tags: 前端开发
---

![最近比较火的几本书](rm.jpg)

## 常用查询手册
> * [Can I use](http://caniuse.com/)
> * [DevDocs](http://devdocs.io/)
> * [DevTools](https://developers.google.com/chrome-developer-tools/?hl=zh-CN)
> * [导航](http://whycss.com/)
> * [OverAPI](http://overapi.com/)
> * [html5ify.com/fks/fks_chart/](http://html5ify.com/fks/fks_chart/)

<!--more-->

某日，某大公司要做一个网站，一群专家、老鸟、菜鸟、前端、后台、全栈们汇集一堂讨论技术框架。

后台框架的选型讨论略显沉闷，“SpringMVC + MyBatis + Redis”，几个后台老鸟互相给了个眼色，白纸黑字写了下来。本想有所作为的全栈们似乎想要说些什么，奈何自己势单力薄，欲言又止。

前端框架的选型开始了。几个全栈前端撸了撸袖子，意欲大干一场。

“用ng吧，google的产品，质量有保证！”老A抛出了一个烫手的山芋。
“ng是什么？”前端菜鸟小B小声问旁边的师父C。
“就是Angular.js，老A就不会说人话。”老C跟小B说。
“笑话！ng用哪个版本？1版问题太多快要被抛弃，2版刚从娘胎里出生走路都还不会呢，谁敢用？”作为全栈代表的老D毫不留情地回击老A。
“还是backbone好，结合marionette，代码写起来还是很爽的！”用惯了backbone的菜鸟小E勇敢地提出了自己的想法。
“backbone框架也太简单点了吧？要写好多代码，做好多重复性工作。”刚被浇了一盆冷水的老A重新挺直了腰板发表意见。
“支持国产，用一下vue.js？”
几个老鸟纷纷摇头，“没怎么用过不太熟悉啊！”
“react？”
“貌似学习曲线有点高啊！”
“Extjs吧，我用着还是蛮好用的。”众人纷纷投之以鄙夷的眼神。
“GWT呢？”众人哄堂大笑

“我建议这个框架选型问题我们先放一边，我们先来选择一下用什么来写？js？coffeeScript？es6？”一个后台老鸟看不下去了。
“当然是js啊！”
“别老土了，看过2016年的前端流行趋势没？以后是es6的天下，我们要有点远见不是？”
“coffeeScript我觉得也挺好啊，有点小清新的感觉~”
“要不我们试试TypeScript？”
“TypeScript的模块加载机制很怪啊。”
“用ES6 webpack就可以。”
“不习惯，前端还是用requirejs的好！”
“seajs多简洁啊，阿里出品，玉伯发起的，我还是他的粉丝呢~”

眼见还是争执不下，PM过来维护了一下秩序：“这样讨论下去也不是个事儿，我提议这样，让这次承担开发任务的X组组长会议之后做一次技术方案出来，然后大家有针对性的讨论。正好现在也到饭点了，大家要不先去吃饭去吧？”

众人作罢。

“backbone + jQuery2.1 + requirejs + grunt + mocha” X组组长提出了这一整套技术方案。
“为什么用jQuery2，不考虑兼容性吗？”
“jQuery太大了，用zepto代替吧”
“这个网站不是主要在移动端展示嘛，cash体积最小，很合适的！”
“grunt太笨重，gulp多简洁”
“jasmine测试也不错”
……


最后，由于项目经理对开发周期的要求，前端选型不得不告一段落，最终的网站只用到了jQuery等几个简单的js库。由于大家对jQuery都很熟悉，所以开发效率很高，再加上几个前端老鸟的性能调优，整个网站呈现效果颇让人满意。

本故事纯属事实，如有雷同，赏个赞呗！

**前端的开源和共享的本质造就了前端资源的空前繁荣，同样也会逼死选择困难症患者。同时，前端发展这么快，新框架后浪推前浪，想要对每个框架都了如指掌是很困难的。所谓前端熟手大多数情况下只能对自己熟悉的几个框架做出合理的评价。然而只是作为框架使用者是很难达到顶尖前端的程度。**

如果一定要说一个越早知道越好的小知识：

**在你确定需要框架之前，不要迷恋框架，不要过度设计。简单的往往是最好的。有了扎实的基础做根蒂，框架不过是浮华云烟。**


## JS高级前端开发
> * [SunLn 的前端收藏夹](https://github.com/SunLn/SunLn-F2E-Bookmarks)
> * [jsfront 的前端收藏夹](https://github.com/jsfront)
> * [Front--end--tutorial](https://github.com/MoonYaph/Front--end--tutorial)


## 前端常用工具
> * [CSS, JavaScript 压缩, 美化, 加密, 解密](http://tool.css-js.com/)
> * [Tiny在线图片压缩](https://tinypng.com/)
> * [CSS在线图片合并](http://spritegen.website-performance.org/)
> * [CssGaga](http://www.99css.com/cssgaga/)
> * [gtmetrix性能测试](https://gtmetrix.com/)
> * [pagespeed性能测试](https://developers.google.com/speed/pagespeed/insights/)

## 知乎
> * [知乎上前端开发领域有哪些值得推荐的问答？](http://www.zhihu.com/question/20246142)
> * [前端界有哪些越早知道越好的小技巧小知识？](https://www.zhihu.com/question/43687153)
> * [你见过哪些令你瞠目结舌的 JavaScript 奇技淫巧？](https://www.zhihu.com/question/37904806)
> * [你见过哪些令你瞠目结舌的 Java 奇技淫巧？](https://www.zhihu.com/question/37760140)
> * [你见过哪些令你瞠目结舌的 C/C++ 奇技淫巧？](https://www.zhihu.com/question/37692782)
> * [你见过哪些令你瞠目结舌的 Python 奇技淫巧？](https://www.zhihu.com/question/37904398)


