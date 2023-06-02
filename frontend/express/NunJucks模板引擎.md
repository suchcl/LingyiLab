模板引擎，主要的能力就是渲染数据，数据类型主要有字符串、对象、数组，除了需要将这些不同的数据类型的数据在模板中正常的渲染出来，也要根据条件进行判断是否渲染，如条件判断、逻辑判断等。

### 数据传递

nunjucks，可以接收的数据，只有对象类型，数组可以理解为一种特殊的对象。

当然了，也可以接收单个的变量，但是这个变量也是一种变形的对象，如：

```js
const str = "Apple";
res.render("index", {str});
```

虽然表面上看是传递了一个变量，但是本质上是以对象的形式传递的，这里实际上传递的是：

```js
res.render("index", {str:str});
```
对象中属性名和值相同，做了简写形式。

> nunjucks,只能接收对象类型数据。或者说，从controller中，只能将对象类型的数据传递给模板。

#### 对象

看案例。

```js
router.get("/", function (req, res, next) {
  const str = "Apple";
  const data = {
    code: 200,
    message: "success",
    title: "Express",
    content: "Welcom to Express's World!哈哈好",
  };
  res.render("index", data);
});
```

案例是说在请求根路径的时候，会渲染index.njk模板，同时把data数据传递给index.njk模板。从代码中可以看到，数据data是一个对象，没有通过{}封装。在模板中的使用方式如下：

```html
<h1>{{title}}</h1>
<p>{{code}}</p>
<p>{{message}}</p>
<p>Welcome to {{title}}</p>
<h4>{{content}}</h4>
```

通过对象传递给模板的数据，在模板中可以直接使用

#### 字符串传递

#### 数组遍历

### 条件判断


### 模板修改后页面渲染效果同步更新配置

默认情况下，当修改了nunjucks模板后刷新页面，发现页面并没有同步更新，发现只有在有数据更改的情况下才能实现页面的同步更改，但很多场景下是只会修改样式或者页面结构，并不会涉及到数据的更改，那么这种情况下怎么实现模板和页面的同步更改呢？

实现这个效果，可以借助chokidar包通过2个步骤实现：

1. 安装chokidar包

这是一个监听文件变化的插件

```bash
npm install chokidar --save
```

2. 在nunjucks的配置中配置watch: true

```js
nunjucks.configure("views",{
  autoescape: true,
  express: app,
  watch: true // 监听nunjucks模板的变化，实现模板和页面同步更新
});
```

不同的技术方案组织方式可能配置的地方不同，但是本质上是在nunjucks的配置中添加上watch，并设置为true即可。

### 模板中引入公共模板

在nunjucks模板中，也可以像动态语言一样直接引入一个公共文件，方式如下：

```html
{% include "./header.njk" %}
```

可以看到，在nunjucks中，可以在一对大括号中通过两个百分号%包裹的地方写表达式，然后通过include关键词引入了一个公共的文件，公共文件可以使用相对路径和绝对路径。