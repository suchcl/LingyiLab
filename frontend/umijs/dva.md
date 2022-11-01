### dva是什么？

dva是一个基于redux和redux-saga的数据流方案。

我们先简单了解下react的数据方案历史。

我们都知道，react是一个UI库，它自己本身只关注UI层面的事情，其他的周边生态如路由、数据等管理和存储等，都没有做，聚焦UI。这就是react的特点，这也就导致了react的技术社区比较活跃，每个技术团队都可以有自己的实现，在带来了技术活跃的同时，也有一点不好的地方，就是技术混乱，没有统一的标准。这对于一个前端开发者来说尤其是一个刚接触react的开发者来说，非常的不友好。

由于React专注于UI，没有考虑数据存储的实现，那么社区就出现了各种各样的数据存储方案，其中比较知名的是redux ------ 很多人都以为redux是针对react的数据流方案，其实不是的。redux也可以在vue中处理好数据流问题，只是redux是在react中获得了较大的成功，再加上vue有自己的vuex数据流方案，就让很多人误以为redux就是针对react的数据流方案。

redux无疑在react中取得了较大的成功，但是redux有一点不足，就是它只考虑到、实现了同步的数据流，没有考虑到异步场景下的数据流的问题，于是就出现了redux-saga，redux-saga解决了异步的数据流方案。

那么dva呢，是一个基于redux和redux-saga的数据流方案，并且还内置了react-router和fetch，简化了一些开发体验。所以，很多人也将dva看作是一个轻量级的应用框架。

### 简单了解下dva的工作流

可以看下下图：

![dva工作流](./images/i11.png)

从图片我们可以看出来，数据仓库中有同步数据、异步数据和订阅(subscription).

> 严格来讲，订阅是不属于数据仓库范畴的，而是属于页面的，只是为了代码的便于代码的管理而归属到了数据仓库。

dva的数据工作流，页面可以调用数据仓库中的同步数据和异步数据，但是数据仓库只能以同步的reducer将数据返回给页面。

### dva的组成

dva，其实就是一个对象，这个对象主要包含了几个部分：

namespace、state、reducers、effects、subscriptions。其中，reducers、effects和subscriptions中都是函数。一个完整的dva示例如下：

```ts
const UserModel = {
    namespace: 'users',
    state: {

    },
    reducers:{

    },
    effects:{

    },
    subscriptions:{

    }
};

export default UserModel;
```