---
layout:     post
title:dns劫持、http劫持和jsp劫持
subtitle:   
date:       2017-10-04
author:     CY
header-img: img/home-bg-art.jpg
catalog: true
tags:
    - DNS
    - HTTP
    - JSP
---



先说明一下，ISP即为Internet Service Provider, 网络运营商，就是家里宽带使用的服务商，电信，移动，联通等
##1. 动机

我们平时上网的时候，对网页上有广告已经习以为常，但是这里面很多广告也并不是网站自己投放的，而且你的ISP劫持了你的流量对你投放的

ISP为什么这么做？在一个网站投放广告，只有这个网站有游览量才会有对广告有曝光。但是在ISP这里投放广告，只要是通过他家ISP上网的，都有几率看到广告，无论你游览什么网站（除了加密网站之外）

##2. 如何鉴别已经被ISP劫持

如果你每次游览网站都会出现排版类似的广告，那八成你已经是被劫持了，尤其是游览那些原本没有广告的页面还发现广告。那么恭喜你，这时候不是运营商直接劫持你，就是运营商提供的DNS劫持了你， 下面几个图告诉你被劫持的时候是什么样子的




上面三个图可以看出，广告的套路基本一致，而且这些广告都是出现在了原本不应该有广告的页面上，和网站本身的风格也不太统一

##2.1 区分DNS劫持和HTTP劫持

DNS劫持就比较好解决了，而且大部分人都不建议使用ISP提供的DNS,用阿里的223.5.5.5或者114.114.114.114都可以解决DNS劫持

如果修改DNS还不能消除广告，那可以尝试使用手机4G网络打开相同的页面，如果广告消失，那基本就是ISP的问题，如果还有广告但是套路不一样，那么恭喜你，你无论是ISP还是手机运营商都在劫持你的流量

##3. 解决办法

解决ISP劫持最有效的办法是给工信部直接投诉，投诉地址是: http://www.chinatcc.gov.cn:8080/cms/shensus/


到时候你的运营商会给你打回访电话，告诉你收到工信部的投诉，然后询问你的情况，你就直接和他说你好几个朋友都被运营商劫持了，都是给工信部直接投诉，然后就恢复了。如果他们说不是他们劫持的流量就让他们自己派人来排查，反正问题不解决就一直在工信部投诉

##4.最后

运营商流量劫持在我看来是一件非常不道德的事情，首先，这种问题大部分人因为不懂技术不知道矛头应该指向谁。其次，这种事情的危害可大可小，如果你只是觉得多看了几个广告并没有什么问题，那么我可以告诉你，今天他给你看的广告，明天他载入一段恶意代码记录你网页上的操作，就可以拦截到你在网页上输入的所有内容，包括密码。最后，一定要记住http和https的区别



切记不要在非https的网络连接下输入敏感数据，用户名和密码之类的，就算是https, 也要看清楚网站域名是不是你要访问的网站

其他有关链接

https://www.zhihu.com/question/41545611

https://www.zhihu.com/question/38861118 

https://www.zhihu.com/question/29340133

测试连接：

任意非https加密的国内网站

www.kfc.com.cn 
http://static.owspace.com/wap/294382.html?from=timeline&isappinstalled=0 
http://m.blog.csdn.net/isentech/article/details/77680089?from=timeline&isappinstalled=0
## 优先级

新的 GCD 引入了 QoS (Quality of Service) 的概念。

先看看下面的代码：

```swift
DispatchQueue.global(qos: .userInitiated).async {

}

```


QoS 对应的就是 `Global Queue` 中的优先级。 其优先级由最低的 `background` 到最高的 `userInteractive` 共五个，还有一个未定义的 `unspecified`。

```swift
public static let background: DispatchQoS

public static let utility: DispatchQoS

public static let `default`: DispatchQoS

public static let userInitiated: DispatchQoS

public static let userInteractive: DispatchQoS

public static let unspecified: DispatchQoS
```

## 自定义 Queue

除了直接使用 `DispatchQueue.global().async` 这种封装好的代码外，还可以通过`DispatchWorkItem` 自定义队列的优先级，特性：

```swift
let queue = DispatchQueue(label: "swift_queue")
let dispatchworkItem = DispatchWorkItem(qos: .userInitiated, flags: .inheritQoS) {
    
}
queue.async(execute: dispatchworkItem)

```
## GCD定时器

Swift 中 `dispatch_time`的用法改成了：

```swift
let delay = DispatchTime.now() + .seconds(60)
DispatchQueue.main.asyncAfter(deadline: delay) { 
    
}
```

相较与OC来说更易读了：

```objc
let dispatch_time = dispatch_time(DISPATCH_TIME_NOW, Int64(60 * NSEC_PER_SEC))
```

- 参考 [GCD 在 Swift 3 中的玩儿法](https://www.swiftcafe.io/2016/10/16/swift-gcd/)
