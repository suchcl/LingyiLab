### @vue/cli4.x设置开发环境代理服务器

标题写的是vue-cli的4.x版本，实际上应该是从3.x版本就可以使用同样的方法了。方法：在vue.config.js中，新增一个devServe的配置项，demo如下：

```javascript
module.exports = {
    // 开发环境设置代理
    devServer: {
        proxy: {
            "/api": {
                target: "http://127.0.0.1:7001", // 这个url是自定义的，根据自己的api服务器地址自行修改即可
                changeOrigin: true,
                ws: true
            }
        }
    }
};
```

这样我们在开发环境的时候，在有接口请求的地方直接写协议url即可，而不需要写api的全路径，给我们的日常开发带来不少的便利。