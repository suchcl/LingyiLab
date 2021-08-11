### 认识canvas

canvas是一个HTMl第5个版本标准中新增的一个元素，可以使用js脚本来绘制图形。例如现在使用率非常高的echars就是使用canvas绘制的（最新版本的可以选择使用svg或者canvas绘制，上一个版本就直接使用的canvas绘制的）。canvas可以绘制一些2d图形，也可以绘制3d图形。

> 总结一下就是canvas是一个可以被用来通过javascript（Canvas API或者WebGL API）绘制图形。

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

### 总结两点需要注意的地方

1. 标签需要闭合
   
```html
<!--错误的，不能自闭合-->
<canvas />

<!--canvas闭合标签-->
<canvas></canvas>
```

2. 元素需要设置尺寸：默认为300x150

> 这里建议优先使用html属性为canvas设置宽高尺寸

### 渲染上下文

canvas创造了一个固定大小的画布，它公开了一个或多个渲染上下文，这个上下文可以用来绘制和处理要展示的内容，这里我们将主要关注2D的渲染上下文中。这里说到了我们将主要关注2D的上下文，那就说明了还有其他类型的渲染方式，如3D上下文（只不过是通过WebGL使用的OpenGL ES的标准）。

### 绘制图形

canvas只支持两种形式的图形绘制：矩形和路径。所有的其他类型额图形都是通过一条或者多条路径组合而成的。虽然canvas只支持两种图形的绘制，但是canvas给我们提供了很多路径的生成方法。


### 绘制矩形的方法

> 在绘制图形的时候，我们记住几个英文单词，分别是fill、stroke、clear，fill为填充，stroke滑动、描边，clear清除。绘制图形中的很多方法，都是基于这几个单词来进行的。

```javascript
fillRect(x,y,width,height); // 绘制一个起点为(x,y)宽为width和高危height的填充矩形

strokeRect(x,y,width,height); // 绘制一个起点为(x,y)、宽为width和高危height的描边矩形

clearRect(x,y,width,height); // 清除1个区域的矩形，起点为(x,y)
```

### 绘制路径

图形的基本路径是路径，路径是通过不同颜色、不同宽度、不同曲线连接而形成的不同形状的集合。一个路径，或者是一个子路径，都是闭合的。绘制路径的一般步骤：

1. 创建路径的起点；

2. 使用画图命令、方法去绘制路径；

3. 路径封闭；

4. 路径生成，通过描边或者填充路径区域来渲染图形。

#### 绘制路径的常用方法

```javascript
beginPath(); // 新建一条路径，一旦开始绘制路径，图形的绘制命令就会被指向到路径上

closePath(); // 闭合路径，路径闭合之后，图形的绘制命令重新回到canvas上下文中

stroke(); // 通过线条来绘制图形轮廓

fill(); // 通过填充路径的区域生成实心的图形
```

一般的步骤，生成、绘制路径的第一步是beginPath(),