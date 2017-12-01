---
layout:     post
title:      Browser对象和Bom汇总
subtitle:   收集工作中用过的bom对象
date:       2017-07-24
author:     CCC
header-img: img/post-bg-ios10.jpg
catalog: true
tags:
    - http
    - 前端
---


## 前言

今天用了location获取用户请求的协议,如果是http的话,劫持之

## 收集用过的Browser的对象

window.closed 返回true或false;
window.close() 关闭当前页面;
window.open() 打开一个新的浏览器窗口或查找一个已命名的窗口;
document.location.host 设置或返回主机名和当前 URL 的端口号;
document.location.href 设置或返回完整的 URL;
document.location.protocol 	设置或返回当前 URL 的协议;
document.location.search 设置或返回从问号 (?) 开始的 URL（查询部分）;
document.location.port 设置或返回当前 URL 的端口号;
document.location.pathname 设置或返回当前 URL 的路径部分

End
