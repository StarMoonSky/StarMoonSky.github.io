---
layout:     post
title:      JavaScript独孤九剑[原创]
subtitle:   百日练棍,千日练枪,万日练刀,一生练剑
date:       2017-07-19
author:     程娇阳
header-img: img/post-bg-hacker.jpg
catalog: true
tags:
    - JavaScript
---

>前言:
   剑气纵横三万里,一剑光寒十九洲。
   
   本少侠自幼喜欢文学,尤其武侠小说,很羡慕大侠们舞刀弄剑、飞檐走壁。
# Objectice-C

在上个 Objectice-C 项目中，使用的 HMAC 和 SHA1 进行加密。如下代码：

```objc
+ (NSString *)hmacsha1:(NSString *)text key:(NSString *)secret {
    
    NSData *secretData = [secret dataUsingEncoding:NSUTF8StringEncoding];
    NSData *clearTextData = [text dataUsingEncoding:NSUTF8StringEncoding];
    unsigned char result[20];

```



## swift

最近用 swift 重构项目,用 Swift [重写了](https://stackoverflow.com/questions/26970807/implementing-hmac-and-sha1-encryption-in-swift?rq=1) HMAC 的 SHA1 加密方式。

### 使用

```swift
// 使用HMAC和SHA加密
let hmacResult:String = "myStringToHMAC".hmac(HMACAlgorithm.SHA1, key: "myKey")
```

### 代码

使用下面代码时，需要在 OC 桥接文件`xxx-Bridging-Header`中 `#import <CommonCrypto/CommonHMAC.h>`

```swift
extension String {
    func hmac(algorithm: HMACAlgorithm, key: String) -> String {
        let cKey = key.cStringUsingEncoding(NSUTF8StringEncoding)
        let cData = self.cStringUsingEncoding(NSUTF8StringEncoding)
        var result = [CUnsignedChar](count: Int(algorithm.digestLength()), repeatedValue: 0)
        CCHmac(algorithm.toCCHmacAlgorithm(), cKey!, strlen(cKey!), cData!, strlen(cData!), &result)
        var hmacData:NSData = NSData(bytes: result, length: (Int(algorithm.digestLength())))

    }

    func digestLength() -> Int {
        var result: CInt = 0
        switch self {
        case .MD5:

        return Int(result)
    }
}


```

