### egg中获取客户端参数的形式

常用的http请求方法有get、post、delete、put等，使用的最为广泛的是get和post。

获取客户端get传参方式的参数值

```javascript
const params = {
    id: this.ctx.query.id,
    username: this.ctx.query.name
};
console.log(`编号：${params.id}`);
console.log(`用户名：${params.username}`);
```

获取客户端post方式传参方式参数值

```javascript
    async updateArticle(){
        const {ctx} = this;
        
        // 获取post传参方式数据
        const params = {
            id: ctx.request.body.id,
            userName: ctx.request.body.username,
            mobile: ctx.request.body.mobile
        };
        const data = params;
        ctx.body = data;
    }
```

> egg默认开启了csrf验证，在使用post方式传参的时候需要配置下验证方式，也可以简单的直接用用掉,具体可参考：[https://github.com/eggjs/egg-security](https://github.com/eggjs/egg-security)

禁用，需要在config.default.js中做些配置：

```javascript
  // 禁用post提交方式的csrf验证
  config.security = {
    csrf: {
      enable: false
    }
  };
```