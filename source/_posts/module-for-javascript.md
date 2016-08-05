---
title: 谈JavaScript模块儿化
date: 2016-08-05 16:15:35
tags: 模块儿化
---

## 序

在做服务器开发的时候，诸如 `Java / .NET` 开发中我们都听过命名空间（洋名：`namespace`），我们通常会把各个功能放到一个模块儿下，比如在 `Java` 中我们对文件进行操作，需要导入 `File` 类

```java
import java.io.File; //导入File类

File f1 = new File("example.txt");
```

<!--more-->


比如我们在 `.NET` 中需要对文件操作，就需要对文件进行操作，就需要引入命名空间 `System.IO`

```csharp
using System.IO; //引用命名空间

FileStream sFile = new FileStream("example.txt", FileMode.Open);
```

当然 `php` 中引入某个模块儿是用 `require` ，我们在 `nodejs` 中也是用 `require` 这个方法，在此我就不一一举栗了。

## 意义

其实模块儿化就是为更好的分工，各个模块完成`单一职责`，如果没有模块儿化开发，我们的东西就如同一锅大杂烩，这样不利于项目的协同开发和维护，在服务器开发中已经严格的将各个模块进行划分了，对于系统的类我可以直接导入，或者引用命名空间，当然对于第三方类库，我们可以引用 `jar`、`dll`方式。

## 前端模块儿化

前端html/css/javascript相对松散，这里我就主要对JavaScript模块儿化进行说明，在js中模块儿化通常都有AMD、CMD、CommonJS及UMD规范。

### AMD规范

AMD规范，全称 **Asynchronous Module Definition**，称为**异步模块加载规范**。一般应用在**浏览器端**，流行的浏览器端异步加载库[RequireJS](http://www.requirejs.org/)实现的就是AMD规范。

下面是使用AMD规范定义一个名为foo模块方式，此模块儿依赖jquery。

```javascript
// 文件名: foo.js
define(['jquery'], function () {
    // 定义fn方法
    function fn(){};
    
    // 暴露公共方法
    return fn;
});
```

AMD讲究的是**前置执行**。稍微复杂的例子如下，foo模块有多个依赖及方法暴漏，

```javascript
// 文件名: foo.js
define(['jquery', 'underscore'], function ($, _) {
    // 一些方法
    function a(){};//私有方法
    function b(){};//共有方法
    function c(){};//共有方法

    // 暴露公共方法
    return {
        b: b,
        c: c
    }
});
```

`define`是**AMD**规范用来声明模块的接口，示例中的第一个参数是一个数组，表示当前模块的依赖。第二个参数是一个回调函数，表示此模块的执行体。只有当依赖数组中的所有依赖模块都是可用的时，AMD模块加载器（比如`RequireJS`）才会去执行回调函数并返回此模块的暴露接口。

注意，回调函数中参数的顺序与依赖数组中的依赖顺序一致。（即：`jquery`->`$`，`underscore`->`_`）当然，在这里我可以将回调函数的参数名称改成任何我们想用的可用变量名，这并不会对模块的声明造成任何影响。除此之外，你不能在模块声明的外部使用$或者_，因为他们只在模块的回调函数体中才有定义。关于`AMD`规定声明模块的更多内容，请参考[这里](https://github.com/amdjs/amdjs-api/wiki/AMD#using-require-and-exports)。

### CMD规范

`CMD`规范，全称 **Common Module Definition**，称为**通用模块加载规范**。一般也是用在**浏览器端**。浏览器端异步加载库[Sea.js](http://seajs.org/docs/)实现的就是`CMD`规范。

下面是使用AMD规范定义一个名为foo模块的方式，此模块依赖jquery，

```javascript
define(function (require, exports, module) {
    // 加载依赖
    var $ = require('jquery');
    
    // 定义fn方法
    function fn(){};

    // 暴露fn方法
    return fn;
});
```

CMD规范倾向依赖就近，稍微复杂一点例子

```javascript
define(function (requie, exports, module) {
    // 依赖可以就近书写
    var a = require('./a');
    a.test();
    
    // ...
    // 软依赖
    if (status) {
        var b = requie('./b');
        b.test();
    }
});
```

### CommonJS规范

根据**CommonJS**规范，一个单独的文件就是一个模块。每一个模块都是一个单独的作用域，也就是说，在一个文件定义的变量（还包括函数和类），都是私有的，对其他文件是不可见的。一般也是用在**服务器端**。

如果你在`Node.js`平台上写过东西，你应该会比较熟悉`CommonJS`规范。加载的模块文件一般都已经存在本地硬盘，所以加载起来比较快，不用考虑异步加载的方式，所以`CommonJS`规范比较适用。与前面的`AMD`及`CMD`规范不一样的是，`CommonJS`规范一般应用于服务端（`Node.js`平台），而且`CommonJS`加载模块采用的是同步方式（这跟他适用的场景有关系）。同时，得力于[Browserify](https://github.com/substack/node-browserify)这样的第三方工具，我们可以在浏览器端使用采用`CommonJS`规范的js文件。

下面是使用CommonJS规范声明一个名为foo模块的方式，同时依赖jquery模块，

```javascript
// 文件名: foo.js
// 加载依赖
var $ = require('jquery');

// 定义fn方法
function fn(){};

// 暴露fn方法
module.exports = fn;
```

稍微复杂一点的示例如下，拥有多个依赖以及抛出多个接口，

```javascript
// 文件名: foo.js
var $ = require('jquery');
var _ = require('underscore');

// 定义一些方法
function a(){};    // 私有方法
function b(){};    // 共有方法
function c(){};    // 共有方法

// 暴露a、b方法
module.exports = {
    b: b,
    c: c
};
```

### UMD规范

因为`AMD`，`CommonJS`规范是两种不一致的规范，虽然他们应用的场景也不太一致，但是人们仍然是期望有一种统一的规范来支持这两种规范。于是，`UMD`（`Universal Module Definition`，称之为`通用模块规范`）规范诞生了。

```javascript
(function (root, factory) {
    if (typeof define === 'function' && define.amd) {
        // AMD
        define(['jquery'], factory);
    } else if (typeof exports === 'object') {
        // Node, CommonJS-like
        module.exports = factory(require('jquery'));
    } else {
        // Browser globals (root is window)
        root.returnExports = factory(root.jQuery);
    }
}(this, function ($) {
    // methods
    function myFunc(){};

    // exposed public method
    return myFunc;
}));
```

> 个人觉得`UMD`规范更像一个语法糖。应用`UMD`规范的`js`文件其实就是一个立即执行函数。函数有两个参数，第一个参数是当前运行时环境，第二个参数是模块的定义体。在执行`UMD`规范时，会优先判断是当前环境是否支持`AMD`环境，然后再检验是否支持`CommonJS`环境，否则认为当前环境为浏览器环境（`window`）。当然具体的判断顺序其实是可以调换的。

下面是一个更加复杂的示例，

```javascript
(function (root, factory) {
    if (typeof define === 'function' && define.amd) {
        // AMD
        define(['jquery', 'underscore'], factory);
    } else if (typeof exports === 'object') {
        // Node, CommonJS-like
        module.exports = factory(require('jquery'), require('underscore'));
    } else {
        // Browser globals (root is window)
        root.returnExports = factory(root.jQuery, root._);
    }
}(this, function ($, _) {
    //    methods
    function a(){};    //    private because it's not returned (see below)
    function b(){};    //    public because it's returned
    function c(){};    //    public because it's returned

    //    exposed public methods
    return {
        b: b,
        c: c
    }
}));
```

如果你写了一个小工具库，你想让它及支持`AMD`规范，又想让他支持`CommonJS`规范，那么采用`UMD`规范对你的代码进行包装吧，就像[这样](https://github.com/gejiawen/bullhead/blob/master/index.js)。

### 小结

> `AMD`，`CMD`是用在浏览器端的，异步的，如**RequireJS**和**SeaJS**; 
> `CommonJS`是用在服务器端的，同步的，如**NodeJS**;
> 其中，`AMD`先提出，`CMD`是根据`CommonJS`和`AMD`基础上提出的。 
