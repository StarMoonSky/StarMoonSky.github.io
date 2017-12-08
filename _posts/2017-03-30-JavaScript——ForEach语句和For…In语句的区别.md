---
layout:     post
title:      JavaScript——ForEach语句和For…In语句的区别
subtitle:   不要老是用for循环语句
date:       2017-03-30
author:     CC
header-img: img/post-bg-iWatch.jpg
catalog: true
tags:
    - JS
    - for循环
    - for in
---



## For循环语句

JavaScript中最基本的循环语句，用途广泛。这里有for循环的基本句法：

for (i = 0; i < 10; i++) { 
  // 内容
}
我们这个for循环由三个语句组成：一个语句(i = 0)在整个循环开始之前执行；一个语句(i < 10)定义循环运行长度；还有一个语句(i++)在每轮循环结束后执行。

在这个例子里，整个循环开始之前设i = 0，只要i < 10，循环就不断继续。每轮循环过后，i的值都加一。最后，每轮循环都运行花括弧中的代码。



## ForEach

forEach是一个数组方法，可以用来把一个函数套用在一个数组中的每个元素上，只可用于数组。

一个简单的例子，用console.log方法终端打印出一个数组内所有的元素。用for语句写的话看起来大概是这样的：

const arr = ['cat', 'dog', 'fish'];
for (i = 0; i < arr.length; i++) { 
  console.log(arr[i])
}
// cat
// dog
// fish
很好，成功了。相同的结果，用forEach()如何实现？做法如下：

const arr = ['cat', 'dog', 'fish'];
arr.forEach(element => {
  console.log(element);
});
// cat
// dog
// fish
使用forEach语句时，只要指定一个回调函数就行了。这个回调函数会套用在数组中的每个元素上。

## For…In语句

for...in语句的句法看起来是这样的：

for (variable in object) {  
  // 内容
}
for...in语句用于循环访问对象的可枚举属性。对象的每个属性都会有一个可枚举(Enumerable)值，如果值为真(true)，则该属性为可枚举(Enumerable)。

翻成中文。

记住，一个对象创建出来时，会从它的原型中继承某些方法，比如Object.keys()方法。这些方法都是不可枚举的，而你添加到对象里的属性一般而言是可枚举的。让我们看一个例子，帮助理解。在下面的例子里，我们要把一个对象中所有可枚举属性的值都记录打印出来：

const obj = {  
  a: 1,
  b: 2,
  c: 3,
  d: 4
}
for (let elem in obj) {  
  console.log( obj[elem] )
}
// 1
// 2
// 3
// 4
做得更漂亮些，我们还可以把这些属性的键key与值value成对地打出来：

for (let elem in obj) {
  console.log(`${elem} = ${obj[elem]}`);
}
// a = 1
// b = 2
// c = 3
// d = 4
别忘了，数组本身也是对象。也就是说我们也可以把for...in循环应用到数组上去：

const arr = ['cat', 'dog', 'fish'];
for (let i in arr) {  
  console.log(arr[i])
}
// cat
// dog
// fish
另外，一个字符串中的每个字符都有索引值，所以我们甚至可以把for...in语句用在字符串上。看看这个：

const string = 'hello';
for (let character in string) {  
    console.log(string[character])
}
// h
// e
// l
// l
// o
注意：for...in循环语句是按任意顺序循环的，所以如果需要以特定顺序循环，就不该找它了。




