### express使用html模板

在使用expres是的时候，更多的时候因该是用来提供一些接口，偶尔的少部分场景也会用来直接渲染页面。

现在express默认使用的是pug模板引擎，pug以前叫jade，后来改了个名字。出了pug这个默认的模板引擎外，也可以自定义配置其他的模板引擎，使用量比较多的如ejs、vm等。

现在我的项目中有一个渲染页面诉求，我期望使用html，那么在express中怎么配置使用html模板呢？

### express配置使用html模板

1. 安装ejs

```bash
npm install ejs --save
```

2. app.js导入ejs的引用

```js
var ejs = require('ejs');
```

3. 模板引擎设置(app.js)

```js
app.engine('.html', ejs.__express);
app.set('view engine', 'html');
```

到此，express配置使用html模板已经完成，效果如下:

![express配置使用html模板](./images/i7.png)