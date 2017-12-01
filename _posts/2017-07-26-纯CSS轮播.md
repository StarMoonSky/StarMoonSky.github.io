---
layout:     post
title:      CSS轮播
subtitle:   利用 纯CSS3动画制作轮播,弱化客户端的js
date:       2017-07-26
author:     CC
header-img: img/post-bg-hacker.jpg
catalog: true
tags:
    - css
    - JAVASCRIPT
---


## 其实也没啥卵用

平常我们都会用js写轮播,其实也没人写了,都是复制粘贴一把梭

## 正文

我最近的项目里,有一个展示区域,需要用到轮播,项目已经提交服务器了,需要改一个样式,顺便搞个slider,就都在一个css文件里搞了.
html结构是这样的

```objc
<div id="container">
			<div id="slider_box">
				<img src="timg.jpg" alt="">
				<img src="backg.jpg" alt="">
				<img src="bak1.jpg" alt="">
				<img src="bak2.jpg" alt="">
			</div>
	   </div>
```
两个div里面放着四张图片
### 动起来
```objc
#container{
				width:400px;
				height:300px;
				overflow:hidden
			}
            #slider_box{
				animation:5s slider ease infinite normal
			}
			#container img{
				width:400px;
				height:300px;
			}
			@keyframes slider{
			 0% {margin-top:0}
			 25% {margin-top:-300px}
			50% {margin-top:-600px}
			 75% {margin-top:-900px}
			 
			}
```


### 甚至还可以添加一段js控制动画的开始和停止

```objc
 <script>
		(function(){
			container.onmouseover=function(e){
			if(e.target.nodeName=='IMG'){
				slider_box.style.animationPlayState='paused'
			}
			}
			slider_box.onmouseout=function(){
				slider_box.style.animationPlayState='running'
			}
		})()
```
炫酷的一B
