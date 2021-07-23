### egg.js作为服务端项目，怎么设置可跨域

受SOP（同源策略）安全策略的影响，js不允许向非同源的域发起请求，那么在eggjs作为服务端的项目中，怎么设置允许客户端的跨域请求呢？

在egg项目中，我们可以通过cors标准来实现资源共享，客服同源策略的影响。

简单步骤如下：

先安装egg-cors包

```bash
npm install egg-cors --save
```

做一些简单配置：

```javascript
// config/plugin.js配置
module.exports = {
    // 跨域配置 
    cors: {
        enable: true,
        package: "egg-cors"
    }
};

// config/config.default.js 添加如下配置
    /**
    * 设置跨域
    * 在一些简单场景下，该设置也可以生路
    */
    config.security = {
        csrf: {
        enable: false,
        ignoreJSON: true
        },
        domainWhiteList: ["*"]
    };

    /**
    * 通过cors跨域资源共享策略实现跨域
    * cors是一项W3C标准，它允许向跨源服务器发送异步请求，克服了异步请求的同源限制
    */
    config.cors = {
        origin: "*",
        allowMethods: "GET,HEAD,PUT,POST,DELETE,PATCH"
    };
```