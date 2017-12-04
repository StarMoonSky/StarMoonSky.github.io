---
layout:     post
title:      python-requests库和beautiful库
subtitle:   爬呀爬
date:       2017-07-10
author:     CC
header-img: img/post-bg-mma-3.jpg
catalog: true
tags:
    - 爬虫
    - http
---


## requests库
安装requests库简单的一b 使用pip install requests 稍等片刻就安装完成

## 基本用法
import requests
 
r = requests.get('http://baidu.com')
print type(r)
print r.status_code
print r.encoding
#print r.text
print r.cookies

以上代码我们请求了baidu的网址，然后打印出了返回结果的类型，状态码，编码方式，Cookies等内容。

如果网站没有在head里charset编码格式,或者用了错误的编码格式  加上这一段代码就ok
r.encoding=r.apparent_encoding 后面的是根据页面中的内容解析出来的编码格式 通常比较准确
### 请求方式

r = requests.post("http://httpbin.org/post")
r = requests.put("http://httpbin.org/put")
r = requests.delete("http://httpbin.org/delete")
r = requests.head("http://httpbin.org/get")
r = requests.options("http://httpbin.org/get")

requests库提供了http所有的基本请求方式
####  基本GET请求
最基本的GET请求可以直接用get方法
```swift
r = requests.get("http://httpbin.org/get")
```

如果想要加参数，可以利用 params 参数
```swift
import requests

payload = {'key1': 'value1', 'key2': 'value2'}
r = requests.get("http://httpbin.org/get", params=payload)
print r.url
```

运行的结果是这样的 	
```swift
http://httpbin.org/get?key2=value2&key1=value1
```
如果想请求JSON文件，可以利用 json() 方法解析

例如自己写一个JSON文件命名为a.json，内容如下

```swift
["foo", "bar", {
  "foo": "bar"
}]
```
利用如下程序请求并解析
```swift
import requests

r = requests.get("a.json")
print r.text
print r.json()
```
运行结果如下，其中一个是直接输出内容，另外一个方法是利用 json() 方法解析,感受一下不同吧
```swift
["foo", "bar", {
 "foo": "bar"
 }]
 [u'foo', u'bar', {u'foo': u'bar'}]
```
如果想添加 headers，可以传 headers 参数
```swift
import requests

payload = {'key1': 'value1', 'key2': 'value2'}
headers = {'content-type': 'application/json'}
r = requests.get("http://httpbin.org/get", params=payload, headers=headers)
print r.url
```
通过headers参数可以增加请求头中的headers信息

#### 基本POST请求

对于 POST 请求来说，我们一般需要为它增加一些参数。那么最基本的传参方法可以利用 data 这个参数。
```swift
import requests

payload = {'key1': 'value1', 'key2': 'value2'}
r = requests.post("http://httpbin.org/post", data=payload)
print r.text
```
运行结果
```swift
{
  "args": {}, 
  "data": "", 
  "files": {}, 
  "form": {
    "key1": "value1", 
    "key2": "value2"
  }, 
  "headers": {
    "Accept": "*/*", 
    "Accept-Encoding": "gzip, deflate", 
    "Content-Length": "23", 
    "Content-Type": "application/x-www-form-urlencoded", 
    "Host": "httpbin.org", 
    "User-Agent": "python-requests/2.9.1"
  }, 
  "json": null, 
  "url": "http://httpbin.org/post"
}
```
可以看到参数传成功了，然后服务器返回了我们传的数据。

有时候我们需要传送的信息不是表单形式的，需要我们传JSON格式的数据过去，所以我们可以用 json.dumps() 方法把表单数据序列化。
```swift
import json
import requests

url = 'http://httpbin.org/post'
payload = {'some': 'data'}
r = requests.post(url, data=json.dumps(payload))
print r.text
```
运行结果
```swift
{
  "args": {}, 
  "data": "{\"some\": \"data\"}", 
  "files": {}, 
  "form": {}, 
  "headers": {
    "Accept": "*/*", 
    "Accept-Encoding": "gzip, deflate", 
    "Content-Length": "16", 
    "Host": "httpbin.org", 
    "User-Agent": "python-requests/2.9.1"
  }, 
  "json": {
    "some": "data"
  },  
  "url": "http://httpbin.org/post"
}
```
通过上述方法，我们可以POST JSON格式的数据

如果想要上传文件，那么直接用 file 参数即可

新建一个 a.txt 的文件，内容写上 Hello World!

```swift
import requests

url = 'http://httpbin.org/post'
files = {'file': open('test.txt', 'rb')}
r = requests.post(url, files=files)
print r.text
```
可以看到运行结果如下
```swift
{
  "args": {}, 
  "data": "", 
  "files": {
    "file": "Hello World!"
  }, 
  "form": {}, 
  "headers": {
    "Accept": "*/*", 
    "Accept-Encoding": "gzip, deflate", 
    "Content-Length": "156", 
    "Content-Type": "multipart/form-data; boundary=7d8eb5ff99a04c11bb3e862ce78d7000", 
    "Host": "httpbin.org", 
    "User-Agent": "python-requests/2.9.1"
  }, 
  "json": null, 
  "url": "http://httpbin.org/post"
}
```
这样我们便成功完成了一个文件的上传。

requests 是支持流式上传的，这允许你发送大的数据流或文件而无需先把它们读入内存。要使用流式上传，仅需为你的请求体提供一个类文件对象即可
```swift
with open('massive-body') as f:
    requests.post('http://some.url/streamed', data=f)
```


####  Cookies

如果一个响应中包含了cookie，那么我们可以利用 cookies 变量来拿到
```swift
import requests

url = 'http://example.com'
r = requests.get(url)
print r.cookies
print r.cookies['example_cookie_name']
```
以上程序仅是样例，可以用 cookies 变量来得到站点的 cookies

另外可以利用 cookies 变量来向服务器发送 cookies 信息

```swift
import requests

url = 'http://httpbin.org/cookies'
cookies = dict(cookies_are='working')
r = requests.get(url, cookies=cookies)
print r.text
```
运行结果

```swift
'{"cookies": {"cookies_are": "working"}}'
```
可以已经成功向服务器发送了 cookies

## 超时配置
可以利用 timeout 变量来配置最大请求时间
```swift
requests.get('http://github.com', timeout=0.001)
```
注：timeout 仅对连接过程有效，与响应体的下载无关。

也就是说，这个时间只限制请求的时间。即使返回的 response 包含很大内容，下载需要一定时间，然而这并没有什么卵用。

## 会话对象
在以上的请求中，每次请求其实都相当于发起了一个新的请求。也就是相当于我们每个请求都用了不同的浏览器单独打开的效果。也就是它并不是指的一个会话，即使请求的是同一个网址。比如
```swift
import requests

requests.get('http://httpbin.org/cookies/set/sessioncookie/123456789')
r = requests.get("http://httpbin.org/cookies")
print(r.text)
```
结果是
```swift
{
  "cookies": {}
}
```
很明显，这不在一个会话中，无法获取 cookies，那么在一些站点中，我们需要保持一个持久的会话怎么办呢？就像用一个浏览器逛淘宝一样，在不同的选项卡之间跳转，这样其实就是建立了一个长久会话。

解决方案如下
```swift
import requests

s = requests.Session()
s.get('http://httpbin.org/cookies/set/sessioncookie/123456789')
r = s.get("http://httpbin.org/cookies")
print(r.text)
```
在这里我们请求了两次，一次是设置 cookies，一次是获得 cookies

运行结果
```swift
{
  "cookies": {
    "sessioncookie": "123456789"
  }
}
```
发现可以成功获取到 cookies 了，这就是建立一个会话到作用。体会一下。

那么既然会话是一个全局的变量，那么我们肯定可以用来全局的配置了。
```swift
import requests

s = requests.Session()
s.headers.update({'x-test': 'true'})
r = s.get('http://httpbin.org/headers', headers={'x-test2': 'true'})
print r.text
```
通过 s.headers.update 方法设置了 headers 的变量。然后我们又在请求中设置了一个 headers，那么会出现什么结果？

很简单，两个变量都传送过去了。

运行结果
```swift
{
  "headers": {
    "Accept": "*/*", 
    "Accept-Encoding": "gzip, deflate", 
    "Host": "httpbin.org", 
    "User-Agent": "python-requests/2.9.1", 
    "X-Test": "true", 
    "X-Test2": "true"
  }
}
```
如果get方法传的headers 同样也是 x-test 呢？
```swift
r = s.get('http://httpbin.org/headers', headers={'x-test': 'true'})
```
嗯，它会覆盖掉全局的配置
```swift
{
  "headers": {
    "Accept": "*/*", 
    "Accept-Encoding": "gzip, deflate", 
    "Host": "httpbin.org", 
    "User-Agent": "python-requests/2.9.1", 
    "X-Test": "true"
  }
}
```
那如果不想要全局配置中的一个变量了呢？很简单，设置为 None 即可
```swift
r = s.get('http://httpbin.org/headers', headers={'x-test': None})
```
运行结果
```swift
{
  "headers": {
    "Accept": "*/*", 
    "Accept-Encoding": "gzip, deflate", 
    "Host": "httpbin.org", 
    "User-Agent": "python-requests/2.9.1"
  }
}
```
以上就是 session 会话的基本用法

## SSL证书验证

现在随处可见 https 开头的网站，Requests可以为HTTPS请求验证SSL证书，就像web浏览器一样。要想检查某个主机的SSL证书，你可以使用 verify 参数

现在 12306 证书不是无效的嘛，来测试一下
```swift
import requests

r = requests.get('https://kyfw.12306.cn/otn/', verify=True)
print r.text
```
结果
```swift
requests.exceptions.SSLError: [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed (_ssl.c:590)
```
果真如此

来试下 github 的
```swift
import requests

r = requests.get('https://github.com', verify=True)
print r.text
```
嗯，正常请求，内容我就不输出了。

如果我们想跳过刚才 12306 的证书验证，把 verify 设置为 False 即可
```swift
import requests

r = requests.get('https://kyfw.12306.cn/otn/', verify=False)
print r.text
```
发现就可以正常请求了。在默认情况下 verify 是 True，所以如果需要的话，需要手动设置下这个变量。

## 代理
如果需要使用代理，你可以通过为任意请求方法提供 proxies 参数来配置单个请求
```swift
import requests

proxies = {
  "https": "http://41.118.132.69:4433"
}
r = requests.post("http://httpbin.org/post", proxies=proxies)
print r.text
```
也可以通过环境变量 HTTP_PROXY 和 HTTPS_PROXY 来配置代理
```swift
export HTTP_PROXY="http://10.10.1.10:3128"
export HTTPS_PROXY="http://10.10.1.10:1080"
```
通过以上方式，可以方便地设置代理。
