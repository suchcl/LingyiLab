### vetur

做前端开发的同学应该都比较熟悉它，vetur是一个vscode插件，用来提供对.vue单文件组件提供代码高亮以及语法支持，还可以提供代码格式化的能力。

除此之外，前端开发的同学，也知道，vue2和vetur对于ts的支持，并不是分友好。在@vue/composition-api插件之前，vue2中的ts使用时需要vue-prototype-decorator插件的支持，通过装饰器模拟的方式进行模拟，但是这种方式不是从底层的支持，而仅仅是在最外层做了一些转换，所以才有了vue2中使用ts时的一塌糊涂的体验。

### volar

在vue3发布之后(2020年9月18日，vue3- one piece版本)，vue3是直接使用ts开发的，从底层上直接支持了ts。所以，vue3，对ts的支持很友好。

可参考：https://juejin.cn/post/6966106927990308872