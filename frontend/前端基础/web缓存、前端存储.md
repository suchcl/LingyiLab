<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. 客户端存储的理解](#1-%E5%AE%A2%E6%88%B7%E7%AB%AF%E5%AD%98%E5%82%A8%E7%9A%84%E7%90%86%E8%A7%A3)
- [2. 前端缓存](#2-%E5%89%8D%E7%AB%AF%E7%BC%93%E5%AD%98)
- [3. 前端常用的3种缓存技术：Cookie、localStorage、sessionStoage](#3-%E5%89%8D%E7%AB%AF%E5%B8%B8%E7%94%A8%E7%9A%843%E7%A7%8D%E7%BC%93%E5%AD%98%E6%8A%80%E6%9C%AFcookielocalstoragesessionstoage)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. 客户端存储的理解

web应用允许使用浏览器提供的API将数据存储在客户端硬件设备上；

客户端存储遵循同源策略，不同站点的页面之间的数据不能共享；

在同一个站点之间的不同页面之间，数据可以共享；

数据在客户端硬件设备上的存储的有效期可以是临时的，比如关闭浏览器就销毁，也可以是永久的，可以在客户端应景设备上存储任意指定时间，只要没有手动销毁；

在使用客户端存储的时候需要注意安全问题，如账号、银行卡号等敏感信息；

### 2. 前端缓存

前端缓存，把web应用中的数据存储到客户端磁盘上，就是前端的缓存技术。

在前端应用中，常用的前端缓存技术主要有：

1. 大文件离线存储，如大型游戏应用等

2. 本地数据库，如sqlite等；

3. 前端常用的3种缓存技术：Cookie、localStorage、sessionStorage

### 3. 前端常用的3种缓存技术：Cookie、localStorage、sessionStoage

1. Cookie

Cookie是由服务器端生成的一些文本信息，然后将这些信息发送给User-Agent(一般情况下就是浏览器)，服务器告诉浏览器要设置一下Cookie，浏览器就会将Cookie以key/value键值对的形式存储在客户端某个目录下的文件内，下次发起Http请求的时候，请求会将同一网站下的cookie发送给服务器，就是将cookie添加在请求头部(需要浏览器没有禁用cookie).不同的Cookie设置会有不同的结果。

本质上，Cookie就是一个小型的文本文件，浏览器对Cookie的大小是有严格限制的。

在设置Cookie的时候，value是一个字符串，这个字符串是有格式要求的。

> Chrome浏览器关于Cookie的设置，有允许所有Cookie、在无痕模式下阻止第三方Cookie、阻止第三方Cookie、阻止所有Cookie。

**为什么要有Cookie呢？**

web应用是通过http协议来传输数据的，但是Http协议是无状态的协议，一旦数据交换完成，客户端和服务器之间的链接就会关闭，当再次交换数据的时候需要建立新的链接。这时就会有一个问题出现：服务器没有办法从链接上跟踪和客户端之间的会话。

我们在使用一些web产品的时候，经常会有记住账号和密码的功能，下次再次登录的时候，就不需要再次登录了，不用输入账号和密码了，在产品的使用上，给我们带来了一定的便利(当然了，也可能会带来一定的安全风险，如果没有处理好)。这里就是利用的cookie技术。

**Cookie的特点**

- 有时效特性

Cooie有很多特性，比如expires时效、域名domain、path路径、secure安全、HttpOnly，在设置cookie的时候，都可以设置这些属性，如果不设置，就会使用这些属性的默认值。

Cookie有临时性的，也有永久性的。如果在设置cookie的时候，不设置时效expires属性，那么这个cookie就是一个临时属性，浏览器关闭，cookie就销毁、失效。

- 有同源策略的限制

只有在同源策略下的cookie，才能读取；由于同源策略的安全机制的限制，不能获取非同源下的cookie；

- 大小限制

Cookie有数量和大小的限制。在不同的浏览器下，数量的限制不同，但是大小的限制，基本上都是4k。

|          | IE6            | IE7/8          | Opera          | Firefox        | safari       | Chrome         |
| -------- | -------------- | -------------- | -------------- | -------------- | ------------ | -------------- |
| 个数限制 | 每个域名下20个 | 每个域名下50个 | 每个域名下30个 | 每个域名下50个 | 没有数量限制 | 每个域名下53个 |
| 大小限制 | 4095字节       | 4095字节       | 4096字节       | 4097字节       | 4097字节     | 4097字节       |

IE已经退出了历史舞台了，所以现在我们可以不在记忆各种和IE相关的数据了，只要大概的记住Opera是个每个域名下30个的限制，其他的浏览器不超过50个就可以了。

大小的限制，这个基本是比较统一，可以统一的记4096字节。

- 安全性

Cookie存储在本地，可以被更改，安全性不高，所以敏感程度高的数据，不建议存储到Cookie中，如账号、银行卡号、证件号码之类的。

- Cookie的使用

Cookie一般是web应用的服务端开发人员设置的，前端开发人员很少使用，但是也有的场景会用到，就比如前面介绍到的在本地临时缓存一些不敏感的信息。

js中没有原生的API可以直接获取和设置cookie，但是我们可以去简单的封装一下，基本可以通用：

```js
    /**
     * 设置cookie
     * @param {string} name cookie名
     * @param {string} value cookie值
     * @param {number} date 时长，天
     */
    setCookie(name, value, day) {
        if (day !== 0) {
            var expires = day * 24 * 60 * 60 * 1000;
            var date = new Date(+new Date() + expires);
            document.cookie = `${name} = ${encodeURI(value)};expires=${date.toString()}`;
        } else {
            document.cookie = `${name}=${encodeURI(value)}`
        }
    },
    /**
     * 获取cookie
     * @param {string} name cookie名
     * @returns {string}
     */
    getCookie(name) {
        var strCookie = document.cookie;
        var arrCookie = strCookie.split('; ');
        for (var i = 0; i < arrCookie.length; i++) {
            var arr = arrCookie[i].split('=');
            if (name === arr[0]) {
                return arr[1]
            }
        }
        return '';
    },
    /**
     * 删除cookie
     * @param {string} name cookie名
     */
    delCookie(name) {
        // var expires = new Date(+new Date() - 24 * 60 * 60 * 1000);
        var expires = new Date('1970-01-01');
        var cval = this.getCookie(name);
        if (cval !== '') {
            document.cookie = `${name} = ${encodeURI(cval)};expires=${expires.toString()}`;
        }
    }
```

删除cookie，js是没有给提供删除cookie的api的。通用的删除cookie的做法是，给cookie设置一个早于当前时间的过期时间，这样，这个cookie就无效了，也就是相当于是删除了指定名称的cookie了。

因为js中的Date对象记录的是自1970年1月1日起经过的毫秒数，所以删除cookie时设置过期时间时有的就直接设置为了1970年1月1日了，如new Date('1970-01-01')，也可以设置一个早于当前时间的一个时间戳，都是可以的。

**httpOnly**

在Cookie的众多属性中，来重点关注一下httpOnly，这个属性指定cookie能否被客户端js去访问。

默认请看下，cookie不会携带httpOnly属性，所以在默认情况下，客户端js是可以访问cookie的，可访问cookie，就是表示js可以读取、删除cookie。如果服务端在设置cookie的时候，设置了httpOnly属性，那么客户端就没有办法去操作这些cookie了，只能由服务端去修改。

2. localStorage

本地存储,是永久保存的，不会随着浏览器的关闭而销毁；

数据可以手动删除；

localStorage受同源策略的限制，不同源之间的localStorage数据是不能相互访问的；

localStorage受浏览器厂商的限制，在chrome浏览器下存储的数据，在edge等其他浏览器中是不能访问的；

> 同源策略：协议、端口、域名

3. sessionStorage

会话级别，浏览器关闭，数据会自动销毁、删除；

sessionStoage存储的数据，在浏览器或者标签关闭时，数据会自动销毁。

在同一个标签页内前进或者后退操作时，数据不会丢失；

sessionStoage在localStorage同源策略限制的基础上，还有一些更加严格的要求和限制：

sessionStoage还在限制在窗口中(窗口是最顶级窗口)：

    - 即在同一个窗口或者标签的不同页面之间，可以共享sessionStorage的数据；

    - 如果是多个iframe，那么它们之间也是共享sessionStorage数据的；

但是在不同的窗口和标签中，不能共享sessionStorage中的数据，即使这些窗口或者标签中是来自同一个页面；

4. localStorage和sessionStorage的关系

localStorage和sessionStorge都是window对象的属性，表示同一个Storage对象。因为localStorage和sessionStorage都是表示的Storage对象，所以他们拥有共同的方法，只是使用的场景不同而已。

localStorage:本地存储

sessionStoage: 会话存储

共同的方法：

```js
// 数据存储
setItem(key,value)

// 数据读取
getItem(key)

// 数据删除
removeItem(key)

// 删除所有的缓存数据
clear() // 注意这里不需要参数，删除所有的缓存数据

// 获取指定位置的键名
key(pos:number)
```

还有一个属性：

```js
// 返回数据项的数量，整数
length
```

### 4. cookie、localStorage和sessionStorage的区别

1. 存储大小

cookie最小，为4k的限制；

localStorage和sessionStorage大概在5M左右；

2. 时效

localStorage:永久存储，浏览器关闭后数据不会被自动清除，本身没有过期时间，但是可以手动删除；

sessionStorage:浏览器关闭，数据自动销毁；

Cookie:可以设置过期时间，在过期时间之前一直有效，即使关闭浏览器数据也不会销毁；

3. 与服务器之间的交互方式

cookie的数据会随着http请求自动发送到服务端，服务器端也可以写cookie到浏览器端；

storage(localStorage和sessionStorage)不会随着http请求自动发送数据到服务器端，只是将数据保存到本地；

4. 作用域

cookie:

    - 同源策略限制：不同源的文档之间不能相互访问和操作cookie

    - 浏览器厂商的限制：不同浏览器下设置的cookie，在其他浏览器是不能访问和操作

localStorage:

    - 同源策略的限制；

    - 同源的文档之间可以相互访问和修改数据；

    - 受浏览器厂商的限制：如在chrome浏览器存储的数据，在edge等其他浏览器上是不能够访问

sessionStoage:

    - 在localStorage同源策略的基础上，有更加严格的限制；

    - 被限制在窗口中，同一个窗口或标签页的不同页面之间共享sessionStorage

    - 不同窗口或标签页之间不能共享sessionStorage，即便是同一个文档

    - 这里说的窗口，是指顶级窗口，如果页面里面有多个iframe，那么这多个iframe之间是共享sessionStorage的