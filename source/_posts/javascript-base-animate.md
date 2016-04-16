---
title: JavaScript中的运动
date: 2016-04-09 13:23:47
tags: JavaScript运动
---

## 原理

> 运动其实就是在一段时间内改变元素 `width`、`height`、`top`、`right`、`bottom`、`left`和`opactiy`的值，到达目的后停止。

## 基础运动
- 匀速运动
- 缓冲运动
- 弹性运动

### 一.匀速运动

```javascript
/*
 * 公式：
 * 速度恒定
 * */
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

![匀速运动效果](匀速运动.gif)

<!--more-->

### 二.缓冲运动

```javascript
/*
 * 公式：
 * 速度 = (目标值 - 当前值)/系数
 * */
var iSpeed = 0;
function animate(ele, iTarget) {
    clearInterval(ele.timer);
    ele.timer = setInterval(function () {
        var curOffsetLeft = ele.offsetLeft;
        iSpeed = (iTarget - curOffsetLeft) / 10;
        iSpeed = iSpeed > 0 ? Math.ceil(iSpeed) : Math.floor(iSpeed);
        if (iSpeed == 0) {
            clearInterval(ele.timer);
        } else {
            ele.style.left = curOffsetLeft + iSpeed + 'px';
        }
    }, 20);
}
```

![缓冲运动效果](缓冲运动.gif)

### 三.弹性运动

```javascript
/*
 * 公式：
 * 速度 += (目标值 - 当前值)/系数（6、7、8）
 * 速度 *= 摩擦系数（0.7、0.75）
 * */
var iSpeed = 0;
function startMove(ele, iTarget) {
    clearInterval(ele.timer);
    ele.timer = setInterval(function () {
        var curOffsetLeft = ele.offsetLeft;
        iSpeed += (iTarget - curOffsetLeft) / 6;
        iSpeed *= 0.7;
        if (Math.abs(iSpeed) < 1 && Math.abs(iTarget - curOffsetLeft) < 1) {
            clearInterval(ele.timer);
            ele.style.left = iTarget + 'px';
        } else {
            ele.style.left = curOffsetLeft + iSpeed + 'px';
        }
    }, 30);
}
```

![弹性运动效果](弹性运动.gif)



