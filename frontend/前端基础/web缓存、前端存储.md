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



2. localStorage

3. sessionStorage