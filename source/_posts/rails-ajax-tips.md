title: rails ajax tips
date: 2016-04-20 09:23:26
category: rails
tags:
---
前不久在做一个rails项目时，要实现一个ajax刷新页面效果，rails能收到发来的请求，但是总是去渲染html页面，而不是渲染对应的js.erb文件，而这个controller里的action需要同时响应html和ajax请求。

那么rails是怎么和ajax结合的呢，首先要了解什么是SJR（Server-generated JavaScript Responses），这个可以看DHH大神的文章，翻译版：https://ruby-china.org/topics/16132

首先rails传统的ajax方案是给link或者form加一个:remote => true, 这样做会由jquery-ujs对链接进行劫持把普通请求变成ajax请求，其中很重要的一条就是增加一个datatype参数，然后在request请求中会带上Accept参数，rails会根据Accept进行响应分发。比如datatype为script，则响应js文件，datatype为json，则响应json文件。jquery-ujs默认的datatype为script。
这样做的话，那么下面的请求都会正常响应：
```
<%= link_to 'index', root_url %> //返回html
<%= link_to 'index', root_url, :remote => true %> //返回js
```
你还可以指定请求类型：
```
<%= link_to 'index', root_url, :remote => true, "data-type" => :json %> //返回json
```

如果自己写ajax请求的话要注意带上dataType，以保证rails正确响应你的请求：
```js
    $.ajax({
      method: method,
      url: action,
      data: data,
      dataType: 'script'
    });
```

还有一种方案是在url中带上后缀，利用route将format传入action：
```js
    $.ajax({
      method: method,
      url: http://127.0.0.1:3000/index.js,
      data: data,
    });
```
action会根据format进行响应：
```
respond_to do |format|
    format.html
    format.js {} //返回js
end
```
参考：
http://tech.thereq.com/post/17243732577/rails-3-using-linkto-remote-true-with-jquery
http://roseweixel.github.io/blog/2015/07/05/integrating-ajax-and-rails-a-simple-todo-list-app/
