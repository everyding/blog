---
title: 弹性布局
date: 2017-01-15 13:51:22
tags: 布局
---

![flex布局思维导图](flex.png)

<!--more-->

## 基础与术语

### 对于父属性（Flex容器）

![对于父属性](flex-container.svg)

#### 显示（display）

这里定义了柔性容器，内联或块，取决于给定的值。它为所有直接子项启用了一个flex上下文。

```css
.container {
    display: flex; /* inline-flex */
}
```

**注意，CSS列对flex容器没有影响。**

#### 柔性方向（flex-direction）

![柔性方向](flex-direction2.svg)

这建立了主轴，因此定义了挠性​​物品被放置在挠性容器中的方向。Flexbox（除了可选的包装）单向布局概念。将flex项目视为主要布置在水平行或垂直列中。

```css
.container {
    flex-direction: row | row-reverse | column | column-reverse;
}
```

> * `row`（默认）：左到右 `ltr`; 从右到左 `rtl`
> * `row-reverse`：从右到左的 `ltr`; 从左到右 `rtl`
> * `column`：相同 `row` 但从上到下
> * `column-reverse`：相同 `row-reverse`，但底部到顶部

#### 柔性包装（flex-wrap）

![柔性包装](flex-wrap.svg)

默认情况下，flex项目都将尝试适合一行。您可以更改此选项，并允许根据需要使用此属性包装项目。方向在这里也起作用，确定新线被堆叠的方向。

```css
.container {
    flex-wrap: nowrap | wrap | wrap-reverse;
}
```

> * `nowrap`（默认）：单行/左到右`ltr`; 从右到左`rtl`
> * `wrap`：多行/左至右`ltr`; 从右到左`rtl`
> * `wrap-reverse`：多行/从右到左在`ltr`; 从左到右`rtl`

#### flex-flow（适用于：parent flex容器元素）

这是一个速记`flex-direction`和`flex-wrap`性质，它们共同确定了挠曲容器的主要和交叉轴。默认值是`row nowrap`。

```css
flex-flow: <‘flex-direction’> || <‘flex-wrap’>
```

#### 对齐内容（justify-content）

![对齐内容](justify-content.svg)

这定义了沿着主轴的对准。当一行上的所有flex项目不灵活，或者灵活但已达到其最大大小时，它有助于分配额外的剩余空间。当它们溢出线时，它也对项目的对齐施加一些控制。

```css
.container {
    justify-content: flex-start | flex-end | center | space-between | space-around;
}
```

> * `flex-start` （默认）：项目被打包到开始行
> * `flex-end`：项目朝向结束行包装
> * `center`：项目沿线居中
> * `space-between`：项目均匀分布在行中; 第一项在开始行，最后一项在结束行
> * `space-around`：项目均匀分布在其周围等间距的线上。注意，视觉上空间不相等，因为所有项目在两侧具有相等的空间。第一个项目将相对于容器边缘具有一个单位的空间，但是在下一个项目之间有两个单位的空间，因为下一个项目具有适用的自己的间隔。

#### 对齐项目（align-items）

![对齐项目](align-items.svg)

这定义了如何在当前行上沿交叉轴布置弹性项目的默认行为。把它作为justify-content版本为十字轴（垂直于主轴）。

```css
.container {
    align-items: flex-start | flex-end | center | baseline | stretch;
}
```

> * `flex-start`：项目的交叉开始边缘被放置在交叉开始线上
> * `flex-end`：将跨边缘边缘的项目放置在横线上
> * `center`：项目以交叉轴为中心
> * `baseline`：项目是对齐的，例如它们的基线对齐
> * `stretch` （默认）：stretch以填充容器（仍然尊重min-width / max-width）

#### align-content

这种对齐时，有在交叉轴额外的空间，类似于如何内柔性容器的线justify-content对齐主轴线中的个别项目。

**注：此属性没有效果时，只有一条弯曲线项目。**

```css
.container {
    align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}
```

> * `flex-start`：行包装到容器的开头
> * `flex-end`：填充到容器末端的行
> * `center`：填充到容器中心的线
> * `space-between`：线均匀分布; 第一行在容器的开头，而最后一行在结束
> * `space-around`：线均匀分布，每条线周围等间距
> * `stretch` （默认）：lines stretch以占用剩余空间

### 对于子属性（弯曲项）

![对于子属性](flex-items.svg)

参看：[https://css-tricks.com/snippets/css/a-guide-to-flexbox/](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)


