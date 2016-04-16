---
title: 速度版和时间版运动区别
date: 2016-04-10 21:14:49
tags: 速度版运动 时间版运动
---

## 定时器在浏览器中的问题

当我们把浏览器最小化 `Windows + D` 或者切换Tab页面时，此刻定时器执行速率会变缓，这是浏览器的一种机制，能够避免了资源浪费。

<!--more-->

## 速度版运动

其实我们最开始做运动时，都是从速度版开始的，诸如：

```javascript
var iSpeed = 1;
function animate(ele, iTarget) {
    clearInterval(ele.timer);
    ele.timer = setInterval(function () {
        var curOffsetLeft = ele.offsetLeft;
        if (curOffsetLeft >= iTarget) {
            clearInterval(ele.timer);
            ele.style.left = iTarget + 'px';
        } else {
            ele.style.left = curOffsetLeft + iSpeed + 'px';
        }
    }, 20);
}
```

很明显我们发现定时执行频率较高。

## 时间版运动

时间版运动其实就是指定这个运动从原始点执行到目标点耗费的**时间**，诸如jQuery就是利用时间版实现：

```javascript
$('#box2').animate({
    left: 500
}, 2000, 'linear');
```

## 区别

时间版运动更加节省资源，因此我们在切回浏览器时，我们会发现它会**准时到达目标点**，但是我们会发现速度版运动它切回浏览器时，**却还依旧在运动**。还有一个区别是速度版在做多值同时运动时，会出现有的属性提前到达目标点有的却后到达目标点。当然是不是这样速度版就一无是处呢？答案时否定的，我们设想在这样一个应用场景，从A点运动到B点，时间是5秒，在运动过程中我们鼠标移入物体，物体停止运动，当我们离开物体继续运动，这种场景时间版运动就会在中途运动到B点，速度就会更快了，但是速度版运动就不会有这个问题了。所以我们在项目中应该尽量取舍，这两种运动都有各自的优势，可谓是仁者见仁智者见智。

## 拓展

Tween算法是来自Flash的一个算法，后来也拓展到JavaScript中来了

```javascript
/*
 * t：current time（当前时间）
 * b：beginning value（初始值）
 * c：change in value（变化量）
 * d：duration（持续时间）
 *
 * return 目标点
 * */
var Tween = {
    linear: function (t, b, c, d) {  //匀速
        return c * t / d + b;
    },
    easeIn: function (t, b, c, d) {  //加速曲线
        return c * (t /= d) * t + b;
    },
    easeOut: function (t, b, c, d) {  //减速曲线
        return -c * (t /= d) * (t - 2) + b;
    },
    easeBoth: function (t, b, c, d) {  //加速减速曲线
        if ((t /= d / 2) < 1) {
            return c / 2 * t * t + b;
        }
        return -c / 2 * ((--t) * (t - 2) - 1) + b;
    },
    easeInStrong: function (t, b, c, d) {  //加加速曲线
        return c * (t /= d) * t * t * t + b;
    },
    easeOutStrong: function (t, b, c, d) {  //减减速曲线
        return -c * ((t = t / d - 1) * t * t * t - 1) + b;
    },
    easeBothStrong: function (t, b, c, d) {  //加加速减减速曲线
        if ((t /= d / 2) < 1) {
            return c / 2 * t * t * t * t + b;
        }
        return -c / 2 * ((t -= 2) * t * t * t - 2) + b;
    },
    elasticIn: function (t, b, c, d, a, p) {  //正弦衰减曲线（弹动渐入）
        if (t === 0) {
            return b;
        }
        if ((t /= d) == 1) {
            return b + c;
        }
        if (!p) {
            p = d * 0.3;
        }
        if (!a || a < Math.abs(c)) {
            a = c;
            var s = p / 4;
        } else {
            var s = p / (2 * Math.PI) * Math.asin(c / a);
        }
        return -(a * Math.pow(2, 10 * (t -= 1)) * Math.sin((t * d - s) * (2 * Math.PI) / p)) + b;
    },
    elasticOut: function (t, b, c, d, a, p) {    //正弦增强曲线（弹动渐出）
        if (t === 0) {
            return b;
        }
        if ((t /= d) == 1) {
            return b + c;
        }
        if (!p) {
            p = d * 0.3;
        }
        if (!a || a < Math.abs(c)) {
            a = c;
            var s = p / 4;
        } else {
            var s = p / (2 * Math.PI) * Math.asin(c / a);
        }
        return a * Math.pow(2, -10 * t) * Math.sin((t * d - s) * (2 * Math.PI) / p) + c + b;
    },
    elasticBoth: function (t, b, c, d, a, p) {
        if (t === 0) {
            return b;
        }
        if ((t /= d / 2) == 2) {
            return b + c;
        }
        if (!p) {
            p = d * (0.3 * 1.5);
        }
        if (!a || a < Math.abs(c)) {
            a = c;
            var s = p / 4;
        }
        else {
            var s = p / (2 * Math.PI) * Math.asin(c / a);
        }
        if (t < 1) {
            return -0.5 * (a * Math.pow(2, 10 * (t -= 1)) *
                Math.sin((t * d - s) * (2 * Math.PI) / p)) + b;
        }
        return a * Math.pow(2, -10 * (t -= 1)) *
            Math.sin((t * d - s) * (2 * Math.PI) / p) * 0.5 + c + b;
    },
    backIn: function (t, b, c, d, s) {     //回退加速（回退渐入）
        if (typeof s == 'undefined') {
            s = 1.70158;
        }
        return c * (t /= d) * t * ((s + 1) * t - s) + b;
    },
    backOut: function (t, b, c, d, s) {
        if (typeof s == 'undefined') {
            s = 3.70158;  //回缩的距离
        }
        return c * ((t = t / d - 1) * t * ((s + 1) * t + s) + 1) + b;
    },
    backBoth: function (t, b, c, d, s) {
        if (typeof s == 'undefined') {
            s = 1.70158;
        }
        if ((t /= d / 2 ) < 1) {
            return c / 2 * (t * t * (((s *= (1.525)) + 1) * t - s)) + b;
        }
        return c / 2 * ((t -= 2) * t * (((s *= (1.525)) + 1) * t + s) + 2) + b;
    },
    bounceIn: function (t, b, c, d) {    //弹球减振（弹球渐出）
        return c - Tween['bounceOut'](d - t, 0, c, d) + b;
    },
    bounceOut: function (t, b, c, d) {
        if ((t /= d) < (1 / 2.75)) {
            return c * (7.5625 * t * t) + b;
        } else if (t < (2 / 2.75)) {
            return c * (7.5625 * (t -= (1.5 / 2.75)) * t + 0.75) + b;
        } else if (t < (2.5 / 2.75)) {
            return c * (7.5625 * (t -= (2.25 / 2.75)) * t + 0.9375) + b;
        }
        return c * (7.5625 * (t -= (2.625 / 2.75)) * t + 0.984375) + b;
    },
    bounceBoth: function (t, b, c, d) {
        if (t < d / 2) {
            return Tween['bounceIn'](t * 2, 0, c, d) * 0.5 + b;
        }
        return Tween['bounceOut'](t * 2 - d, 0, c, d) * 0.5 + c * 0.5 + b;
    }
};
```

![当使用正则表达式返回了想要的结果时程序员的样子](http://images.cnitblog.com/news/66372/201304/24143338-b7367e7223944b7db7ac847f7d643d28.gif)

