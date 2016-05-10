---
title: 前端开发规范
date: 2016-05-09 20:54:09
tags: 规范
---

此规范主要实现的目标：**代码一致性**和**最佳实践**。通过代码风格的一致性，降低维护代码的成本以及改善多人协作的效率。同时遵守最佳实践，确保页面性能得到最佳优化和高效的代码。

# • 基本规范

## IDE

推荐 `WebStorm`、`PhpStorm`、`IDEA`，能够将所有的代码格式问题搞定，形成统一标准。

![WebStorm 界面](ws.png)

 <!--more-->

## 缩进

统一用 `Tab` 缩进

## 文件编码

**使用不带 `BOM` 的 UTF-8 编码**

• 在 HTML中指定编码 `<meta charset="utf-8">` ；
• 无需使用 `@charset` 指定样式表的编码，它默认为 `UTF-8` （参考 [@charset](https://developer.mozilla.org/en-US/docs/Web/CSS/@charset)）。

## 一律使用小写字母

```html
<!-- 推荐-->
<img src="google.png" alt="Google" />

<!-- 不推荐 -->
<A HREF="/">Home</A>
```

```css
/* 推荐 */
color: #e5e5e5;

/* 不推荐 */
color: #E5E5E5;
```

## 省略外链资源 URL 协议部分

省略外链资源（图片及其它媒体资源）URL 中的 http / https 协议，使 URL 成为相对地址，避免 [Mixed Content](https://developer.mozilla.org/en-US/docs/Security/MixedContent) 问题，减小文件字节数。

**其它协议（ftp 等）的 URL 不省略。**

```html
<!-- 推荐 -->
<script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>

<!-- 不推荐 -->
<script src="http://www.google.com/js/gweb/analytics/autotrack.js"></script>
```

```css
/* 推荐 */
.example {
  background: url(//www.google.com/images/example);
}

/* 不推荐 */
.example {
  background: url(http://www.google.com/images/example);
}
```

# • HTML规范

## 文档类型

为每个 HTML 页面的第一行添加标准模式（standard mode）的声明， 这样能够确保在每个浏览器中拥有一致的表现。

```html
<!DOCTYPE html>
```

## 语言属性

为什么使用 lang="zh-cmn-Hans" 而不是我们通常写的 lang="zh-CN" 呢? 请参考知乎上的讨论: [网页头部的声明应该是用 lang="zh" 还是 lang="zh-cn"？](https://www.zhihu.com/question/20797118)

```html
<!-- 中文 -->
<html lang="zh-Hans">

<!-- 简体中文 -->
<html lang="zh-cmn-Hans">

<!-- 繁体中文 -->
<html lang="zh-cmn-Hant">

<!-- English -->
<html lang="en">
```

## HEAD 模板

```html
<!DOCTYPE html>
<html lang="zh-cmn-Hans">
<head>
    <meta charset="utf-8">
    
    <!-- SEO -->
    <title>Style Guide</title>
    <meta name="description" content="不超过150个字符">
    <meta name="keywords" content="">
    <meta name="author" content="name, email@gmail.com">
    
    <!-- No Baidu Siteapp -->
    <meta http-equiv="Cache-Control" content="no-siteapp"/>
    
    <!-- Set render engine for 360 browser -->
    <meta name="renderer" content="webkit|ie-comp|ie-stand">
    
    <!-- 优先使用最新版本的IE 和 Chrome 内核 -->
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
    
    <!-- 为移动设备添加 viewport -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <!-- iOS 图标 -->
    <link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-57x57-precomposed.png">

    <link rel="alternate" type="application/rss+xml" title="RSS" href="/rss.xml" />
    <link rel="shortcut icon" href="path/to/favicon.ico">
</head>
```

## HTML 标签的使用应该遵循标签的语义

下面是常见标签语义

• p - 段落
• h1,h2,h3,h4,h5,h6 - 层级标题
• strong,em - 强调
• ins - 插入
• del - 删除
• abbr - 缩写
• code - 代码标识
• cite - 引述来源作品的标题
• q - 引用
• blockquote - 一段或长篇引用
• ul - 无序列表
• ol - 有序列表
• dl,dt,dd - 定义列表

```html
<!-- 不推荐 -->
<div>Esprima serves as an important <span class="strong">building block</span> for some JavaScript language tools.</div>

<!-- 推荐 -->
<p>Esprima serves as an important <strong>building block</strong> for some JavaScript language tools.</p>
```

## CSS 和 JavaScript 引入

**引入 `CSS` 时必须指明 `rel="stylesheet"`**

```html
<link rel="stylesheet" href="page.css">
```

**引入 `CSS` 和 `JavaScript` 时无须指明 `type` 属性**

解释：`text/css` 和 `text/javascript` 是 `type` 的默认值。

**在 `head` 中引入页面需要的所有 `CSS` 资源**

解释：在页面渲染的过程中，新的CSS可能导致元素的样式重新计算和绘制，页面闪烁。

**`JavaScript` 应当放在页面末尾，或采用异步加载**

解释：将 `script` 放在页面中间将阻断页面的渲染。出于性能方面的考虑，如非必要，请遵守此条建议。

```javascript
<body>
    <!-- a lot of elements -->
    <script src="init-behavior.js"></script>
</body>
```

## 尽量减少标签数量

```html
<!-- 不推荐 -->
<span class="avatar">
  <img src="...">
</span>

<!-- 推荐 -->
<img class="avatar" src="...">
```

## class 与 id

• class 应以功能或内容命名，不以表现形式命名；
• class 与 id 单词字母小写，多个单词组成时，采用中划线-分隔；
• 使用唯一的 id 作为 Javascript hook, 同时避免创建无样式信息的 class；

```html
<!-- 不推荐 -->
<div class="j-hook left contentWrapper"></div>

<!-- 推荐 -->
<div id="j-hook" class="sidebar content-wrapper"></div>
```

## 属性顺序
   
HTML 属性应该按照特定的顺序出现以保证易读性。
   
• id
• class
• name
• data-xxx
• src, for, type, href
• title, alt
• aria-xxx, role

```html
<a id="..." class="..." data-modal="toggle" href="###"></a>

<input class="form-control" type="text">

<img src="..." alt="...">
```

## 引号

属性的定义，统一使用双引号。

```html
<!-- 不推荐 -->
<span id='j-hook' class=text>Google</span>

<!-- 推荐 -->
<span id="j-hook" class="text">Google</span>
```

## 嵌套

`a 不允许嵌套 div` 这种约束属于语义嵌套约束，与之区别的约束还有严格嵌套约束，比如 `a 不允许嵌套 a`。

严格嵌套约束在所有的浏览器下都不被允许；而语义嵌套约束，浏览器大多会容错处理，生成的文档树可能相互不太一样。

**语义嵌套约束**

`<li>` 用于 `<ul>` 或 `<ol>` 下；
`<dd>`, `<dt>` 用于 `<dl>` 下；
`<thead>`, `<tbody>`, `<tfoot>`, `<tr>`, `<td>` 用于 `<table>` 下；

**严格嵌套约束**

inline-Level 元素，仅可以包含文本或其它 inline-Level 元素;
`<a>`里不可以嵌套交互式元素`<a>`、`<button>`、`<select>`等;
`<p>`里不可以嵌套块级元素`<div>`、`<h1>~<h6>`、`<p>`、`<ul>/<ol>/<li>`、`<dl>/<dt>/<dd>`、`<form>`等。
更多详情，参考[WEB标准系列-HTML元素嵌套](http://www.smallni.com/element-nesting/)

## 布尔值属性

HTML5 规范中 `disabled`、`checked`、`selected` 等属性不用设置值。

```html
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
  <option value="1" selected>1</option>
</select>
```

## 图片

**禁止 `img` 的 `src` 取值为空。延迟加载的图片也要增加默认的 `src`**

`src` 取值为空，会导致部分浏览器重新加载一次当前页面，参考：[https://developer.yahoo.com/performance/rules.html#emptysrc](https://developer.yahoo.com/performance/rules.html#emptysrc)

**避免为 `img` 添加不必要的 `title` 属性**

解释：多余的 `title` 影响看图体验，并且增加了页面尺寸。

**为重要图片添加 `alt` 属性**

解释：可以提高图片加载失败时的用户体验。

**添加 `width` 和 `height` 属性，以避免页面抖动**

# • CSS规范

## 属性定义后必须以分号结尾

```css
/* 不推荐 */
.selector {
    margin: 0
}

/* 推荐 */
.selector {
    margin: 0;
}
```

## 属性声明顺序

相关的属性声明应当归为一组，并按照下面的顺序排列：

• **Formatting Model** 相关属性包括：`position` / `top` / `right` / `bottom` / `left` / `float` / `display` / `overflow` 等
• **Box Model** 相关属性包括：`border` / `margin` / `padding` / `width` / `height` 等
• **Typographic** 相关属性包括：`font` / `line-height` / `text-align` / `word-wrap` 等
• **Visua**l 相关属性包括：`background` / `color` / `transition` / `list-style` 等

```css
.sidebar {
    /* formatting model: positioning schemes / offsets / z-indexes / display / ...  */
    position: absolute;
    top: 50px;
    left: 0;
    overflow-x: hidden;

    /* box model: sizes / margins / paddings / borders / ...  */
    width: 200px;
    padding: 5px;
    border: 1px solid #ddd;

    /* typographic: font / aligns / text styles / ... */
    font-size: 14px;
    line-height: 20px;

    /* visual: colors / shadows / gradients / ... */
    background: #f5f5f5;
    color: #333;
    -webkit-transition: color 1s;
       -moz-transition: color 1s;
            transition: color 1s;
}
```

## 清除浮动

当元素需要撑起高度以包含内部的浮动元素时，通过对伪类设置 clear 或触发 BFC 的方式进行 clearfix。尽量不使用增加空标签的方式。如果需要更小副作用清除浮动参看 [A new micro clearfix hack](http://nicolasgallagher.com/micro-clearfix-hack/) 一文。


```css
.cf:before,
.cf:after {
    content: " "; 
    display: table; 
}

.cf:after {
    clear: both;
}

.cf {
    *zoom: 1;
}
```

## 值与单位

**文本内容必须用双引号包围**

```css
/* 不推荐 */
html[lang|=zh] q:before {
    font-family: 'Microsoft YaHei', sans-serif;
    content: '“';
}

html[lang|=zh] q:after {
    font-family: 'Microsoft YaHei', sans-serif;
    content: '”';
}

/* 推荐 */
html[lang|="zh"] q:before {
    font-family: "Microsoft YaHei", sans-serif;
    content: "“";
}

html[lang|="zh"] q:after {
    font-family: "Microsoft YaHei", sans-serif;
    content: "”";
}
```

**当数值为 0 - 1 之间的小数时，省略整数部分的 `0`**

```css
/* 不推荐 */
panel {
    opacity: 0.8;
}

/* 推荐 */
panel {
    opacity: .8;
}
```

**`url()` 函数中的路径不加引号**

```css
body {
    background: url(bg.png);
}
```

**`url()` 函数中的绝对路径可省去协议名。**

```css
body {
    background: url(//baidu.com/img/bg.png) no-repeat 0 0;
}
```

**长度为 `0` 时须省略单位**

```css
/* 不推荐 */
body {
    padding: 0px 5px;
}

/* 推荐 */
body {
    padding: 0 5px;
}
```

## 颜色

**RGB颜色值必须使用十六进制记号形式 `#rrggbb`，不允许使用 `rgb()`**

带有alpha的颜色信息可以使用 `rgba()`

```css
/* 不推荐 */
.success {
    box-shadow: 0 0 2px rgba(0,128,0,.3);
    border-color: rgb(0, 128, 0);
}

/* 推荐 */
.success {
    box-shadow: 0 0 2px rgba(0, 128, 0, .3);
    border-color: #008000;
}
```

**颜色值是英文字符采用小写，若可以缩写时，必须使用缩写形式**

```css
/* 不推荐 */
.success {
    background-color: #AACCAA;
    color: #EEEEEE;
}

/* 推荐 */
.success {
    background-color: #aca;
    color: #eee;
}
```

**颜色值不允许使用命名色值**

```css
/* 不推荐 */
.success {
    color: lightgreen;
}

/* 推荐 */
.success {
    color: #90ee90;
}
```

## 文本编排

**`font-weight` 属性必须使用数值方式描述**

CSS 的字重分 100 – 900 共九档，但目前受字体本身质量和浏览器的限制，实际上支持 `400` 和 `700` 两档，分别等价于关键词 `normal` 和 `bold`。

```css
/* 不推荐 */
h1 {
    font-weight: bold;
}

/* 推荐 */
h1 {
    font-weight: 700;
}
```

## 兼容性

**带私有前缀的属性由长到短排列，按冒号位置对齐**

标准属性放在最后，按冒号对齐方便阅读，也便于在编辑器内进行多行编辑。

```css
.box {
    -webkit-box-sizing: border-box;
       -moz-box-sizing: border-box;
            box-sizing: border-box;
}
```


# • JavaScript规范

## • 命名

**变量**, 使用 Camel 命名法。

```javascript
var loadingModules = {};
```

**私有属性、变量和方法**以下划线 _ 开头。

```javascript
var _t = this;
```

**常量**, 使用全部字母大写，单词间下划线分隔的命名方式。

```javascript
var HTML_ENTITY = {};
```

**函数**, 函数的**参数**,使用 Camel 命名法。

```javascript
function stringFormat(source) {}

function hear(theBells) {}
```

**类**, 使用 Pascal 命名法，类的 **方法 / 属性**, 使用 Camel 命名法

```javascript
function TextNode(value, engine) {
    this.value = value;
    this.engine = engine;
}

TextNode.prototype.clone = function () {
    return this;
};
```

**枚举变量** 使用 Pascal 命名法。**枚举的属性**， 使用全部字母大写，单词间下划线分隔的命名方式。

```javascript
var TargetState = {
    READING: 1,
    READED: 2,
    APPLIED: 3,
    READY: 4
};
```

## • 命名语法

**类名**，使用名词。

```javascript
function Engine(options) {}
```

**函数名**，使用动宾短语。

```javascript
function getStyle(element) {}
```

**boolean** 类型的变量使用 is 或 has 开头。

```javascript
var isReady = false;
var hasMoreCommands = false;
```

**Promise** 对象用动宾短语的进行时表达。

```javascript
var loadingData = ajax.get('url');
loadingData.then(callback);
```

## • 布尔

**下面的布尔表达式都返回 false:**

• null
• undefined
• '' 空字符串
• 0 数字0

**但小心下面的, 可都返回 true:**

• '0' 字符串0
• [] 空数组
• {} 空对象


## • 字符串

**字符串开头和结束使用单引号 `'` **

解释：

1.输入单引号不需要按住 `shift`，方便输入；
2.实际使用中，字符串经常用来拼接 HTML。为方便 HTML 中包含双引号而不需要转义写法。

示例：

```javascript
var str = '我是一个字符串';
var html = '<div class="cls">拼接HTML可以省去双引号转义</div>';
```

**使用 `数组` 拼接字符串**

```javascript
// 推荐
var arr = [], str;
arr.push('<ul>');
arr.push('<li>第一项</li>');
arr.push('<li>第二项</li>');
arr.push('<ul>');
str = arr.join('');

// 非常推荐
var str = [
    '<ul>',
        '<li>第一项</li>',
        '<li>第二项</li>',
    '</ul>'
].join('');
```

**复杂的数据到视图字符串的转换过程，选用一种模板引擎**

解释：

使用模板引擎有如下好处：

1.在开发过程中专注于数据，将视图生成的过程由另外一个层级维护，使程序逻辑结构更清晰；
2.优秀的模板引擎，通过模板编译技术和高质量的编译产物，能获得比手工拼接字符串更高的性能；
3.模板引擎能方便的对动态数据进行相应的转义，部分模板引擎默认进行HTML转义，安全性更好。

我们推荐使用 `artTemplate` 体积较小，在所有环境下性能高，语法灵活。


## • 数组

**使用数组字面量 `[]` 创建新数组，除非想要创建的是指定长度的数组**

```javascript
// 不推荐
var arr = new Array();

// 推荐
var arr = [];
```

**遍历数组不使用 `for in`**

for-in 循环只用于 `object/map/hash` 的遍历, 对 `Array` 用 for-in 循环有时会出错. 因为它并不是从 0 到 length - 1 进行遍历, 而是所有出现在对象及其原型链的键值。


**不因为性能的原因自己实现数组排序功能，尽量使用数组的 `sort` 方法**
  
解释：自己实现的常规排序算法，在性能上并不优于数组默认的 `sort` 方法。以下两种场景可以自己实现排序：
  
1.需要稳定的排序算法，达到严格一致的排序结果。
2.数据特点鲜明，适合使用桶排。
  
**清空数组使用 `arr.length = 0`**


## • 对象

**使用对象字面量 `{}` 创建新 `Object`**

```javascript
// 不推荐
var obj = new Object();

// 推荐
var obj = {};
```

**对象创建时，如果一个对象的所有 `属性` 均可以不添加引号，建议所有 `属性` 不添加引号**

```javascript
var info = {
    name: 'someone',
    age: 28
};
```

**对象创建时，如果任何一个 `属性` 需要添加引号，则所有 `属性` 建议添加 `'`**

```javascript
// 不推荐
var info = {
    name: 'someone',
    age: 28,
    'more-info': '...'
};

// 推荐
var info = {
    'name': 'someone',
    'age': 28,
    'more-info': '...'
};
```

**不允许修改和扩展任何原生对象和宿主对象的原型**

```javascript
// 以下行为绝对禁止
String.prototype.trim = function () {
  // TODO
};
```

**属性访问时，尽量使用 `.`**

属性名符合 Identifier 的要求，就可以通过 . 来访问，否则就只能通过 `[expr]` 方式访问。

通常在 JavaScript 中声明的对象，属性命名是使用 Camel 命名法，用 `.` 来访问更清晰简洁。部分特殊的属性（比如来自后端的 JSON ），可能采用不寻常的命名方式，可以通过 `[expr]` 方式访问。

```javascript
info.age;
info['more-info'];
```


# • jQuery 规范

## 使用最新版本的 jQuery

最新版本的 jQuery 会改进性能和增加新功能，若不是为了兼容旧浏览器，建议使用最新版本的 jQuery。以下是三条常见的 jQuery 语句，版本越新，性能越好。

![分别使用 1.4.2、1.4.4、1.6.2 三个版本测试浏览器在一秒内能够执行多少次，结果 1.6.2 版执行次数远超两个老版本](jq.png)

## jQuery 变量

1.存放 jQuery 对象的变量以 `$` 开头；
2.将 jQuery 选择器返回的对象缓存到本地变量中复用；
3.使用驼峰命名变量；

```javascript
var $myDiv = $('#myDiv');
$myDiv.click(function(){...});
```

## 选择器

1.尽可能的使用 ID 选择器，因为它会调用浏览器原生方法 `document.getElementById` 查找元素。当然直接使用原生 `document.getElementById` 方法性能会更好；
2.在父元素中选择子元素使用 `.find()` 方法性能会更好, 因为 ID 选择器没有使用到 Sizzle 选择器引擎来查找元素。

```javascript
//不推荐
var $productIds = $('#products .class');

//推荐
var $productIds = $('#products').find('.class');
```

## 事件

1.如果需要，对事件使用自定义的 `namespace`，这样容易解绑特定的事件，而不会影响到此 DOM 元素的其他事件监听；
2.对 Ajax 加载的 DOM 元素绑定事件时尽量使用事件委托。事件委托允许在父元素绑定事件，子代元素可以响应事件，也包括 Ajax 加载后添加的子代元素。

```javascript
$('#myLink').on('click.mySpecialClick', myEventHandler);
$('#myLink').unbind('click.mySpecialClick');
```

```javascript
// 不推荐
$('#list a').on('click', myClickHandler);

// 推荐
$('#list').on('click', 'a', myClickHandler);
```

## jQuery 模版插件

请参看：[https://github.com/jnoodle/plugin-templates/blob/master/jQuery-plugin-template.md](https://github.com/jnoodle/plugin-templates/blob/master/jQuery-plugin-template.md)