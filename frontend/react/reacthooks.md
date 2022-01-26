<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. 简单认识react hooks](#1-%E7%AE%80%E5%8D%95%E8%AE%A4%E8%AF%86react-hooks)
- [2. 了解React](#2-%E4%BA%86%E8%A7%A3react)
  - [2.1 使用组件的方式描述UI](#21-%E4%BD%BF%E7%94%A8%E7%BB%84%E4%BB%B6%E7%9A%84%E6%96%B9%E5%BC%8F%E6%8F%8F%E8%BF%B0ui)
  - [2.2 React组件的本质是什么？](#22-react%E7%BB%84%E4%BB%B6%E7%9A%84%E6%9C%AC%E8%B4%A8%E6%98%AF%E4%BB%80%E4%B9%88)
- [2.3 Hooks](#23-hooks)
- [3. Hooks基础](#3-hooks%E5%9F%BA%E7%A1%80)
  - [3.1 内置Hooks](#31-%E5%86%85%E7%BD%AEhooks)
    - [3.1.1 useState，让函数式组件具备维持状态的能力](#311-usestate%E8%AE%A9%E5%87%BD%E6%95%B0%E5%BC%8F%E7%BB%84%E4%BB%B6%E5%85%B7%E5%A4%87%E7%BB%B4%E6%8C%81%E7%8A%B6%E6%80%81%E7%9A%84%E8%83%BD%E5%8A%9B)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. 简单认识react hooks

react引入了hooks之后，函数式组件就具备了状态管理、生命周期管理等能力，几乎可以实现原来class式组件等所有能力。

函数式组件结合hooks带来的简洁的写法，以及直观的逻辑重用能力，让函数式组件称为了react中的一等公民。目前，在整个react生态中，几乎所有项目的开发都已经在围绕hooks开展了。

从class式组件模式开发，到函数式组件模式开发转变，可能会遇到各种各样的问题，但是这也都是正常的。因为从class式组件的开发到函数式组件模式的开发，转换的不仅仅是写法的区别，而是整个开发思路的转变。这就需要我们开发者都要投入到当前使用的技术思路中去思考问题，才能把技术的道路走通。

**应该怎么去学React Hooks？**

1. 最重要的是要准确的知道Hooks的功能边界，也就是知道它能做什么。

否则就有可能会陷入一个误区，就是既然Hooks那么好，那我所有的问题都使用Hooks去做，也或者是使用Hooks是最优秀的解决方案，但是却没有想到它。

2. 掌握核心概念和原理

![React Hooks核心概念和原理图](./images/i30.webp)

### 2. 了解React

React，其实就是一个很简单的UI库，它的用法，主要就是3个概念：组件、状态和JSX。

React中，任何一个state发生变化时，整个函数组件都会被重新执行一遍，而且除了state，多次执行之间没有任何的关系。所以在React中考虑一个组件的实现时，我们要首先考虑这个组件中都有哪些组件（state），这些状态的变化都是由什么触发的，从而将整个组件的功能串起来。

**思考** React最打动你的特性是什么？或者说它的最大的优点有哪些？

#### 2.1 使用组件的方式描述UI

React中，所有的UI都是通过组件去描述和组织的。也可以简单的理解，React中所有的元素都是组件，具体来讲又可以分为两种组件：

1. 内置组件：内置组件其实就是映射的HTML组件，如div、p、table、img等，作为约定，内置组件，都使用小写方式。

2. 自定义组件：自定义组件就是自己定义的组件，是一些内置组件的集合，形成了一个新的模块功能。作为约定，自定义组件使用大驼峰的命名规范，就是首字母大写，多个单词拼接时，每个单词的首字母都大写，如Header、NewsList等。

React和DOM节点定义的方式类似，React组件也是树状结构的，且React应用只有一个根组件。

#### 2.2 React组件的本质是什么？

React组件的模型，其实就是Model到View的映射，这里的model对应到React中，就是state+props：

![React组件模型：Model到View的映射](./images/i31.webp)

**什么是数据绑定？**

当Model(state、props)中的数据发生变化时，UI会自动发生变化，即所谓的数据绑定。

所以从这个角度来讲，我们可以把UI的展现看成一个函数的执行过程。其中，model是输入参数，函数的执行结果是DOM树，也就是View。而react要保证的，就是每当Model发生变化时，函数会重新执行，且生成新的DOM树，然后React再把新的DOM树以最优的方式更新到浏览器。

### 2.3 Hooks

Hooks，就是钩子的意思。React中，Hooks就是把某个目标结果钩到某个可能会变化的数据源或者事件源上，当被钩到的数据源或者事件源发生变化时，产生这个目标结果的代码就会重新执行，产生更新后的结果。对于函数式组件，这个结果就是最终的DOM树。

Hooks的思想，不光是在React中可用，其他的应用场景也可用。

Hooks的最大的好处，就是逻辑的复用。

**Hooks的最大的好处，就是逻辑的复用**

在Hooks之前的React使用中，经常被大家诟病的一点就是非常难以实现逻辑的复用，必须借助告诫组件等复杂的设计模式。但是告诫组件会产生荣誉的组件节点，让调试变的困难。这些问题在Hooks中得到了很好的解决，所以说Hooks的最大好处，就是简化了逻辑的复用。

**Hooks的另一个好处，就是有助于关注分离**

有助于关注分离，意识是说Hooks能够让针对同一个业务逻辑的代码尽可能的聚合在一起。

这一点在类式组件中很难实现的，因为在类式组件中，我们不的不把同一个业务逻辑的代码分散在不同的生命周期方法中。

所以说，通过Hooks的方式，可以让代码更加容易理解和维护。

**类式组件和函数式组件的区别**

类式组件和函数组件的一个区别，就是类式组件是通过技术角度组织到一起的，例如在不同的生命周期阶段做一些特定的事情，而函数式组件式通过业务角度组织到一起的，相同业务逻辑的代码组织在一起，从而更加的容易理解和维护。

Hooks称为了React开发的主流方式，它在一定程度上体现了React的开发思想，即从State =》View的函数映射。

### 3. Hooks基础

#### 3.1 内置Hooks

如果我们过去是基于类式组件做开发，或者刚开始学习的时候学习的是类式组件，那么就会很熟悉类式组件中的生命周期，如componentDidMount、componentWillUnmount等等，需要考虑每个生命周期的钩子中可以做什么事情，什么事情需要放在哪个周期钩子函数中合适。但是我们现在要学习的是基于Hooks的函数式组件编程，这是一个完全不同的思路，在学习和开发中，我们不用去关心组件的生命周期。

但是如果我们以前已经熟悉了类式开发，那么就可以彻底的忘掉类式组件中的生命周期方法；如果以前没有接触过React，那么恭喜你，没有了类式组件思维模式的包袱，可以轻装上阵。

当遇到需求时，**直接考虑怎么使用Hooks去实现**

React内置的Hooks其实非常少，一共只有10个，如useState、useEffect、useContext、useCallback、useMemo、useRef、useReducer、useDebugValue、useImperativeHandle、useLayoutEffect。

##### 3.1.1 useState，让函数式组件具备维持状态的能力

useState这个Hook是用来管理状态的，它可以让函数组件具备维持状态的能力。也就是说，在一个函数组件多次渲染之间，这个state是共享的。

```jsx
import React from 'react';

export default function Count() {
    // 创建一个保存count的state，且初始化为8
    const [count, setCount] = React.useState(8);
    const increment = () => {
        setCount(count + 1);
    }
    return <div>
        <p>{count}</p>
        <button onClick={increment}>+</button>
    </div>;
}
```

根据上面的案例，我们可以大概看出来useState这个hook的用法：

1. useState(initialState)的参数initialState是创建state的初始值，这个值可以是任意类型，如Number、Object、Array等；

2. useState()的返回值是一个有着2个元素的数组：第1个元素是用来读取state的值，第2个元素是用来设置state值的方法。

需要注意的是，state的变量是只读的，如果要修改state的值，必须且是只能通过第2个元素，就是修改这个state值的方法去修改。

3. 如果要创建多个state，那么就需要多次调用useState()

```jsx
    // 创建一个保存count的state，且初始化为8
    const [count, setCount] = React.useState(8);
    // 创建用于保存用户列表的state，类型为Array
    const [users, setUSers] = React.useState([]);
    // 创建用于保存个人档案的state
    const [profile, setProfile] = React.useState({
        name: "Nicholas Zakas",
        age: 18,
        gender: "sex"
    });
```

**什么值需要且可以保存在state中呢？**

state是React中一个非常重要的机制，那么什么样的值需要或者可以保存在state中呢？

原则就是：<font color="#f20">state中永远不要保存可以通过计算得到的值</font>。如

1. 从props传递过来的值。有些场景从props传递过来的值无法直接使用，而是需要经过一定的处理之后才会在UI上展示，比如排序。可以通过props的方式传递过来排序的方式、规则，每次调用排序的时候，都重新计算一次排序算法、过程，而不是直接把排序的结果保存在state中。

2. 从URL中获取到的值。有的场景需要从RL中获取参数，并把它作为组件的一部分状态。那么这个时候，我们可以在需要的时候直接从URL中获取这个参数，而不是直接从URL中读取出来保存在state中。

3. 从cookie、localStorage中读取的值。像这些保存在缓存中的数据，需要的时候，直接从缓存中读取，而不是先读取出来再保存在state中。

**useState的弊端**

虽然useState这个Hook便于维护state状态，但是也有自己的弊端。一旦组件有自己的状态，那么就意味着如果如果组件重新渲染了，那么组件就需要有恢复状态的过程，就会让组件变得复杂。

如果通过一些状态管理工具如redux，去管理所有组件状态的话，那么组件本身就是无状态的了。无状态组件就可以更纯粹的聚焦在表现层，没有太多的业务逻辑，从而可以让组件更加的易于使用和维护。

##### 3.1.2 useEffect(): 执行副作用

useEffect，用于执行一段副作用。

那么什么是副作用呢？其实，副作用，就是一段和当前执行结果无关的代码。比如说要修改函数外部的一个变量，要发起一个http请求等，也就是说，在函数组件的当次执行过程中，useEffect()中的代码是不影响渲染出来的UI的。

useEffect()函数可以接收2个参数：

```js
useEffect(callback,dependencies);
```

第一个参数为要执行的回调函数，第二个参数为可选的依赖项数组dependencies，依赖项数组是可选的。如果不指定依赖项，那么每次函数组件执行完后都会执行回调函数callback，如果指定了依赖项，那么只有在依赖项中的值发生变化的时候，才会执行callback。

如果和class类式组件对应的话，那么useEffect()涵盖了componentDidMount、componentDidUpdate、componentWillUnmount三个生命周期方法，如果我们习惯了使用类式组件，千万不要拿useEffect和生命周期中的某个或者某几个生命周期钩子函数去对应。我们只要记住，useEffect是每次组件render()完成后判断依赖并执行就可以了。

例如一个Blog详情的demo，这个组件会接收一个参数表示blog的id，而当id发生变化时，组件需要发起请求来获取文章的内容并展示：

```jsx
import React, { useEffect, useState } from 'react';

export default function BlogView({ id }) {
    // 设置本地的用于存储content的state
    const [blogContent, setBlogContent] = useState(null);

    useEffect(() => {
        // useEffect函数的callback要避免直接的async函数，要封装一下
        const doAsync = async () => {
            // 当id发生变化时，要清空content以保持内容的一致性
            setBlogContent(null);
            // 发情http请求，获取blog的内容详情
            const res = await fetch(`/blog-content/${id}`);
            // 将获取到的新的blog详情放入state
            setBlogContent(await res.text());
        };
        doAsync();
    }, [id]); // 使用id作为依赖项，当id发生了变化时，执行网络请求(副作用)

    const isLoading = !blogContent;
    return <>
        {isLoading ? "Loading……" : blogContent}
    </>;
}
```

案例利用useEffect()完成了一次数据请求并将新数据展示到页面中的操作。在这个案例中，使用id作为依赖项，在id发生变化的时候，就利用useEffect去执行副作用，请求新的内容。

**useEffect()还有2个特殊的用法：没有依赖项，或者依赖项为空数组**

1. 没有依赖项，每次render后都会重新执行

```js
useEffect(() => {
    // 每次render完后都执行
    console.log("每次render完后都执行");
});
```

2. 依赖项为一个空数组，则只有在首次render时触发，对应类式组件就是componentDidMount()

```js
useEffect(() => {
    // 依赖项为空数组，只有在第一次render时执行,对应类式组件就是componentDidMount()
    console.log("依赖项为空数组，只有在第一次render时执行,对应类式组件就是componentDidMount()");
},[]);
```

**useEffect()还可以返回一个函数，用于在组件销毁时做一些清理的工作，如移除事件的监听、移除定时器等，类似于类式组件中的componentWillUnmount钩子函数**

```js
// 自定义hooks
const useWindowSize = () => {
    const [size, setSize] = useState(getSize());
    useEffect(() => {
        const handler = () => {
            setSize(getSize());
        }
        window.addEventListener("resize", handler);

        // 返回一个函数，在组件销毁时调用
        return () => {
            window.removeEventListener("resize", handler);
        }
    }, []);
    return size;
}
```

**useEffect()让我们能够在下面4种场景下去执行一个回调函数产生副作用**

1. 每次render()后都执行：不提供第2个依赖项参数

```js
useEffect(() => {});
```

2. 仅在第一次render()后执行：提供一个空数组作为依赖项

```js
useEffect(() => {},[]);
```

3. 第一次render及以后依赖项发生变化时执行：提供一个依赖项数组

```js
useEffect(() => {},[deps]);
```

4. 组件销毁时执行：返回一个回调函数

```js
useEffect(() => {
    return () => {}
},[]);
```

##### 3.1.3 正确理解依赖项

在useEffect()中提到了依赖线的概念，其实除了在useEffect()中会用到依赖项，在后面即将要接触到的useMemo、useCallback也会用到。

如前面在刚接触Hooks时提到的，Hooks提供了让我们监听某个数据变化的能力。这个变化可能会触发组件的刷新，也可能会创建一个副作用，又或者是刷新一个缓存。那么定义要监听的那些数据变化的机制，就是指hooks的依赖项。

需要注意的是，依赖项并不是内置hooks的一个特殊机制，而是可以认为是一种设计模式。有类似需求的hooks都可以使用这种设计模式去实现。

在定义依赖项时，需要注意3点：

1. 依赖项中定义的变量一定是在回调函数中用到，否则声明的依赖项就没有了意义。

2. 依赖项一般情况下是一个常量数组，而不是一个变量。因为一般在创建callback的时候，就已经很清楚需要依赖哪些项了；

3. React会使用浅比较来对比依赖项是否发生了变化，所以要特别注意数组和对象类型。如果我们每次创建一个新对象，即使和之前的值是等价的，也会认为是依赖项发生了变化。

```js
function HookDemo(){
    // 组件每次执行的时候，都会创建一个新的数组
    const todos = [
        {
            text: "lear hooks"
        }
    ];
    useEffect(() => {
        console.log("Todos changed!");
    },[todos]);
}
```

> 浅比较，也称为引用相等，js中，====是作浅比较，只检查左右两边是否是同一个对象的引用

> 深比较，也称原值相等比较，深比较是指检查两个对象的所有属性是否都相等，深比较需要以递归的方式遍历两个对象的所有属性，操作比较比较耗时，深比较不管这2个对象是否是对同一个对象的引用。

##### 3.1.4 掌握hooks的使用规则

Hooks本身作为一个纯粹的js函数，不是通过某个特殊的API去创建的，而是直接定义一个函数。它需要遵循一定的规则才能正常的使用。Hooks的使用规则，主要包含下面2个：只能在函数组件的顶级作用域使用、只能在函数组件或者其他hooks中使用。

1. 只能在函数组件的顶级作用域使用

所谓的顶级作用域，就是指在函数内的最外层作用域，而不能在循环、条件判断或者嵌套函数内执行，而是必须在函数内的最外层作用域。同时Hooks在组件的多次渲染之间，必须按顺序被执行。

因为在react组件内部，其实是维护了一个对应组件的固定Hooks执行列表的，以便在多次渲染之间保持Hooks的状态，并做对比。

下面的代码一定会被执行到：

```js
function Demo(){
    const [count,setCount] = useState(0);
    return <div>{count}</div>;
}
```

但是下面的代码，就会出现问题，因为这些场景中，hooks并没有在函数组件的最外层作用域。

```js
function ErrorHooks(){
    const [count,setCount] = useState(0);
    if(count > 20){
        // 错误，useEffect不能出现在条件判断中
        useEfffect(() => {
            // 执行某些业务逻辑
            // ……
        },[count]);
    }

    // 这里的return，可能会提前结束组件的渲染，后面的代码将不再被执行
    if(count == 0){
        return "";
    }

    // 错误，不能将Hooks放在return之后
    const [loading,setLoading] = usestat(false);

    // ……
    return <div>{count}</div>
}
```

**Hooks的这个规则，可以总结为两点**

* 所有hook必须要被执行到

* 必须要按顺序执行

2. 只能在函数组件或者其他hooks中使用

Hooks作为专门为函数式组件设计的机制，使用情况只有两种：**一种是在函数组件内，另一种情况是在自定义的Hooks里面**

这个规则，如果在同时存在类组件和函数式组件的项目里，就会造成一定的困扰。因为hooks的简洁、直观，在函数式组件中，我们肯定是倾向于Hooks来实现逻辑的复用。但是在类式组件中，怎么办呢？可以利用**高阶组件的模式，将Hooks封装成高阶组件，从而在类组件中使用**

##### 3.1.5 使用ESLint插件帮助检查Hooks的使用

