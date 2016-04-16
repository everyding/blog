---
title: TweenMax基础入门
date: 2016-04-16 16:35:09
tags: TweenMax
---

## to()

**移动到目标点**

> * 参数一：元素或者对象
> * 参数二：执行时间（单位：秒）
> * 参数三：移动到目标点属性，回调也在该对象中
> * 参数四：延时（单位：秒，除了数字还可以是表达式，诸如：'+=1'、'-=0.5'）

示例：

```javascript
var t = new TimelineMax();

t.to(box, 1, { width: 200, onComplete: function(){
    alert(20);
}}, 1);
t.to(box, 1, { height: 200, onReverseComplete: function(){
        alert('高度100px');
    } }, '+=1');
t.to(box, 2, { left: 200 });
t.to(box, 2, { top: 200 });
t.to(box, 2, { rotation: 180 });
t.to(box, 2, { opacity: 0 });
```

<!--more-->

## play()、stop()、reverse()、clear()

分别表示：`开始运动`、`停止运动`、`反转运动`、`清除动画`

示例：

```javascript
btnPlay.onclick = function(){
    t.play();
};

btnStop.onclick = function(){
    t.stop();
};

btnReverse.onclick = function(){
    t.reverse();
};

btnClear.onclick = function(){
    t.clear();
};
```

## add()、tweenTo()

add()用于添加状态，tweenTo()标识运动到那个状态，只需要传入一个状态即可

```javascript
var t = new TimelineMax();

t.add('state0');//添加状态：'state0'
t.to(box, 1, {width: 200}, 1);
t.to(box, 1, {height: 200}, '+=1');
t.add('state1');
t.to(box, 2, {left: 200});
t.to(box, 2, {top: 200});
t.add('state2');
t.to(box, 2, {rotation: 180});
t.to(box, 2, {opacity: 0});
t.add('state3');
t.stop();

t.tweenTo('state2');//运动到状态：'state2'
```

## time()

time()获取动画执行的时间

```javascript
var t = new TimelineMax();

t.to(box, 1, {width: 200}, 1);
t.to(box, 1, {height: 200, onComplete: function(){
 alert('执行时间' + t.time() + '秒');
}}, '+=1');
```

## totalDuration()、currentLabel()、getLabelTime()

totalDuration()动画执行总时间，currentLabel()当前的状态，getLabelTime()该状态下执行时间

```javascript
var t = new TimelineMax();

t.add('state0');
t.to(box, 1, {width: 200}, 1);
t.to(box, 1, {height: 200}, '+=1');
t.add('state1');
t.to(box, 2, {left: 200, onComplete: function(){
    alert('当前状态执行时间：' + t.getLabelTime(t.currentLabel()));
}});
t.to(box, 2, {top: 200});
t.add('state2');
t.to(box, 2, {rotation: 180, onComplete: function(){
    alert('当前状态：' + t.currentLabel());
}});
t.to(box, 2, {opacity: 0});
t.add('state3');

alert('动画执行总时间：' + t.totalDuration());
```

## getLabelBefore()、getLabelAfter()

getLabelBefore()上一个状态，getLabelAfter()下一个状态

```javascript
var t = new TimelineMax();

t.add('state0');
t.to(box, 1, {width: 200}, 1);
t.to(box, 1, {height: 200, onComplete: getInfo}, '+=1');

t.add('state1');
t.to(box, 2, {left: 200});
t.to(box, 2, {top: 200, onComplete: getInfo});

t.add('state2');
t.to(box, 2, {rotation: 180});
t.to(box, 2, {opacity: 0, onComplete: getInfo});

t.add('state3');

getInfo();

function getInfo() {
    var currentLabel = t.currentLabel();//当前状态
    var currentTime = t.getLabelTime(currentLabel);//当前时间
    var beforeLabel = t.getLabelBefore(currentTime);
    var afterLabel = t.getLabelAfter(currentTime);

    info.innerHTML = '上一个状态：' + beforeLabel + '<br>当前状态：' + currentLabel + '<br>下一个状态：' + afterLabel;
}
```

## seek()

seek()直接执行到目标，无动画特效




