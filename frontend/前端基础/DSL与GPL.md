### DSL与GPL

DSL，全称Domain Specific Language，领域特定语言。指一种为解决特定领域问题的计算机编程语言，如CSS、SQL、JSON等都可以归属为DSL。

GPL，全称General Purpose Language，通用编程语言。通用编程语言，是为了解决通用问题的，不适应应用在特定领域，如C、Java等编程语言。这些编程语言不是为了解决特定的样式问题、数据结构问题，而是它们可以解决很多行业的通用问题。

最近几年，DSL在前端开发领域出现的频率比较大，和近几年前端开发技术的发展有很大的关系。

### DSL语言的分类

DSL语言大概可以分为3类：外部DSL、内部DSL和语言工作台。

1. 内部DSL和语言工作台

内部DSL可以认为是一种通用编程语言的特定用法，只不过有一些特定的用法，形成了自己的风格。比如前端开发比较熟悉的jQuery，还有Gulp、Grunt等，它们都是基于Javascript这门通用编程语言，只是它们又在解决特定场景的问题时又形成了自己独特的风格。

可以简单看下jQuery的代码风格:

```js
$("#id").show()
        .next("div")
        .hide();
```

jQuery在DOM操作上，有自己独特的方法，是别的库不具备的。

2. 外部DSL

外部DSL，是真正的DSL，是一种独立的编程语言或规范语言，大多都有自己独立的语法。在前端开发领域常用的DSL如CSS、HTML、JSX等都属于外部DSL。

```HTML
<style>
    .box {
        width: 200px;
        height: 100px;
        margin: 0 auto;
    }
</style>
<div class="box">
    <div class="title"></div>
    <div class="content"></div>
</div>
```

3. 语言工作台

