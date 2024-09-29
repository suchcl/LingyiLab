demo: expressserver

### Nunjucks模板在nodejs项目中的简单使用

### 1. 简介

Nunjucks是一个功能丰富且强大的模板引擎，用于在Node.js服务器端渲染HTML和其他文本格式的模板。它类似于Python的Jinja2模板引擎，但是被设计用于JavaScript环境，特别是Express和Koa这样的Web框架.Nunjucks的高性能、模板语法丰富、可扩展、自动转移、异步加载等特点,使得它在Node.js项目中有着广泛的应用.

### 2. 快速上手

#### 2.1 模板引擎安装

```bash
npm install nunjucks
```

#### 2.2 搭建node.js项目,配置nunjucks模板引擎

node.js项目的搭建,以express为例,具体可以参考[https://www.expressjs.com.cn/starter/generator.html](https://www.expressjs.com.cn/starter/generator.html).

```bash
# 创建express项目
npx express-generator

# 如果是较老的node版本,也可以使用下面的指令分步骤搭建
npm install -g express-generator

express
```

配置项目启动指令

```json
"scripts": {
    "dev": "nodemon ./bin/www"
}
```

express项目中配置nunjucks模板

```js
// 导入nunjucks模板
const nunjucks = require('nunjucks');

// 模板引擎配置
nunjucks.configure('views', {
  autoescape: true,
  express: app,
  watch: true
})
app.set("view engine", "njk");
```

新建简单模板index.njk

```html
<!DOCTYPE html>
<html>
  <head>
    <title>{{title}}</title>
    <link rel='stylesheet' href='/css/style.css' />
  </head>
  <body>
    <h1>{{title}}</h1>
  </body>
</html>
```

controller渲染模板,并设置一个简答的测试数据

```js
router.get('/', function(req, res, next) {
  res.render('index', { title: 'Hello Nunjucks!' });
});
```

启动项目

```bash
npm dev
```

<img src="./images/i11.png" width="120" />

至此,已经完成了在一个nodejs项目中nunjucks模板引擎的配置.

### 3. 常用模板功能

#### 3.1 文件扩展名

#### 3.2 数据展示

#### 3.3 过滤器

#### 3.4 表达式

##### 3.4.1 if表达式

##### 3.4.2 逻辑表达式

##### 3.4.3 比较表达式

#### 3.5 for循环

#### 3.6 宏(macro)

#### 3.7 set

#### 3.8 include

#### 3.9 import


### 4 小结



逻辑非 not

```js
{% if not flag %}
    <p>来来来</p>
{% endif %}
```