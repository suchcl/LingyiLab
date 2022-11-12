<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. umi项目中页面跳转传递及接收参数](#1-umi%E9%A1%B9%E7%9B%AE%E4%B8%AD%E9%A1%B5%E9%9D%A2%E8%B7%B3%E8%BD%AC%E4%BC%A0%E9%80%92%E5%8F%8A%E6%8E%A5%E6%94%B6%E5%8F%82%E6%95%B0)
- [2. Link组件方式页面跳转，并实现参数的传递和接收](#2-link%E7%BB%84%E4%BB%B6%E6%96%B9%E5%BC%8F%E9%A1%B5%E9%9D%A2%E8%B7%B3%E8%BD%AC%E5%B9%B6%E5%AE%9E%E7%8E%B0%E5%8F%82%E6%95%B0%E7%9A%84%E4%BC%A0%E9%80%92%E5%92%8C%E6%8E%A5%E6%94%B6)
  - [2.1 Link组件实现常规页面跳转，不传递和接收参数](#21-link%E7%BB%84%E4%BB%B6%E5%AE%9E%E7%8E%B0%E5%B8%B8%E8%A7%84%E9%A1%B5%E9%9D%A2%E8%B7%B3%E8%BD%AC%E4%B8%8D%E4%BC%A0%E9%80%92%E5%92%8C%E6%8E%A5%E6%94%B6%E5%8F%82%E6%95%B0)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. umi项目中页面跳转传递及接收参数

umi项目中页面之间跳转，可以通过两种方式实现：

1. 路由组件：Link组件

Link组件，是umi内置的组件，可以用在umi项目中的单页面之间的跳转。

```tsx
<Link to="/route1">页面1</Link>
```

> <font color="#f20">如果umi项目中需要跳转到外部链接，那么需要使用a标签。</font>

2. js事件跳转

通过事件响应的方式实现页面之间的跳转.

```tsx
const toPage2 = () => {
    history.push("/route2");
}

<button onClick={toPage2}>通过点击事件跳转到页面2</button>
```

### 2. Link组件方式页面跳转，并实现参数的传递和接收

#### 2.1 Link组件实现常规页面跳转，不传递和接收参数

Link组件在实现常规页面之间的跳转，当不需要携带和接收参数的时候，和HTML中的a元素的使用方式类似，只是a元素的标签名更改为Link，a元素的href属性更改为to属性。

Link组件，只可在umi项目内的单页面之间进行跳转，不能实现从项目内的单页面跳转到项目外的链接。如果在一个umi项目内需要跳转到项目外部的链接，请使用a元素。

> react项目中，可以使用任意的HTML标签元素，并不是说在react项目中，就只能使用react元素，或者在umi项目中，就只能使用umi给我们封装好的一些组件。

因为是最为常规的页面之间的跳转，所以其实现和使用也比较简单。

```tsx
<Link to="/route2">页面2</Link>
```

Link，和HTML标记a元素标签等价，to属性和a元素中的href属性等价，这样，就可以实现一个页面的跳转。

**新标签页打开页面**

在不使用类似React、Vue等前端框架做前端开发的时候，通过标签a实现页面之间的跳转，默认是在当前页面打开，如果需要在新标签打开页面的时候，可以给a标签添加一个target属性，设置为_blank即可。那么现在使用了React中的Link标签，怎么实现新标签页打开页面呢？

其实，React-router中的Link以及umi的Link，都是基于a标签做的一些封装，最终体现出来的，也是a标记。其实说了那么多，可以归结为一句话，就是在使用Link组件想从新标签页打开页面的时候，也可以直接给Link组件添加一个target属性，设置为_blank即可，就可以实现新标签页打开了。

```tsx
<Link to="/route2" target="_blank">新标签页打开页面2</Link>
```

