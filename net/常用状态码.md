<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [常用状态码](#%E5%B8%B8%E7%94%A8%E7%8A%B6%E6%80%81%E7%A0%81)
  - [16种常用的状态码](#16%E7%A7%8D%E5%B8%B8%E7%94%A8%E7%9A%84%E7%8A%B6%E6%80%81%E7%A0%81)
  - [其他不太常用的状态码](#%E5%85%B6%E4%BB%96%E4%B8%8D%E5%A4%AA%E5%B8%B8%E7%94%A8%E7%9A%84%E7%8A%B6%E6%80%81%E7%A0%81)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 常用状态码

HTTP状态码用来标识客户端和服务端交互的结果，标记服务端信息处理的是否正常、通知显示的处理结果提示信息，如果正确的处理了客户端请求信息，可能返回一个success，如果处理信息异常，则返回异常信息，定位异常。

![HTTP状态码](./images/i3.png)

状态码由3位数字组成入200、301等，数字的第一位表示了响应的类别，后面2位没有类别。HTTP状态码，可以分为以下5种类型。

**5种HTTP状态码类别**

| 状态码 | 类别                           | 描述                   |
| ------ | ------------------------------ | ---------------------- |
| 1xx    | Informational：信息状态码      | 接受请求正在处理       |
| 2xx    | Success：成功状态码            | 请求正常处理完成       |
| 3xx    | Redirection：重定向状态码      | 需要附加操作已完成请求 |
| 4xx    | Client Error：客户端错误状态码 | 客户端无法处理请求     |
| 5xx    | Server Error：服务端错误状态码 | 服务端处理请求出错     |

HTTP状态码总数大概有60多种，但是常用的大概是16种：

#### 16种常用的状态码

| 状态码 | 状态码英文名称        | 中文描述                                                     |
| ------ | --------------------- | ------------------------------------------------------------ |
| 200    | OK                    | 请求成功。常用于HTTP请求入get、post                          |
| 204    | No Content            | 无内容。服务器成功处理，但是没有内容返回。在没有更新网页的情况下，可以保证当前文档的正常显示 |
| 206    | Partial Content       | 对资源某一部分的请求，服务器成功处理了部分get请求，响应报文中包含由Content-Range指定范围的实体内容 |
|        |                       |                                                              |
| 301    | Moved Permanently     | 永久重定向。请求的资源已经被永久的重定向到新的URI，返回的信息会包含新的URI，浏览器会自动重定向到新的URI。今后任何新的请求都会使用新的URI替代 |
| 302    | Found                 | 临时性重定向。与301类似，但是资源只是被临时性移动，客户端仍然可以继续使用原来的URI |
| 303    | See other             | 查看其他地址，与302类似，使用get请求查看                     |
| 304    | Not Modified          | 所请求的资源没有修改。服务器返回该状态码时，不会返回任何的资源。客户端会缓存访问过的资源，通过提供一个头信息指出客户端希望只返回在指定日期之后修改过的资源。 |
| 307    | Temporary Redirect    | 临时重定向。与302类似，使用get请求重定向，会按照浏览器标准，不会从post变成get |
|        |                       |                                                              |
| 400    | Bad Request           | 客户端请求报文中存在语法错误，服务端无法理解。浏览器会像200 OK一样对待该状态码 |
| 401    | Unauthorized          | 请求要求用户的身份认证。通过HTTP认证(BASIC认证、DIGEST认证)的认证信息，若之前已经进行过一次请求，则表示用户认证失败 |
| 402    | Payment Required      | 保留，将来可能会使用                                         |
| 403    | Forbidden             | 服务端理解客户端的请求，但是拒绝处理                         |
| 404    | Not Found             | 服务端没有办法根据客户端的请求找到资源(网页).通过此代码，网站设计人员可以设置个性化的页面，也可以在服务端拒绝请求时做一些处理措施 |
|        |                       |                                                              |
| 500    | Internal Server Error | 服务器内部错误，没有办法完成请求。可能是web应用存在bug或者其他的一些临时故障 |
| 501    | Not Implemented       | 服务器不支持请求的功能，无法完成请求                         |
| 503    | Service unavailable   | 由于超载火系统维护，服务器暂时无法处理客户端的请求。延时的长度可包含在服务器的Retry-After头信息中 |



#### 其他不太常用的状态码

| 状态码 | 状态英文名称                    | 中文描述                                                     |
| ------ | ------------------------------- | ------------------------------------------------------------ |
| 201    | Created                         | 已创建，成功请求并创建了资源                                 |
| 202    | Accepted                        | 已接受。已接受请求，但是还没有处理完成                       |
| 203    | Non-Authoritative Information   | 非授权信息。请求成功，但返回的meta信息不在原始的服务器，而是一个副本 |
| 205    | Reset Content                   | 重置内容。服务器处理成功，客户端应该重置视图，可通过该状态码清除浏览器的表单域 |
| 300    | Multiple Choices                | 多种选择。请求的资源可包括多个位置，相应可返回一个资源特征与地址的列表用于客户端选择 |
| 305    | Use Proxy                       | 使用代理。所请求的资源必须通过代理访问                       |
| 306    | Unused                          | 已经被废弃的HTTP状态码                                       |
| 402    | Payment Required                | 保留，将来可能会使用                                         |
| 405    | Method Not Allowed              | 客户端请求中的方法被禁止                                     |
| 406    | Not Acceptable                  | 服务器无法根据客户端请求的内容特性完成请求                   |
| 407    | Proxy Authentication Required   | 请求要求代理的身份认证，与401类似，但请求者应当使用代理进行授权 |
| 408    | Request Time-out                | 服务器等待客户端发送的请求时长过长，超时                     |
| 409    | Conflict                        | 服务端完成客户端的PUT请求时可能返回该状态码，服务器处理请求时发生了冲突 |
| 410    | Gone                            | 客户端请求的资源已经不存在。410不同于404，如果资源以前有现在永久删除了可以用410，网站开发人员可以通过301代码指定新的资源的位置 |
| 411    | Length Required                 | 服务器无法处理客户端发送的不带Content-Length的请求信息       |
| 412    | Precondition Failed             | 客户端请求信息的先决条件错误                                 |
| 413    | Request Entity Too Large        | 请求体过大，导致服务器无法处理，并因此拒绝请求。             |
| 414    | Request-URI Too Large           | 请求的URI(请求地址，网址)过长，服务器无法处理                |
| 415    | Unsupported Media  Type         | 服务器无法处理请求附带的媒体格式                             |
| 416    | Requested range not satisfiable | 客户端请求的范围无效                                         |
| 417    | Expectation Failed              | 服务器无法满足Expect的请求头信息                             |
| 501    | Not Implemented                 | 服务器不支持请求的功能，无法完成请求                         |
| 502    | Bad Gateway                     | 充当网关或代理的服务器，从远端服务器获取了一个无效的请求     |
| 504    | Gateway Time-out                | 充当网关或代理的服务器，未及时从远端服务器获取请求           |
| 505    | HTTP Version Not supported      | 服务求不支持请求的HTTP协议的版本，无法完成处理               |

