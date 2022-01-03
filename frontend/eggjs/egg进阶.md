### 1. Egg基本介绍

Egg遵循“约定优于配置”的原则，适合团队开发。当然了，个人开发也可以用。

### 2. 项目创建

以npm为例

```bash
# 可以通过create指令
npm create egg --type=simple

# 也可以通过init指令
npm init egg --type=simple
```

使用npm创建egg项目的两种方式，都可以，创建出来的项目，是完全相同的。

运行项目：

根据项目创建完成后的提示信息

```bash
- cd D:\EggPro\egg1
- npm install
- npm start / npm run dev / npm test
```

也可以使用yarn来创建项目

```bash
yarn create egg --type=simple
```

使用yarn和npm没有太大的区别，我习惯使用npm，后面的案例，都以npm为例，不再单说yarn了。

### 3. egg和express/koa的区别

| 特征对比                    | Egg.js                                 | Express/Koa              |
| --------------------------- | -------------------------------------- | ------------------------ |
| 代码规范性：（MVC开发模式） | 符合MVC模式：Controller、Service、View | 灵活编码，没有明确的规范 |
| 学习成本                    | 中                                     | 易                       |
| 创建机制/扩展机制           | 有                                     | 无                       |
| 多线程管理                  | 有                                     | 无                       |
| HttpClient集成              | 有                                     | 无                       |

### 4.案例编写

```js
// controller
  async newsList() {
    const { ctx } = this;
    ctx.body = "新闻消息";
  }
```

eggjs中，controller部分的所有方法，都要写成异步的，即通过async修饰

### 5.代码/目录结构分析

#### 5.1 controller

controller，一般有3个作用：

1. RESTFul API：接收客户端用户请求参数，并将处理的结果返回给用户；
2. 根据URL请求，渲染HTML页面
3. 代理服务器：将接收到的用户请求转发到另外一个服务器，并将另一个服务器处理后的数据返回给终端用户

controller文件中class的命名，一般都会标识contoller，如UserController

```js
"use strict"; // 开启严格模式
const Controller = require("egg").Controller; // 从egg获取到Controller

// class命名，标识xxxController，表示这是一个controller，并从egg的Controller中继承
class UserController extends Controller {
    // controller中的所有方法，都要是异步的，即async修饰
    async index() {
        const { ctx } = this;
        // 根据url请求，渲染页面内容
        ctx.body = "<h1>个人中心</h1>"
    }

    async list() {
        const { ctx } = this;
        ctx.body = "<h2>用户列表333</h2>";
    }
}

module.exports = UserController;
```

写好了controller后，还要注册下路由，以便让客户端的请求找到响应的controller处理

```js
// router.js
// 所有的js文件，都开启严格模式
'use strict';

/**
 * @param {Egg.Application} app - egg application
 */
module.exports = app => {
  const { router, controller } = app;
  router.get('/', controller.home.index); // controller.home表示controller目录中的home文件
  router.get("/news", controller.home.newsList);
  router.get("/profile", controller.user.index); // controller.user表示controller目录下的user文件
  router.get("/user/userList", controller.user.list);
};
```

