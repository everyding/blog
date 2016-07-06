---
title: CSS锦囊妙计
date: 2016-04-15 13:47:12
tags: CSS锦囊妙计
---

## a伪类顺序

喜欢（love）和讨厌（hate），l(:link)ov(:visited)e，h(:hover)a(:active)te

## 让一个块级元素在某区域内居中（水平和垂直），兼容IE8+

```html
<div class="container">
    <div class="box"></div>
</div>

.container{
    width: 300px;
    height: 300px;
    border: 1px #000 solid;

    position: relative;
}

.box{
    width: 50px;
    height: 50px;
    border: 1px #000 solid;

    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    margin: auto;
}
```

## 在 `Chrome` 浏览器的 `Elements` 里面选中某个元素，按 `H` 可以隐藏该元素。

## 文字换行

```css
/*强制不换行*/
white-space: nowrap; 

/*自动换行*/
word-wrap: break-word;
word-break: normal;

/*强制英文单词断行*/
work-break: break-all;
```

<!--more-->

## [两端对齐](http://www.cnblogs.com/rubylouvre/archive/2012/11/28/2792504.html)

```css
text-align: justify;
text-justify: distribute-all-lines; /*ie6-8*/
text-align-last: justify; /*ie9+*/
-moz-text-align-last: justify; /*ff*/
-webkit-text-align-last: justify; /*chrome 20+*/
```

## [去掉Webkit浏览器中input（或者textarea）的黄色焦点框](http://www.cnblogs.com/niao/archive/2012/09/07/2674511.html)

```css
input, button, select, textarea{ outline: none; }
textarea{ font-size: 13px; resize: none; }
```

## [去掉chrome记住密码后自动填充表单的黄色背景](http://zcoder.cn/2015/01/14/front-end/chrome-autofill/)

## clearfix

```css
.clearfix:after{ visibility: hidden; display: block; font-size: 0; content: " "; clear: both; height: 0; }
.clearfix{ display: inline-block; }
html[xmlns] .clearfix{ display: block; }
* html .clearfix{ height: 1%; }

.clearfix{ *zoom: 1; }
.clearfix:after{ clear: both; display: table; content: ""; }

.clearfix{ overflow: hidden; _zoom: 1; }
```

## min-height: 最小高度兼容代码

```css
.minheight500{ min-height: 500px; height: auto !important; height: 500px; overflow: visible; }
```

## 鼠标不允许点击光标样式

```css
cursor: not-allowed;
```

## Mac font: OS X平台字体优化

```css
font-family: "Hiragino Sans GB", "Hiragino Sans GB W3", '微软雅黑';
```

## 文字过多后显示省略号

```css
.ellipsis, .ell{ white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
```

## 标签属性title换行

`&#13;`

## 关闭 x 符号

`&#215;`

## 全站变灰 gray

```css
html{
    filter: grayscale(100%);
    -webkit-filter: grayscale(100%);
    -moz-filter: grayscale(100%);
    -ms-filter: grayscale(100%);
    -o-filter: grayscale(100%);
    filter: url("data:image/svg+xml;utf8,<svg xmlns=\'http://www.w3.org/2000/svg\'><filter id=\'grayscale\'><feColorMatrix type=\'matrix\' values=\'0.3333 0.3333 0.3333 0 0 0.3333 0.3333 0.3333 0 0 0.3333 0.3333 0.3333 0 0 0 0 0 1 0\'/></filter></svg>#grayscale");
    filter:progid:DXImageTransform.Microsoft.BasicImage(grayscale=1);
    -webkit-filter: grayscale(1);
}
```

## 取消textarea右下角可拖动手柄

```css
resize: none;
```

## 移动端点击取消背景黑框

```css
a{-webkit-tap-highlight-color:rgba(0,0,0,0);}
```

## 取消input,button焦点或点击时蓝色边框

```css
input{ outline: none; }
```

## placeholder占位符颜色自定义

```css
input:-moz-placeholder {color: #369;}
::-webkit-input-placeholder {color:#369;}
```

## 禁止选中文本

```css
-moz-user-select:none;
-webkit-user-select:none;
-ms-user-select:none;
user-select:none;
```

## 模糊（毛玻璃）

[效果1](http://www.zhangxinxu.com/wordpress/2013/11/css-svg-image-blur/)
[效果2](http://mao.li/css3-blur-filter-pratice/)
[终极效果](http://codepen.io/ariona/pen/geFIK)


## 屏蔽苹果浏览器对数字的识别

```html
<meta content="telephone=no" name="format-detection">
```

## HTML5手机浏览直接给一个号码打电话，发短信

```html
<!--移动web页面自动探测电话号码-->
<meta name="format-detection" content="telephone=no">
<meta http-equiv="x-rim-auto-match" content="none">

<a href="tel:15222222222">移动WEB页面JS一键拨打号码咨询功能</a>
<a href="sms:15222222222">移动WEB页面JS一键发送短信咨询功能</a>
```

## CSS判断横屏竖屏

```html
@media screen and (orientation: portrait) {
  /*竖屏 css*/
} 
@media screen and (orientation: landscape) {
  /*横屏 css*/
}
```
&nbsp;

```javascript
//判断手机横竖屏状态：
window.addEventListener("onorientationchange" in window ? "orientationchange" : "resize", function() {
    //移动端的浏览器一般都支持window.orientation这个参数，通过这个参数可以判断出手机是处在横屏还是竖屏状态。
    if (window.orientation === 180 || window.orientation === 0) { 
        alert('竖屏状态！');
    } 
    if (window.orientation === 90 || window.orientation === -90 ){ 
        alert('横屏状态！');
    }  
}, false); 
```

## rem适配

```javascript
function calcRem(){
    var oSize = parseFloat(document.documentElement.clientWidth/7.5).toFixed(4);
    oSize = oSize > 64 ? 64 : oSize;
    document.getElementsByTagName("html")[0].style.fontSize = oSize + "px" ;
}
window.addEventListener("load", calcRem);
window.addEventListener("resize", calcRem);
```





