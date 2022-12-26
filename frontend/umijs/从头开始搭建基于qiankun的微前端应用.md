### 1. 分别创建两个项目

> 本文先以两个umi项目为例搭建应用，完成之后会分别大家vue以及不使用常规如react、vue等前端库、框架搭建的应用，去探索基于qiankun搭建这些应用，以及这些应用之间的通信。

项目以umi为基座应用。

#### 1.1 搭建umi的子应用

```bash
mkdir myapp && cd myapp
yarn create @umijs/umi-app
```

以umi推荐的方式创建两个umi应用，一个作为主应用，即基座应用，一个项目作为子应用。

#### 1.2 搭建vue子应用

<font color="#f20">这里介绍vue项目作为子应用时的配置</font>

> 先尝试探索umi项目，稍厚探索研究vue项目

### 1.3 搭建混合开发类型的子应用，可以以html+js为模型

### 2. 安装依赖

主应用和子应用都分别安装qiankun依赖。

#### 2.1 主应用

1. 安装qiankkun

```bash
yarn add qiankun
```

2. 安装qiankun插件

```bash
yarn add @umijs/plugin-qiankun -D
```

#### 2.2 子应用

安装qiankun插件

```bash
yarn add @umijs/plugin-qiankun -D
```

### 3. 应用配置

#### 3.1 主应用

##### 3.1.1 注册子应用

在umi项目的配置文件.umirc.ts或者config/config.ts文件中，可以进行如下配置：

```ts
// config/config.ts
 //……
  routes,
  // 主应用注册子应用
  qiankun: {
    // 主应用，配置到master
    master: {
      // apps，数组，可以注册多个子应用
      apps: [
        {
          name: 'sub-app1', // 应用名称
          entry: 'http://localhost:8001/' // 应用url
        }
      ]
    }
  },
  // ……
```

##### 3.1.2 装载子应用

装载子应用有2种方式，一种是路由绑定的方式装载子应用，一种是使用<MicroApp />组件的方式装载子应用。

1. 路由绑定方式装载子应用

没有集成微前端应用之前，我们的路由配置大概这样子：

```ts
// config/routes.ts
export default {
  routes: [
    {
      path: '/',
      component: '../layouts/index.js',
      routes: [
        {
          path: '/app1',
          component: './app1/index.js',
          routes: [
            {
              path: '/app1/user',
              component: './app1/user/index.js',
            },
          ],
        },
        {
          path: '/',
          component: './index.js',
        },
      ],
    },
  ],
};
```

假如现在想把app1/user路由挂载一个微前端应用,则只需要改一下路由的配置即可

```ts
{
    path: '/subapp',
    name: '子应用',
    routes: [
        {
        path: '/subapp/subApp1',
        name: '子应用1',
        icon: 'smile',
        microApp: 'sub-app1' // microApp属性是挂载微前端应用区别于其他常规路由唯一不同的地方，需要注意microApp的属性值，是主应用中注册的子应用的name属性值，二者需要保持一致
        },
    ],
},
```

这样，通过路由方式装载一个子应用的方式已经完成。

2. 使用<MicroApp />组件方式装载子应用

使用<MicroApp />组件方式装载子应用，就像使用普通的组件一样简单、方便，可以在组件上以props的方式携带参数，子应用中也可以像普通组件一样像在父组件中获取props一样。

使用<MicroApp />组件，需要先从umi中导入该组件,然后子应用通过useModel('@@qiankunStateFromMaster') 获取到父应用传递过来的参数

> MicroApp是umi封装的一个组件。

```tsx
// 主应用
import {MicroApp} from "umi";

<MicroApp name="sub-app2" onChange={onAdd} age={age} /> // 主应用中就像使用一个普通的子组件一样使用了<MicroApp />组件，且也传递了props

// 子应用
import { useModel } from 'umi'; // 从umi到如useModel
import { Button } from "antd";
import styles from "./index.less";

export default function MyPage() {
    //  useModel('@@qiankunStateFromMaster') 子应用可以在其内部全局拿到父应用传递过来的参数
    const masterProps = useModel('@@qiankunStateFromMaster');
    const { age, onChange } = masterProps; // 从props(可以这么理解，虽然并不是严格意义上的props)中解构参数

    // 子应用中事件，会传给父应用去处理
    const onAdd = () => {
        onChange();
    }
    return (
        <div className={styles.indexContainer}>
            <div>
                <Button type='primary' onClick={() => { onAdd() }}>子应用变化，将最新的值传递给父应用</Button>
                <div>从父应用获取到最新的值：{age}</div>
            </div>
        </div>
    )
}
```

#### 3.2 子应用

1. umi子应用

注册@umijs/plugin-qiankun插件

主应用已经装载了子应用，子应用已经安装了qiankun依赖，接下来只需要注册下qiankun插件即可。在umi项目的.umirc.ts或者config/config.ts中做个简单配置即可

```ts
// config/config.ts
  // ……
  qiankun: {
    slave:{}
  },
  // ……
```
到此，主应用和子应用都为umi项目的微前端应用框架搭建完成。

2. vue应用

3. 其他混合式开发应用

### 4. 应用通信

#### 4.1 主应用和子应用都是umi项目之间的通信

#### 4.2 主应用为umi应用子项目为vue项目的的应用个之间的通信

#### 4.3 主应用为umi应用子项目为混合式开发应用的应用之间的通信

### 5. 微前端项目的集成

微前端应用项目的集成，我理解最大的重点是在登录逻辑的打通，登录态的同步，是微前端应用集成后首先需要考虑和解决的问题。

比如如果主应用是通过cookie验证登录状态的，那么当从主应用跳转到子应用时，则通过cookie校验是否已经登录，如果已经登录了，则子应用直接跳转出登录逻辑而进入到相应的页面。如果主应用没有登录或者登录状态失效，那么子应用需要将没有登录状态告诉父应用，或者在跳转到子应用之前父应用先检测登录状态，如果没有登录则进行登录逻辑的处理。