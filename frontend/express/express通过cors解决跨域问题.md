### express通过cors解决跨域问题

关于跨域的一些详细介绍，可以参考[express跨域](./express跨域.md),这里我们只简单的介绍下在express中通过cors解决跨域问题.

安装cors中间件包

```bash
# 安装cors包
yarn add cors # 也可以使用npm、pnpm等包管理工具安装，根据个人习惯即可
```

**配置所有路由都支持跨域**

express中导入cors中间件并使用

```js
// 导入cors中间件包
const cors = require("cors");

// 添加cors中间件
app.use(cors());
```

到这里，最简单的通过cors中间件解决跨域问题已经解决，这种基础版的结局问题方式，支持所有的路由都支持跨域，且cors中间都使用的默认配置。

**配置指定路由支持跨域**

```js
// 导入cors中间件包
const cors = require("cors");

// 在指定的路由中添加cors引用
router.get("/appList", cors(), OaController.getAppList);
```

这种就是只在指定的/appList路由支持跨域，其他的路由不支持跨域

### 关于cors的一些简单介绍

cors(Cross-Origin Resource Sharing)是一个nodejs包，用于解决跨域资源共享问题，它为express应用程序提供了一个中间件，可以轻松的添加跨域支持。

使用cors中间件可以允许其他域名下的客户端向指定的express服务器发情http请求，从而实现跨域请求，cors中间件会自动添加cors相关的headers到HTTP响应中，以便浏览器可以理解和处理它们。

cors常用的中间件选项：

- origin: 指定允许的源。可以是字符串、正则表达式、函数或数组。默认为*，表示允许所有的源

- methods: 指定允许的HTTP方法。可以是字符串或数组，默认为GET、HEAD、POST

- allowedHeaders: 指定允许的headers。可以是字符串或数组，默认为*，表示允许所有的headers

- exposedHeaders: 指定客户端可以访问的headers。可以是字符串或者数组

- credentials: 指定是否允许发送和接收身份验证数据，默认为false

- maxAge: 指定预检请求的有效期，单位为秒