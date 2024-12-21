### 无法找到模块“../pages/test/index.vue”的声明文件。“/Users/xxxx/src/pages/test/index.vue”隐式拥有 "any" 类型

通过vite搭建的vue3项目，昨天新建的vue文件，没有报错任何的异常提示。刚才又新建了一个vue文件，结果在router文件导入该页面组件的是，提示找不到vue的声明文件，具体信息如下：

```bash
无法找到模块“../pages/test/index.vue”的声明文件。“/Users/xxxxx/src/pages/test/index.vue”隐式拥有 "any" 类型。
```

**解决方案**

在项目根目录下的env.d.ts(也可能是vite-env.d.ts，vite初始化的项目是这个文件名)文件中，添加上vue文件的类型声明:

```ts
declare module "*.vue" {
    import type { DefineComponent } from "vue";
    const component: DefineComponent<{}, {}, any>;
    export default component;
}
```

然后，提示消失。