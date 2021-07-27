### 中间件

egg中的中间件，目录在app中，

```bash
├─app
|  ├─router.js
|  ├─public
|  ├─middleware
|  |     └auth.js
|  ├─controller
|  |     ├─book.js
|  |     ├─home.js
|  |     ├─login.js
|  |     └user.js
```

将自定义中间件放置在app/middleware目录下，然后可以在config/config.default.js中进行配置：

```javascript
// 添加中间件
config.middleware = ["auth"];
```

这里可以配置多个中间件，执行顺序为从前到后的顺序依次执行。

中间件的开发，可以做一个简单的约定，一个中间件就是一个文件，是一个exports的一个函数。该函数接收2个参数，options和app。options为中间件的配置项，app为当前应用的实例。