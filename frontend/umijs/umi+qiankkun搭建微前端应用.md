### 1.umi+qiankun搭建微前端应用

微前端应用，我了解过的有MicroApp(https://micro-zoe.github.io/micro-app/)和qiankun(https://qiankun.umijs.org/zh/guide),不过以前都是简单的了解过，由于实际项目并没有这个诉求，也就没有深入调研实践过，仅仅简单的了解了下。

MicroApp和qiankun的一个最外在的区别，就是基座应用。

由于是很早之前看的，现在先简单的说下，以后补充个确认的结论。印象中，MicroApp，需要搭建一个基座应用，这个基座应用，就是纯粹的基座应用，不做别的用途；其他应用，即需要嵌入到这个基座应用的那些应用都作为这个应用的子应用，这些子应用地位平等，不存在主从的关系。而在qiankun中，不需要搭建这么一个纯粹的基座应用。qiankun的思想，是选择一个主应用(逻辑上的主应用吧，理论上哪个应用都可以)作为前端应用的基座应用，其他应用作为子应用接入。

<font color="#f20">这是我大概的一个印象，接下来我补充确切的文档说明。</font>

关于MicroApp，可以参考：[MicroApp](../%E6%9E%B6%E6%9E%84%E4%B8%8E%E8%AE%BE%E8%AE%A1/%E5%BE%AE%E5%89%8D%E7%AB%AF.md)

关于qiankun，可以参考[qiankun](../%E6%9E%B6%E6%9E%84%E4%B8%8E%E8%AE%BE%E8%AE%A1/qiankun.md)

### 2.umi介入qiankkun，搭建微前端应用

下面我们就逐步记录下umi项目接入qiankun搭建微前端应用的过程和步骤。

#### 2.1 主应用

1. 安装qiankun

```bash
yarn add qiankun
```

2. 安装@umijs/plugin-qiankun插件

```bash
yarn add @umijs/plugin-qiankun -D
```

3. 注册子应用:在配置文件.umirc.ts或者config/config.ts中，添加qiankun配置项

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

4. 状态子应用(就是配置路由，可以跳转到子应用)

添加子应用路由，和普通的应用路由，稍有区别，要新增一个microApp字段，属性名为第3步中配置的apps中的name属性值。

```ts
routes: [
    // ……
    {
    path: '/subApp1',
    name: '子应用1',
    icon: 'smile',
    microApp: 'sub-app1'
    },
    // ……
]
```

#### 2.2 子应用

1. 安装@umijs/plugin-qiankun插件

```bash
yarn add @umijs/plugin-qiankun -D
```

2. 挂载@umijs/plugin-qiankun插件

其实就是将子应用配置为从属应用，从子应用中的配置文件中配置，因为我的子应用也是umi项目，所以就以umi项目为例进行记录了。

> 如果子应用是其他类型的应用如vue应用、不是前后端分离项目，接下来再做个调研，

```ts
// config/config.ts
  // ……
  qiankun: {
    slave:{}
  },
  // ……
```

到这一步，基座应用和子应用都是umi项目的应用已经搭建完成，且可以正常运行了。

> 有的创建项目的脚手架没有在package.json文件中创建中设置name属性及属性值，这个不需要特别记忆，就是在项目运行的时候如果报错了，知道去添加下这个属性即可。

3. 导出相应生命周期的钩子

在src/app.ts中添加以下生命周期的钩子函数,如果没有app.ts文件则自行创建即可。

```ts
// src/app.ts
export const qiankun = {
    // 应用加载之前
    async bootstrap(props:any){
        console.log('应用加载之前:', props);
    },

    // 应用render之前
    async mount(props:any){
        console.log("应用render之前:", props);
    },

    // 应用卸载之后
    async unmount(props:any){
        console.log("应用卸载之后:", props);
    }
};
```