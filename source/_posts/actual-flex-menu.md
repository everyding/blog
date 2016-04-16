---
title: 【实战】弹性菜单
date: 2016-04-09 19:04:04
tags: 弹性运动 透视特效
---

## 实现源码：

```html
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title>带透视效果的弹性菜单</title>
    <style>
        ul{width: 600px;height: 40px;background-color: #eee;padding: 0;margin: 0 auto;}
        li{list-style: none;float: left;width: 150px;height: 40px;line-height: 40px;text-align: center;cursor: pointer;}
        #ul1{position: relative;top: 100px;}
        #ul3{color: white;position: absolute;left: 0;top: 0;background-color: transparent;}
        #mark{width: 150px;position: absolute;top: 0;left: 0;background-color: pink;overflow: hidden;}
    </style>
</head>
<body>
<ul id="ul1">
    <ul id="ul2">
        <li>首页</li>
        <li>新闻中心</li>
        <li>产品列表</li>
        <li>关于我们</li>
    </ul>
    <li id="mark">
        <ul id="ul3">
            <li>首页</li>
            <li>新闻中心</li>
            <li>产品列表</li>
            <li>关于我们</li>
        </ul>
    </li>
</ul>
<script>
    var lis = document.getElementById('ul2').getElementsByTagName('li'),
        mark = document.getElementById('mark'),
        ul3 = document.getElementById('ul3'),
        iSpeed = 0,
        i = 0;

    for (; i < lis.length; i++) {
        lis[i].onmouseover = lis[i].onmouseout = function () {
            animate(this.offsetLeft);
        };
    }

    function animate(iTarget) {
        clearInterval(mark.timer);
        mark.timer = setInterval(function () {
            var curOffsetLeft = mark.offsetLeft;
            iSpeed += (iTarget - curOffsetLeft) / 7;
            iSpeed *= 0.75;

            if (Math.abs(iSpeed) < 1 && Math.abs(iTarget - curOffsetLeft) < 1) {
                clearInterval(mark.timer);
                mark.style.left = iTarget + 'px';
                ul3.style.left = -iTarget + 'px';
            } else {
                var tmpOL = curOffsetLeft + iSpeed;
                mark.style.left = tmpOL + 'px';
                ul3.style.left = -tmpOL + 'px';
            }
        }, 20);
    }
</script>
</body>
</html>
```

![弹性菜单效果](弹性菜单.gif)
