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
    - [3.1.2 useEffect(): 执行副作用](#312-useeffect-%E6%89%A7%E8%A1%8C%E5%89%AF%E4%BD%9C%E7%94%A8)
    - [3.1.3 正确理解依赖项](#313-%E6%AD%A3%E7%A1%AE%E7%90%86%E8%A7%A3%E4%BE%9D%E8%B5%96%E9%A1%B9)
    - [3.1.4 掌握hooks的使用规则](#314-%E6%8E%8C%E6%8F%A1hooks%E7%9A%84%E4%BD%BF%E7%94%A8%E8%A7%84%E5%88%99)
    - [3.1.5 使用ESLint插件帮助检查Hooks的使用](#315-%E4%BD%BF%E7%94%A8eslint%E6%8F%92%E4%BB%B6%E5%B8%AE%E5%8A%A9%E6%A3%80%E6%9F%A5hooks%E7%9A%84%E4%BD%BF%E7%94%A8)
    - [3.1.6 useCallback 缓存回调函数](#316-usecallback-%E7%BC%93%E5%AD%98%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0)
    - [3.1.7 useMemo 缓存计算结果](#317-usememo-%E7%BC%93%E5%AD%98%E8%AE%A1%E7%AE%97%E7%BB%93%E6%9E%9C)

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

使用Hooks的一些特性和要遵循的规则，只要有3点：

1. 在useEffect回调函数中使用到的变量，都必须声明在依赖中；

2. Hooks不能出现在条件语句或者循环中，也不能出现在return之后；

3. Hooks只能在函数式组件或者自定义的Hooks中使用；

那么这些规则怎么才能保证被我们执行的好呢，我们可以借助eslint-plugin-react-hooks这个eslint插件帮我们去检查。

使用方法：

安装插件

```bash
npm install eslint-plugin-react-hooks --save-dev
```

在eslint的配置文件中进行规则配置

```js

{
  "plugins": [
    // ...
    "react-hooks"
  ],
  "rules": {
    // ...
    // 检查 Hooks 的使用规则
    "react-hooks/rules-of-hooks": "error", 
    // 检查依赖项的声明
    "react-hooks/exhaustive-deps": "warn"
  }
}
```

前面已经学习了useState()和useEffect()这2个最为核心的hooks，掌握了这2个核心的hooks，就基本上已经掌握了React函数式组件的开发思路。

当我们了解了useState和useEffect这2个最为核心的hooks后，已经可以实现大部分的业务功能开发了，但是还有一些细节的问题，如事件处理函数会被重复定义、数据计算过程没有缓存等等，还都需要一些机制来处理。这些细节问题，可以通过4个内置的hooks(useCallback、useMemo、museRef、useContext)的作用和用法，学习使用这些Hooks去解决这些细节问题。

##### 3.1.6 useCallback 缓存回调函数

在React函数组件中，每一次UI的变化，都是通过重新执行整个函数来执行的，<font color="#f20">这一点和class组件有区别：函数组件中并没有一个直接的方式在多次渲染之间维持一个状态</font>。比如下面的代码：

```jsx
import React from 'react';

export default function Counter2() {
    const [count, setCount] = React.useState(0);
    const increment = () => {
        console.log(`count: ${count}`);
        setCount(count + 1);
    }

    const decrement = () => {
        setCount(count - 1);
    }
    return <div>
        <p>{count}</p>
        <button onClick={increment}>+</button>
        <button onClick={decrement}>-</button>
    </div>;
}
```

案例代码中，我们在按钮上添加了一个事件处理函数，让计数器加1或者减1，但是因为事件处理函数式在函数内部，所以在计数器这个函数组件在多次渲染之间，加1increment和减1decrement的事件处理函数是没有办法被重用的，组件每次渲染都会被创建一个新的。

我们可以思考一下这个函数式组件的执行过程：每次组件状态发生变化的时候，函数组件都会重新执行一遍，在每次重新执行的时候，都会重新创建新的事件处理函数increment和decrement。这2个事件处理函数中，都包含了count这个状态的闭包，以确保每次重新创建的时候都能得到正确的结果。

这也就意味着，即使count这个状态没有发生变化，但是函数组件中其他的状态发生变化，或者其他原因需要重新渲染时，也会创建新的关于count状态的事件处理函数。创建这个状态的新的事件处理函数，在结果上是没有什么影响的，但是从逻辑上来讲，这是没有必要的，因为count这个状态我并没有发生任何变化，那么也就没有必要重新执行关于这个状态的事件处理函数。因为重新执行没有必要执行的代码，不仅增加了系统的资源消耗，更重要的是：<font color="#f20">每次创建新函数的方式会让接收事件处理函数的组件，需要重新渲染</font>。

比如案例中的2个按钮，分别接收了increment和decrement2个事件处理函数，并且作为属性onClick的属性值，如果组件每次渲染时都会创建新的函数，那么React就会认为这个组件的props发生了变化，从而必须重新渲染。因此，理想的状态是：<font color="#f20">只有当count这个状态发生了变化时，我们才去重新定义一个回调函数</font>，useCallback这个hook可以满足我们这个诉求。

```js
useCallback(fn,[deps]); // 用法,deps是依赖的变量数组
```

接下来通过使用useCallback来对上面的加1操作做优化的实现：

```jsx
// 使用useCallback，只有当依赖发生变化时，才去重新执行回调函数
    const increment = useCallback(() => {
        setCount(count + 1);
    }, [count]); // 只有当count发生变化时，才会重新创建回调函数
```

在新的实现里，将count这个状态作为一个依赖传递给useCallback，这样，只有当count这个状态发生变化的时候，才会重新创建一个回调函数，这样就保证了组件不会创建重复的回调函数，而接收这个函数作为属性值的组件，也不会频繁的需要重新渲染。下面来看一下完整的实现：

```jsx
import React, { useCallback } from 'react';

export default function Counter2() {
    const [count, setCount] = React.useState(0); // useState没有从React中解构出来，所以使用方式是：React.useState
    // 常规实现，会重复执行回调函数
    // const increment = () => {
    //     setCount(count + 1);
    // }

    // 使用useCallback，只有当依赖发生变化时，才去重新执行回调函数
    const increment = useCallback(() => {
        setCount(count + 1);
    }, [count]); // 只有当count发生变化时，才会重新创建回调函数
    return <div>
        <p>{count}</p>
        <button onClick={increment}>+</button>
    </div>;
}
```

##### 3.1.7 useMemo 缓存计算结果

除了useCallback，useMemo也是为缓存而设计的。只不过，useCallback缓存的是函数，useMemo缓存的是计算结果。

useMemo的API：

```js
useMemo(fn,[deps]); // fn为一个产生所需要的数据的计算函数，deps是一个依赖，数组类型、格式
```

useMemo的使用场景大概是这样子的：<font color="#f20">如果某个数据是通过其他数据计算得到的，那么只有当用到的数据，即所依赖的数据发生变化时，才应该需要重新计算</font>。

比如一个现实用户信息的列表，现在需要对用户名进行搜索，且UI需要根据搜索结果显示过滤后的用户信息列表。那么这样的一个功能需要2个状态：

1. 用户列表本身数据：默认的用户列表请求；

2. 搜索关键字：用户在输入框输入的用户名关键字；

```jsx
import React, { useEffect, useState } from 'react';

export default function UserListbyUseMemo() {
  const [users, setUsers] = useState(null);
  const [searchKey, setSearchKey] = useState("");

  useEffect(() => {
    const doAsync = async () => {
      // 组件首次加载时，请求用户数据
      const res = await fetch("https://reqres.in/api/users/");
      setUsers(await res.json());
    };
    doAsync();
  }, []);
  let usersToShow = null;

  if (users) {
    // 无论任何原因的组件刷新，这里一定会对数组做一次过滤操作
    // usersToShow = users.data.filter((user) => {
    //   return user.first_name.includes(searchKey);
    // });

    // 这里有一个语法：就是如果箭头函数体只有一个返回语句，那么可以省略函数体的大括号和return关键字，以及语句结束的分号
    usersToShow = users.data.filter(user => user.first_name.includes(searchKey));
  }
  return (
    <div>
      <input
        type="text"
        value={searchKey}
        onChange={(event) => setSearchKey(event.target.value)}
      />
      <ul>
        {usersToShow &&
          usersToShow.length > 0 &&
          usersToShow.map((user) => {
            return <li key={user.id}>{user.first_name}</li>
          })}
      </ul>
    </div>
  );
}

```

上面的这种实现，功能上没有任何问题，但是有一个潜在的性能问题，就是无论什么原因当这个组件被更新了，都会导致用户users数据被重新过滤，这可能并不是我们想要的。因为这个组件上可能除了数据还有其他数据，比如：

```jsx
import React, { useEffect, useMemo, useState } from 'react';

export default function UserListbyUseMemo() {
  const [users, setUsers] = useState(null);
  const [searchKey, setSearchKey] = useState("");
  const [num, setNum] = useState(10);

  useEffect(() => {
    const doAsync = async () => {
      // 组件首次加载时，请求用户数据
      const res = await fetch("https://reqres.in/api/users/");
      setUsers(await res.json());
    };
    doAsync();
  }, []);

  // 常规实现，有个弊端是无论什么原因组件刷新，都会重新过滤下users数据 
  let usersToShow = null;
  if (users) {
    // 无论任何原因的组件刷新，这里一定会对数组做一次过滤操作
    usersToShow = users.data.filter((user) => {
      console.log("user和搜索关键字都没有变");
      return user.first_name.includes(searchKey);
    });
  }

  // 测试数字变化
  const numIncrement = () => {
    setNum(num + 1);
  }
  return (
    <div>
      <h3>我测试下数字变化</h3>
      <button onClick={numIncrement}>数字加1:{num}</button>
      <br />
      <input
        type="text"
        value={searchKey}
        onChange={(event) => setSearchKey(event.target.value)}
      />
      <ul>
        {usersToShow &&
          usersToShow.length > 0 &&
          usersToShow.map((user) => {
            return <li key={user.id}>{user.first_name}</li>
          })}
      </ul>
    </div>
  );
}
```

这个案例，比前面仅仅多了一个num的数据，有一个操作按钮可让num变化，那么每次num变化的时候，users数据也都会过滤一遍。实际上这是没有必要的。因为num的操作和用户数据没有任何关系。这个时候，我们可以使用useMemo()来缓存下结果数据，让只有当用户数据依赖的users和searchKey发生变化的时候，用户数据才重新渲染：

```jsx
  // 通过useMemo，指定只有当users和searchKey发生变化时，才重新过滤用户users数据
  const usersToShow = useMemo(() => {
    console.log("user和搜索关键字都没有变");
    if (!users) {
      return null;
    }
    return users.data.filter((user) => user.first_name.includes(searchKey));
  }, [users, searchKey]);
```

上面的案例中，仅仅改动这一小部分，就可以了，功能完全没有任何问题，还实现了对用户数据过滤的优化，提升了性能问题，节省了资源的开销。

其实，这就是useMemo的一个非常重要的好处：<font style="color:#f20">避免重复计算</font>。

除了可以避免重复计算之外，useMemo()还有一个也非常重要的作用:<font color="#f20">避免子组件的重复渲染</font>。如案例中的usersToShow这个变量，如果每次都需要重新过滤、计算得到，那么对于自组件UserList而言，也会每次都需要刷新、重新渲染，因为usersToShow是一个属性。但是如果能缓存usersToShow这个属性，缓存了前一次的计算结果，那么就可以避免很多次不必要的重复刷新、渲染。

> 有一些场景，useCallback和useMemo是可以通用的。也就是说，可以使用useCallback实现useMemo的作用，也可以使用useMemo实现useCallback的效果。因为从本质上来说，这2个hooks都是做了同一件事：建立了一个绑定到某个结果到依赖数据的关系。只有当依赖数据变化了，这个结果才会被重新得到。

##### 3.1.8 useRef 在多次渲染之间共享数据

函数组件的一个优势，就是简化了思考UI的实现逻辑，但是和class类式组件相比，也缺失了一大功能，就是**在多次渲染之间的数据共享能力**。

在类式组件中，我们可以通过定义成员变量，以便可以在对象上通过成员属性去保存一些数据，但是在函数式的组件中，并不存在成员变量这一空间去保存数据。那么React通过useRef这样的一个Hook去实现了类式组件中数据共享的能力。

useRef API

```jsx
const myRefContainer = useRef(initialValue);
```

我们可以把useRef看作是一个函数组件之外的一个容器空间，在这个容器中，我们可以通过唯一的current属性设置一个值，从而在函数组件的多次渲染之间共享这个数值。 ---- 这一点和React中的ref是如出一辙。

比如一个计时器的案例：

```jsx
import React, { useCallback, useRef, useState } from 'react';

export default function Timer() {
    // 定义time，这个state用于保存计时的累积时间
    const [time, setTime] = useState(0);
    // 定义timer这个容器，用于在夸组件之间保存、共享变量
    const timer = useRef(null);

    // 开始计时的事件处理函数
    const timerStart = useCallback(() => {
        // 使用current属性设置ref的值
        timer.current = window.setInterval((time) => {
            setTime(time => time + 1);
        }, 100)
    }, []);

    // 暂停计时的事件处理函数
    const timerParse = useCallback(() => {
        // 使用window.clearInterval来清理计时器
        window.clearInterval(timer.current);
        timer.current = null;
    }, []);

    // 停止计时器的事件处理函数
    const timerStop = () => {
        window.clearInterval(timer.current);
        timer.current = null;
        setTime(0);
    }
    return (
        <div>
            {time / 10} seconds,
            <br />
            <button onClick={timerStart}>Start</button>
            <button onClick={timerParse}>Parse</button>
            <button onClick={timerStop}>Clear</button>
        </div>
    );
}
```

一般情况下的计时器功能，会有开始计时、暂停、清零操作、功能，在功能实现的时候，我们需要window.setInterval来提供计时功能，需要window.clearInterval提供清空计时器的功能。这是2个基本的操作，但是还有暂停，以及清零(清空计时器功能)功能的细节实现。那么我们就需要一个地方保存window.setInterval计时器的引用，以便可以在暂停和清零的时候精准的找到对应的计时器。这个时候，useRef就派上了用场。

从案例中，我们也可以看出，**useRef和UI的渲染是没有直接的关系的，因此当useRef的值发生变化的时候，是不会引起组件的重新渲染的。这是useRef区别于useState的地方**。

**useRef的两个重要作用**

1. 存储夸渲染的数据；

2. 保存某个DOM节点的引用 ----- 和React中的ref同作用