title: 解决hexo的jquery和fonts被墙
date: 2016-03-09 16:02:37
category: hexo
tags:
---
因为众所周知的原因，骄傲的中国人是不(wu)用(fa)访问ajax.googleapis.com和fonts.googleapis.com这两个网址的，所以jquery和google fonts会响应超时，严重影响我们的hexo博客的用户体验。解决方法是换成360提供的cdn,以hexo官方默认模版landscape为例：
```
打开
themes/landscape/layout/_partial/after-footer.ejs
找到
<script src="//ajax.googleapis.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>
替换为
<script src="//ajax.useso.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>
```

```
打开
themes/landscape/layout/_partial/head.ejs
找到
<link href="//fonts.googleapis.com/css?family=Source+Code+Pro" rel="stylesheet" type="text/css">
替换为
<link href="//fonts.useso.com/css?family=Source+Code+Pro" rel="stylesheet" type="text/css">
```

ref: http://libs.useso.com/