---
title: m3u8格式的视频播放器
date: 2016-04-13 20:55:25
tags: m3u8 视频播放器
---

最近在公司要实现一个Web端视频播放器功能，然后Google各种方案，诸如国产的ckplayer这些，最终还是找到了国外开源的优秀解决方案，我们需要引入一个js文件swfobject.js和两个flash组件：OSMF和HLSProvider来播放。

上面几个开源项目地址：

> * [http://osmf.org](http://osmf.org)
> * [http://osmf.org/dev/2.0gm/StrobeMediaPlayback.html](http://osmf.org/dev/2.0gm/StrobeMediaPlayback.html)
> * [https://github.com/mangui/HLSprovider](https://github.com/mangui/HLSprovider)

<!--more-->

[m3u8](https://zh.wikipedia.org/wiki/M3U)格式我就不介绍了，现在所有的视频网站基本都是通过m3u8的方式来播放视频。

在浏览器上播放m3u8的视频地址有两种方式：

## 1.html的video标签方式

```html
<!DOCTYPE hmtl>
<html>
<head>
<title>the5fire m3u8 test</title>
</head>
<body>
<video controls autoplay>
    <source src="http://www.example.com/example.m3u8">
</video>
</body>
</html>
```

比较遗憾的是目前只有Safari支持，因此通用性不好，若想要更好的兼容就必须采用flash方式，也就是第二种方式。

## 2.flash方式

```html
<!DOCTYPE html>
<html>
<head>
<title>the5fire m3u8 test</title>
<script src="./swfobject.js"></script>
</head>
<body>
<div id="player">
</div>
<script>
    var flashvars = {
        // M3U8 url, or any other url which compatible with SMP player (flv, mp4, f4m)
        // escaped it for urls with ampersands
        src: escape("http://www.example.com/example.m3u8"),
        // url to OSMF HLS Plugin
        plugin_m3u8: "HLSProviderOSMF.swf",
    };
    var params = {
        // self-explained parameters
        allowFullScreen: true,
        allowScriptAccess: "always",
        bgcolor: "#000000"
    };
    var attrs = {
        name: "player"
    };

    swfobject.embedSWF(
        // url to SMP player
        "StrobeMediaPlayback.swf",
        // div id where player will be place
        "player",
        // width, height
        "800", "485",
        // minimum flash player version required
        "10.2",
        // other parameters
        null, flashvars, params, attrs
    );
</script>
</body>
</html>
```

这是目前Web视频播放器，免费的最优秀的解决方案。

![当老板问是谁把服务器给弄瘫痪了时程序员的样子](1.gif)


