js动态追加 css js html
=====================

*本文素有实现方式都是在非IE环境下*

## 追加 css样式

*静态css文件引入外部css文件语法：`@import url(style.css);`*

### 通过 `link` 添加样式

原生js通过向页面追加link标签来追加样式

```js

var style = document.createElement('link');
style.href = 'css文件外部路径';
style.rel = 'stylesheet';
style.type = 'text/css';
var head = document.head || document.getElementsByTagName('head')[0];
head.appendChild( style );

// document.head属于h5内容，IE6/7/8不支持，IE9/Safari/Chrome/FF/Opera均支持。

// 顺带看了一眼 item[0] 返回元素的首个子节点
// 参考链接： https://developer.mozilla.org/zh-CN/docs/Web/API/NodeList/item

```

### 通过 `style` 添加样式

原生js通过向页面追加style标签来追加样式

```js

var style = document.createElement('style');
style.type = 'text/css';
style.innerHTML = "body{background-color:#ff6700;}";
document.getElementsByTagName('head')[0].appendChild( style );

```


## 动态追加 js

### 以链接形式动态加入

```js

var script = document.createElement('script');
script.type = 'text/javascript';
script.src = 'files.js';
document.getElementsByTagName('head')[0].appendChild( script );

```

### 以代码形式动态加入

```js

var script = document.createElement('script');
script.type = 'text/javascript';
script.innerHTML = 'alert("hello world")';
document.getElementsByTagName('head')[0].appendChild( script );

```

## 动态追加 html

### 使用DOM追加

```js

var dialog = document.createElement('div');
var img = document.createElement('img');
var btn = document.createElement('input');
var content = document.createElement('span');

// 添加class
dislog.className = 'dialog';

// 添加属性
img.src = 'close.png';

// 添加行内样式
btn.style.paddingRight = '10px';

// 添加文本
span.innerHTML = 'this is btn';

// 向容器内追加
dialog.appendChild( img );
dialog.appendChild( btn );
dialog.appendChild( span );

```

不考虑IE兼容，添加类型还可以使用`classList`，[classList Web-API-Element](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/classList)

### 使用HTML5 template

```html

<template id="dialog_tpl">
	<div class="dialog">
		<img src="" alt="">
		<input type="button" value="confirm">
		<span></span>
	</div>
</template>

```

```js

var dialog = document.querySelector('#dialog_tpl');
dialog.content.querySelector('img').src = 'close.png';
dialog.content.querySelector('soan').innerHTML = 'this is btn';
document.getElementsByTagName('body')[0].appendChild( dialog.content.cloneNode( true ) );

```

[Node.cloneNode API文档](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/cloneNode)

参考链接： 

1. http://www.cnblogs.com/stephenykk/p/5406614.html
2. http://blog.csdn.net/zxf13598202302/article/details/50485113
3. https://segmentfault.com/q/1010000002596371