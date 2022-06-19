<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [跨域、cors、options请求](#%E8%B7%A8%E5%9F%9Fcorsoptions%E8%AF%B7%E6%B1%82)
  - [前端通过post、src请求时，会有两条请求记录，一条请求的请求方法为OPTIONS，再有一条的请求方法才是post或者get。](#%E5%89%8D%E7%AB%AF%E9%80%9A%E8%BF%87postsrc%E8%AF%B7%E6%B1%82%E6%97%B6%E4%BC%9A%E6%9C%89%E4%B8%A4%E6%9D%A1%E8%AF%B7%E6%B1%82%E8%AE%B0%E5%BD%95%E4%B8%80%E6%9D%A1%E8%AF%B7%E6%B1%82%E7%9A%84%E8%AF%B7%E6%B1%82%E6%96%B9%E6%B3%95%E4%B8%BAoptions%E5%86%8D%E6%9C%89%E4%B8%80%E6%9D%A1%E7%9A%84%E8%AF%B7%E6%B1%82%E6%96%B9%E6%B3%95%E6%89%8D%E6%98%AFpost%E6%88%96%E8%80%85get)
  - [CORS-跨域资源共享](#cors-%E8%B7%A8%E5%9F%9F%E8%B5%84%E6%BA%90%E5%85%B1%E4%BA%AB)
  - [同源策略](#%E5%90%8C%E6%BA%90%E7%AD%96%E7%95%A5)
  - [CORS和同源策略](#cors%E5%92%8C%E5%90%8C%E6%BA%90%E7%AD%96%E7%95%A5)
  - [预检请求(Preflighted Request)](#%E9%A2%84%E6%A3%80%E8%AF%B7%E6%B1%82preflighted-request)
  - [简单请求和和非简单请求](#%E7%AE%80%E5%8D%95%E8%AF%B7%E6%B1%82%E5%92%8C%E5%92%8C%E9%9D%9E%E7%AE%80%E5%8D%95%E8%AF%B7%E6%B1%82)
    - [怎么区分简单请求和非简单请求？](#%E6%80%8E%E4%B9%88%E5%8C%BA%E5%88%86%E7%AE%80%E5%8D%95%E8%AF%B7%E6%B1%82%E5%92%8C%E9%9D%9E%E7%AE%80%E5%8D%95%E8%AF%B7%E6%B1%82)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 跨域、cors、options请求

### 前端通过post、src请求时，会有两条请求记录，一条请求的请求方法为OPTIONS，再有一条的请求方法才是post或者get。

### CORS-跨域资源共享

CORS是一种网络浏览器的技术规范，它为web服务器定义了一种方式，允许网页从不同的域访问其资源。但是这种策略又是同源策略所禁止的。CORS规范定义了一种浏览器和服务器交互的方式来确定是否允许跨域请求。

> CORS是一种浏览器的技术规范，同源策略是一种协议、约定，具体的表现为cookie同源策略、DOM同源策略和XmlHttpRequest同源策略。

CORS的使用也相对比较简单，需要前端(浏览器)和服务器同时做一些处理.

1. 前端(浏览器)端的支持

CORS的使用，需要浏览器的支持，代码上基本没有什么特殊的地方。好的是现在的浏览器已基本上都支持了CORS，如果是IE的话，需要版本不低于IE10.不过好消息是IE已经在2022年的6月15日退出了历史舞台，虽然短时间内还会有IE设备存在，但是已经被边缘化，是逐消失的节奏，接下来的前端应用，基本上可以不用考虑IE了。

2. 服务器端

服务端需要做一些配置，以便可以让浏览器端通过异步请求可以得到有效的回应，否则访问会被拒绝。

> 跨域，需要解决问题的主要在于服务器端。客户端，一般情况下不需要做什么，浏览器支持了就可以了。也有部分需要在客户端做一些简单的处理，如通过JSONP方式解决跨域请求时，就需要在请求的时候提那家jsonp字段，通过在浏览器端添加script标签，然后通过src的方式向服务器请求资源。

> 跨域问题，所有标签的src属性，是没有同源策略的限制的，如img、script等标签的src属性没有同源策略的限制。这个原理，就是jsonp的根本上的原理所在。

### 同源策略


### CORS和同源策略

同源策略是一种约定、协议，对网络的安全做了一些限定，那么在一些特定的场景下，又需要跨过这种约定，那么怎么办呢？

就需要一些特殊的办法去跨过这个门槛。跨过这个门槛的方法有多种，如JSONP、CORS、Access-Conrol-Allow-Origin白名单(其实是cors的一种具体实现)、websocket、代理服务器等。

看到这里应该就明白了，其实CORS是突破同源策略的一种实现。

### 预检请求(Preflighted Request)

预检请求，是CORS中的一种透明服务器验证机制。预检请求首先需要向另外一个域名的资源发送一个HTTP OPTIONS请求头，其目的就是为了判断实际发送的请求是否合法。

需要进行预检请求的2种情况：

1. 简单请求：比如使用Content-Type为application/xml或text/xml的post请求；

2. 请求中设置自定义头，比如X-JSON、X-MENGXIANHUI等。

HTTP请求方法，最常用的是GET和POST，但是除此之外，还有OPTIONS、HEAD、PUT、DELETE、TRACE和CONNECT等方法。

OPTIONS方法是用于请求获得由Request-URI标识的资源在请求/响应的通信过程中可以使用的功能选项。通过这个方法，客户端可以在具体资源请求之前，绝对对该资源采取何种必要措施，或者了解服务器性能。

OPTIONS请求方法的响应不能被缓存。

### 简单请求和和非简单请求

浏览器将CORS请求分为两类：简单请求(simple request)和非简单请求(not-simple request)。简单请求浏览器不会预检，非简单请求，浏览器会进行预检。

#### 怎么区分简单请求和非简单请求？

同时满足下面的3个条件，就是简单请求，否则就是非简单请求。

1. 请求方式只能是：GET、POST和HEAD；

2. HTTP请求头限制下面几个字段：Accept、Accept-language、Content-language、Content-Type、Last-Event-ID；

3. Content-TypeContent-Type只能是如下取值：application/x-www-form-urlencoded、multipart/form-data、text/plain.

