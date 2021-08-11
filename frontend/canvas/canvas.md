### 认识canvas

canvas是一个HTMl第5个版本标准中新增的一个元素，可以使用js脚本来绘制图形。例如现在使用率非常高的echars就是使用canvas绘制的（最新版本的可以选择使用svg或者canvas绘制，上一个版本就直接使用的canvas绘制的）。canvas可以绘制一些2d图形，也可以绘制3d图形。

canvas最早是由apple引入到webkit中的，在Mac OS X中使用，后来被个浏览器实现，现在除了非常早、很老版本的浏览器可能不支持外，正常标准的浏览器都是支持canvas的。

在使用canvas绘制图形的时候，我们看可以通过css、canvas标记的属性来为canvas设置尺寸。在使用canvas绘制图形的时候，该元素有一个默认的尺寸，为300x150(宽x高，单位为像素px)。

在使用canvas绘制图形的时候，我们需要一些HTMl和Javascript的基础知识，如果这些方面不太熟悉的同学，可以先补充一下HTMl和Javascript基础知识，分别可以参考[HTML超文本标记语言](https://developer.mozilla.org/zh-CN/docs/Web/HTML)和[Javascript教程](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript)。

canvas标签使用的时候，和其他的HTML标记基本一样，没有什么区别，除了具体功能的API的差异化之外，有一点需要注意的是，有一些HTML标签可以是自闭合，但是canvas必须要关闭标签，不能让元素自己自闭合。

```html
<!--错误的，不能自闭合-->
<canvas />

<!--canvas闭合标签-->
<canvas></canvas>
```

> canvas默认要设置尺寸属性，如果不设置就启用默认尺寸值（300x150，单位px）

```html
<!--使用默认尺寸：width和height都使用默认值，分别为300x150 px,实际在浏览器显示的时候，可能是375x187.5，也可能是其他设置的缩放比例和默认设置的值的等比例缩放的值-->
<canvas class="app"></canvas>

<!--显示指定canvas的width和height,虽然是通过html属性来指定的，单位也是px-->
<canvas class="app" width="300" height="200"></canvas>

<!--通过css来设置canvas的初始尺寸,这种方式和通过html属性设置方式效果相同，只是表现和结构分离了，代码更容易维护，可读性更高了-->
<canvas class="app"></canvas>
<style>
    .app{
        width: 320px;
        height: 160px;
    }
</style>
```