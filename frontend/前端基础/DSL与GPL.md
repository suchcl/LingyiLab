<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. DSL与GPL](#1-dsl%E4%B8%8Egpl)
- [2. DSL语言的分类](#2-dsl%E8%AF%AD%E8%A8%80%E7%9A%84%E5%88%86%E7%B1%BB)
- [3. 可视化平台](#3-%E5%8F%AF%E8%A7%86%E5%8C%96%E5%B9%B3%E5%8F%B0)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. DSL与GPL

DSL，全称Domain Specific Language，领域特定语言。指一种为解决特定领域问题的计算机编程语言，如CSS、SQL、JSON等都可以归属为DSL。

GPL，全称General Purpose Language，通用编程语言。通用编程语言，是为了解决通用问题的，不适应应用在特定领域，如C、Java等编程语言。这些编程语言不是为了解决特定的样式问题、数据结构问题，而是它们可以解决很多行业的通用问题。

最近几年，DSL在前端开发领域出现的频率比较大，和近几年前端开发技术的发展有很大的关系。

### 2. DSL语言的分类

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

语言工作，是一种专用的IDE，可以将DSL可视化。可视化，一直是前端开发领域永远追求的目标和热点，如VSCode以及前端开发的各种可视化工具。

### 3. 可视化平台

最近几年，很多大厂都在搭建可视化的低代码平台，旨在提高开发效率，降低开发成本，降低页面开发的难度，让服务端开发人员、产品运营人员甚至是任何有页面诉求的人都可以自己搭建自己需要的页面。但是搭建这样的平台，难度之大、投入之高，但是在这样高难度和投入的前提下，也蕴藏了极大的潜在的回报。也就是大厂有这个实力和能力去搭建、开发这样的系统。

这种可视化平台，一般都会期望是通用性较好，适用范围更广，使用难度较低，见效更快，且使用过程要灵活、简单，要有极高的可配置性。我们希望这个平台有很多、很丰富的组件，能够满足各种场景下的页面拼装，并且能够简单的进行事件响应，能够非常容易的进行api的配置、属性的配置、交互的配置。我希望的逻辑也能够在平台上进行傻瓜式配置而不需要进行代码开发。