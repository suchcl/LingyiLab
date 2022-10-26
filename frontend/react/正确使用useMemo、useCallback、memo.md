useMemo和useCallback，在很多场景下，其实不建议使用，因为使用了这2个hooks后，在页面首次render的时候需要额外做一些工作来提供缓存，不利于页面的首次加载。

正是这个原因，也有一些观点，就是说不要在刚开始写代码的时候，就想着怎么去做优化，而是等到发现问题了、或者已经发现了有问题出现的端倪了，再去优化。这个时候也不迟。

我们先不管观点的正确与否、科学与否，我们应该关注的是究竟什么场景下应该使用useMemo、useCallback这2个缓存的hooks。

### 1. 那么什么时候应该使用缓存呢？

1. 缓存useEffect的引用类型依赖；

2. 缓存子组件props中的引用类型；

#### 1.1 缓存useEffect的引用类型依赖



#### 1.2 缓存子组件props中的引用类型

缓存子组件props中的引用类型，主要是为了防止组件非必要的重新渲染导致的性能消耗，在缓存子组件props中的引用类型之前，首先需要明确组件在什么情况下需要重新渲染。

1. 组件的props或者state变化导致组件的重新渲染；

2. 父组件的重新渲染会导致其子组件的重新渲染；

明确了这2个场景之后，那么我们首先可以明确的是，在父组件中和子组件没有关系的状态变更可以不重新渲染子组件，以减少不必要的性能、资源的浪费。

一般情况下呢，我们也知道这个道理，但是就是在实现的时候，存在一些问题。

### 2. useMemo 解决因函数更新而导致自己重新渲染的问题

语法：

```markdown
const fn = useMemo(fn, array);
```

第一个参数是函数，第二个参数是依赖，只有在依赖变化时才会重新执行函数。参数fn，需要返回一个函数:

```ts
  const childClick = useMemo(() => {
    return () => {
      console.log("子组件重新执行了");
    }
  }, [b]);
```

可以看一个完整的案例：

```tsx
// Parent.tsx
import { FC, useMemo, useCallback, useState } from "react";
import Child from "./components/child";


const MultiRender: FC = () => {
  const [a, setA] = useState<number>(0);
  const [b, setB] = useState<number>(0);

  const changeA = () => {
    setA(i => i + 1);
  }

  const changeB = () => {
    setB(i => i + 1);
  }

  const childClick = useMemo(() => {
    return () => {
      console.log("子组件重新执行了");
    }
  }, [b]);

  return (
    <>
      <p>数值a:{a}</p>
      <button onClick={changeA}>改变a</button>
      <button onClick={changeB}>改变b</button>
      <Child data={b} childClick={childClick} />
    </>
  );
};

export default MultiRender;

// Child.tsx
import { FC, memo } from "react";
import styles from './index.less';

interface IProps {
  data: any;
  childClick:any;
}

const Child: FC<IProps> = ({data,childClick}) => {
  console.log("子组件渲染了");
  return (
    <>
      <div className={styles.childCmp}>
        <p>子组件</p>
        <p>从父组件接收的值:{data}</p>
        <button onClick={childClick}>子组件中点击事件</button>
      </div>
    </>
  )
}
export default memo(Child);
```

大概的效果如下：

![父组件和子组件无关状态的变化，不重新渲染子组件](./images/i50.png)

这样在点击“改变a”按钮时，只改变了a的状态，那么子组件是不会重新渲染的，只有在点击了“改变b”按钮后，因为改变了props，所以子组件就跟着变了。

**为什么不使用useMemo，改变a状态会引起子组件的重新渲染呢？**

因为childClick这个自定义事件是通过props传递给子组件的，在父组件中每次a状态发生变化的时候，父组件都会重新渲染，那么childClick这个自定义事件也都会被初始化、重新建立，所以这个props也是在父组件每次重新渲染的时候都会变化，那么props变化了，子组件就会自动更新了。

### 3. useCallback，解决useMemo需要返回一个函数的繁琐的操作

我们通过useMemo，缓解了子组件被重新渲染的问题，但是也发现一个问题，就是useMemo的第一个参数本身就是一个函数，而这个函数参数，需要返回一个函数。或者可以极端的理解一下，这第一个参数中，需要处理的逻辑，直接放在返回值参数中就可以了。效果、功能没有任何问题，那么有没有办法直接在函数参数中处理逻辑，而不需要再返回一个函数呢？

我们可以使用useCallback来解决这个问题，使用的方法和useMemo基本一致，就是useCallback的第一个函数参数不需要再返回一个函数了，有什么问题，直接在第一个函数参数中去处理。看案例:

```tsx
  const childClick = useCallback(() => {
    console.log("通过useCallback方式，更新了子组件");
  },[b]);
```

这样看起来，就比useMemo简洁了一些。来贴下完整案例吧:

```tsx
// Parent.tsx
import { FC, useMemo, useCallback, useState } from "react";
import Child from "./components/child";


const MultiRender: FC = () => {
  const [a, setA] = useState<number>(0);
  const [b, setB] = useState<number>(0);

  const changeA = () => {
    setA(i => i + 1);
  }

  const changeB = () => {
    setB(i => i + 1);
  }

  const childClick = useCallback(() => {
    console.log("通过useCallback方式，更新了子组件");
  },[b]);

  return (
    <>
      <p>数值a:{a}</p>
      <button onClick={changeA}>改变a</button>
      <button onClick={changeB}>改变b</button>
      <Child data={b} childClick={childClick} />
    </>
  );
};

export default MultiRender;

// Child.tsx
import { FC, memo } from "react";
import styles from './index.less';

interface IProps {
  data: any;
  childClick:any;
}

const Child: FC<IProps> = ({data,childClick}) => {
  console.log("子组件渲染了");
  return (
    <>
      <div className={styles.childCmp}>
        <p>子组件</p>
        <p>从父组件接收的值:{data}</p>
        <button onClick={childClick}>子组件中点击事件</button>
      </div>
    </>
  )
}

export default memo(Child);
```

> useState、useMemo、useCallback的值传递给子组件，在父组件中更新了值之后，子组件不会重新渲染，因为这3个hooks处理后的值，都是memoized值(即缓存的值).