### 样式的scoped

js可以通过webpack、新的技术标准实现模块化，CSS虽然可以通过webpack实现组织的模块化，但是实际上css声明的样式还是全局，会覆盖全局，那么怎么实现css的模块化呢，我在当前组件中声明的css怎么只作用在当前组件而不会对其他组件产生影响呢？

通过给style标签添加scoped属性。

```vue
<style scoped>
    .userinfo {
        background-color: #f20;
    }
</style>
```

在给style添加了scoped属性后，该style标记内的所有样式，都只是作用于当前组件。style添加了scoped后：

1. 样式只作用于当前组件，不会作用域其他组件：其他组件使用了当前定义的样式选择器也不会产生影响；

2. 会对当前组件的子组件产生影响；