---
layout:     post
title:      JavaScript&&Python=>outils
subtitle:   汇总工作中遇到的js以及python知识
date:       2017-09-11
author:     CC
header-img: img/post-bg-ios10.jpg
catalog: true
tags:
    - Pyhon
    - HTTP
---

#### 把某几位手机号换成星号
###替换手机号中间4位
```swift
function shelterTelNum(num){
return num.toString().replace(/(\d{3})\d{4}(\d{4})/, '$1****$2');
}
```
###替换手机号前7位
```swift
function shelterTelNum(num){
return num.toString().replace(/\d{7}(\d{4})/, '*******$1');
}
```


#### urllib2 getKeyName

```swift
var keyCodeMap = {

    8: 'Backspace',

    9: 'Tab',

    13: 'Enter',

    16: 'Shift',

    17: 'Ctrl',

    18: 'Alt',

    19: 'Pause',

    20: 'Caps Lock',

    27: 'Escape',

    32: 'Space',

    33: 'Page Up',

    34: 'Page Down',

    35: 'End',

    36: 'Home',

    37: 'Left',

    38: 'Up',

    39: 'Right',

    40: 'Down',

    42: 'Print Screen',

    45: 'Insert',

    46: 'Delete',

    48: '0',

    49: '1',

    50: '2',

    51: '3',

    52: '4',

    53: '5',

    54: '6',

    55: '7',

    56: '8',

    57: '9',

    65: 'A',

    66: 'B',

    67: 'C',

    68: 'D',

    69: 'E',

    70: 'F',

    71: 'G',

    72: 'H',

    73: 'I',

    74: 'J',

    75: 'K',

    76: 'L',

    77: 'M',

    78: 'N',

    79: 'O',

    80: 'P',

    81: 'Q',

    82: 'R',

    83: 'S',

    84: 'T',

    85: 'U',

    86: 'V',

    87: 'W',

    88: 'X',

    89: 'Y',

    90: 'Z',

    91: 'Windows',

    93: 'Right Click',

    96: 'Numpad 0',

    97: 'Numpad 1',

    98: 'Numpad 2',

    99: 'Numpad 3',

    100: 'Numpad 4',

    101: 'Numpad 5',

    102: 'Numpad 6',

    103: 'Numpad 7',

    104: 'Numpad 8',

    105: 'Numpad 9',

    106: 'Numpad *',

    107: 'Numpad +',

    109: 'Numpad -',

    110: 'Numpad .',

    111: 'Numpad /',

    112: 'F1',

    113: 'F2',

    114: 'F3',

    115: 'F4',

    116: 'F5',

    117: 'F6',

    118: 'F7',

    119: 'F8',

    120: 'F9',

    121: 'F10',

    122: 'F11',

    123: 'F12',

    144: 'Num Lock',

    145: 'Scroll Lock',

    182: 'My Computer',

    183: 'My Calculator',

    186: ';',

    187: '=',

    188: ',',

    189: '-',

    190: '.',

    191: '/',

    192: '`',

    219: '[',

    220: '\\',

    221: ']',

    222: '\''
};
/**
 * @desc 根据keycode获得键名
 * @param  {Number} keycode 
 * @return {String}
 */
function getKeyName(keycode) {

    if (keyCodeMap[keycode]) {

        return
        keyCodeMap[keycode];
    } else {
        console.log('Unknow Key(Key Code:' + keycode + ')');

        return

        '';
    }
}
;
```

### 现金额转大写digitUppercase



```swift
/**
 * 
 * @desc   现金额转大写
 * @param  {Number} n 
 * @return {String}
 */
function digitUppercase(n) {

    var fraction = ['角', '分'];

    var digit = [

    '零', '壹', '贰', '叁', '肆',

    '伍', '陆', '柒', '捌', '玖'];

    var unit = [['元', '万', '亿'], ['', '拾', '佰', '仟']];

    var head = n < 0 ? '欠': '';
    n = Math.abs(n);

    var s = '';

    for (var i = 0; i < fraction.length; i++) {
        s += (digit[Math.floor(n * 10 * Math.pow(10, i)) % 10] + fraction[i]).replace(/零./, '');
    }
    s = s || '整';
    n = Math.floor(n);

    for (var i = 0; i < unit[0].length && n > 0; i++) {

        var p = '';

        for (var j = 0; j < unit[1].length && n > 0; j++) {
            p = digit[n % 10] + unit[1][j] + p;
            n = Math.floor(n / 10);
        }
        s = p.replace(/(零.)*零$/, '').replace(/^$/, '零') + unit[0][i] + s;
    }

    return head + s.replace(/(零.)*零元/, '元').replace(/(零.)+/g, '零').replace(/^整$/, '零元整');
};
```


### 格式化现在距${endTime}的剩余时间
```swift
/**
 * 
 * @desc   格式化现在距${endTime}的剩余时间
 * @param  {Date} endTime  
 * @return {String}
 */
function formatRemainTime(endTime) {

    var startDate = new

    Date();
    //开始时间
    var endDate = new

    Date(endTime);
    //结束时间
    var t = endDate.getTime() - startDate.getTime();
    //时间差
    var d = 0,
    h = 0,
    m = 0,
    s = 0;

    if (t >= 0) {
        d = Math.floor(t / 1000 / 3600 / 24);
        h = Math.floor(t / 1000 / 60 / 60 % 24);
        m = Math.floor(t / 1000 / 60 % 60);
        s = Math.floor(t / 1000 % 60);
    }

    return d + "天 " + h + "小时 " + m + "分钟 " + s + "秒";
}


```


#### url参数转对象 parseQueryString


```swift
/**
 * 
 * @desc   url参数转对象
 * @param  {String} url  default: window.location.href
 * @return {Object} 
 */
function parseQueryString(url) {
    url = url == null ? window.location.href: url

    var search = url.substring(url.lastIndexOf('?') + 1)

    if (!search) {

        return {}
    }

    return JSON.parse('{"' + decodeURIComponent(search).replace(/"/g, '\\"').replace(/&/g, '","').replace(/=/g, '":"') + '"}')
}

```

#### 判断是否为手机号 isPhoneNum



```swift
/**
 * 
 * @desc   判断是否为手机号
 * @param  {String|Number} str 
 * @return {Boolean} 
 */
function isPhoneNum(str) {

    return

    /^(0|86|17951)?(13[0-9]|15[012356789]|17[678]|18[0-9]|14[57])[0-9]{8}$/.test(str)
}
```

#### 16进制随机颜色
```swift
function getColor(){
                          
     var colorValue="0,1,2,3,4,5,6,7,8,9,a,b,c,d,e,f";
        var colorArray = colorValue.split(",");
            var color="#";
                for(var i=0;i<6;i++){
               color+=colorArray[Math.floor(Math.random()*16)];
                           }
                           return color;
                      }
```

#### 未完待续
待续
```swift
lorem
```



