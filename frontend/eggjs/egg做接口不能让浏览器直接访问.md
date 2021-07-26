### 使用egg做接口，怎么让浏览器不能直接访问接口

无论我们使用何种开发语言、何种开发框架，只要是开发的接口，都需要通过http协议去访问，那么浏览器就天生支持http协议。所以，无论通过任何一种开发框架或者语言开发的接口都可以被浏览器直接访问。那么又有基于安全的顾虑，不想让浏览器直接访问我们的接口，那怎么办呢？

一般情况下，做浏览器对接口访问限制的是就是做用户权限验证的，例如需要用户登录。如果是一些信息展示类的，不需要用户的身份验证，那么就不需要做浏览器直接对接口的访问限制。我们这里先讨论需要做用户权限校验的场景。

其实我们的期望是浏览器对接口的访问限制，底层上是对用户校验方法实现的限制，需要限制客户端再每次请求服务器接口的是都要带上登录状态就可以了。这里我的简单的实现逻辑是JWT。

JWT：JSON Web Token，是为了在网络应用环境之间传递声明而执行的一种基于JSON的开放标准。

在Egg项目中实现JWT登录逻辑：

安装egg-jwt

```bash
npm install egg-jwt --save
```

在config/config.js配置jwt：

```javascript
  jwt: {
    enable: true,
    package: "egg-jwt"
  }
```

在config/config.default.js中配置secret：

```javascript
  config.jwt = {
    secret: "hello"  //secret可以自定义
  };
```

生成token：一般是在做身份校验的时候生成token，也就是在登录的时候：

```javascript
class LoginController extends Controller {
    async login() {
        const { ctx, app } = this;
        const secret = app.config.jwt.secret;
        const name = "Nicholas";
        const pwd = "Niu3286_.*";
        
        /**
        * 生成token
        * 生成token时可以携带多个参数，是一个对象
        * 最后将生成的token返回给客户端 
        */
        const token = app.jwt.sign({
            name: name
        }, app.config.jwt.secret);
        ctx.body = {
            msg: "登录成功",
            secret: secret,
            token: token
        };
    }
}
```