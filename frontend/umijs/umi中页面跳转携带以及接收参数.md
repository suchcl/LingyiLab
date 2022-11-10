### umi项目中页面跳转传递及接收参数

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