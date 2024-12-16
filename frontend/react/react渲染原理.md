## 1. 简介

当我们使用React UI库编写代码时，无论是组件更新、状态的改变，还是父子组件之间的交互，都会涉及到React的渲染流程。那么我们应该就会有以下的一些疑问：

1. 组件渲染的具体流程是什么？

2. 引起组件重新渲染的因素有哪些？

3. React.memo、useMemo和useCallback等优化手段的原理是什么？怎么利用好它们？

## 2. 渲染过程

### 2.1 初次渲染

首先，我们来定义一个组件:

```tsx
functin Home() {
    return (
        <>
            <div>Home 首页</div>
            <h3>Home组件</h3>
        </>
    )
}
export default Home;
```

当页面初次渲染或者项目初次启动时，React会先创建一个根节点，用来绑定组件,并且使用render函数渲染具体的组件：

```tsx
createRoot(document.getElementById('root')!).render(
  <StrictMode>
    <App />
  </StrictMode>,
)
```

由于我们已经在App组件中引入了Home组件，所以就得到了Home组件中的tsx：

```tsx
<>
    <div>Home 首页</div>
    <h3>Home组件</h3>
</>
```

React会把这段tsx转换为虚拟DOM，即用Javascript对象的方式描述DOM元素：

```js
{
    type: React.Fragment,
    props: {
        children: [
            {type: "div", props: { children: "Home 首页"}},
            {type: "h3", props: { children: "Home组件"}}
        ]
    }
}
```

那么在首次渲染时React会将虚拟DOM转换为真实DOM：

```html
<div id="root">
    <div>Home 首页</div>
    <h3>Home组件</h3>
</div>
```



### 2.2 更新渲染

## 3. 如何避免不必要的渲染？

### 3.1 React.memo

### 3.2 useMemo和useCallback

## 4. 总结

React渲染组件时，首先会执行函数组件，生成一个虚拟DOM树，以描述组件的结构。接着会将其与旧的虚拟DOM树对比，找到需要更新的部分，修改页面。只有state的改变会引起组件的重新渲染，并且它的所有子组件也会被重新渲染。如果想优化这一过程，可以使用React.memo、useDemo或者useCallback这3种方法对应不同的场景。深入理解React的渲染原理，有助于我们快速定位性能瓶颈，解决复杂场景中的问题。