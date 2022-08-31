### 1. 对react的简单的认识

应该从几个方面去阐述：

1. 是什么

2. 怎么用

3. 有什么优势

4. 有什么弊端

5. 针对存在的弊端，有没有改进办法

React支持类式组件和函数式组件，从现在的使用场景和官方团队来看，是比较推荐函数式组件，如官网所说，它只关注UI层面，是一个UI 库(UI Library)而不是一个UI框架(UI Framework).

Reac社区活跃，本身灵活，开发者可以根据自己的业务需求开发具有针对性的组件，设计适合自己的解决方案。在react高灵活性的同时，也给新手带来了很大的迷惑，那么多相似场景的解决方案，哪个是最好的呢，那个我可以直接拿来使用呢？给新手带来了额外的学习成本。

### 2. 一些良好的react开发实践

1. 小组件拆分

react本身对于组件的拆分是没有大小的要求的，并没有明确的规定或者要求说，某个自定义组件达到多少行了就需要考虑重新拆分组件了，或者说某个组件最多只能有多少行了，react没有这样的要求。优秀的实践是按照功能拆分组件，只要是一个单独的功能，就拆分为一个组件。父组件只关心子组件的布局问题，传递给子组件必要的信息，而不去关心子组件的内部实现。

这样拆分完成之后，组件，就成了组成react应用的基本组成部分了。优势很多，子组件拆分的合理，代码的复用性提高，提升开发效率；子组件和父组件解藕，功能独立，互不干涉，减小了安全风险；

2. 每个文件只定义一个组件

先看案例：

```tsx
const Parent = () => {
  const [count,setCount] = useState<number>(0);
  const handleClick = () => {
    setCount(count+1);
  }

  const Child = () => {
    return (
      <button onClick={handleClick}>点击</button>
    )
  }

  return (
    <Child />
  );
}
```

在Parent组件中，又定义了一个Child组件，就是说在Parent组件中嵌套了Child组件。这种方式定义组件，虽然在某些开发场景下带来了一定的遍历，比如Child组件可以调用Parent组件中的函数、使用Parent组件中的数据而不需要传递props，但是这里面也隐藏了很大的性能问题。每次Parent组件更新、重新渲染的时候，Child组件都会被重新创建，原来定义的Child组件被销毁。

类似的组件定义的良好实践是不嵌套定义组件，所有子组件都提取到父组件外部单独定义。如：

```tsx
const Child = (props: any) => {
  const { onClick, number } = props;
  return (
    <>
      <p>数字: {number}</p>
      <button onClick={onClick}>点击变数</button>
    </>
  );
};

export default function index() {
  const [count, setCount] = useState<number>(0);
  const handleClick = () => {
    setCount((count) => count + 1);
  };

  return (
    <>
      <Child onClick={handleClick} number={count} />
    </>
  );
}
```

3. 避免组件嵌套