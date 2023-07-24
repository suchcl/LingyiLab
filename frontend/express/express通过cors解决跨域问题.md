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

