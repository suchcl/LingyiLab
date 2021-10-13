### 怎么在vue中使用less预处理器？

几年以前，记得在vue项目中使用less选择器的时候，需要手动配置一些less-loader或者plugin啥的，具体配置哪个忘记了。但是今天在使用vue-cli构建一个新项目的时候，发现并不需要配置这些loader了，就可以直接使用less预处理器。

我的vue、cli以及less、less-loader的版本是：

```json
"dependencies": {
    "core-js": "^3.6.5",
    "vue": "^2.6.11"
  },
  "devDependencies": {
    "@vue/cli-plugin-babel": "~4.5.0",
    "@vue/cli-plugin-eslint": "~4.5.0",
    "@vue/cli-service": "~4.5.0",
    "less": "^4.1.2",
    "less-loader": "^6.0.0",
  },
```

但是这里有个问题需要注意，如果安装less-loader是不加版本号，直接安装最新的版本，可能会有个报错：

```bash
 ERROR  Failed to compile with 1 error                                                                 5:50:14 ├F10: PM┤

 error  in ./src/layout/header.vue?vue&type=style&index=0&lang=less&

Syntax Error: TypeError: this.getOptions is not a function


 @ ./node_modules/vue-style-loader??ref--10-oneOf-1-0!./node_modules/@vue/cli-service/node_modules/css-loader/dist/cjs.js??ref--10-oneOf-1-1!./node_modules/vue-loader/lib/loaders/stylePostLoader.js!./node_modules/postcss-loader/src??ref--10-oneOf-1-2!./node_modules/less-loader/dist/cjs.js??ref--10-oneOf-1-3!./node_modules/cache-loader/dist/cjs.js??ref--0-0!./node_modules/vue-loader/lib??vue-loader-options!./src/layout/header.vue?vue&type=style&index=0&lang=less& 4:14-470 15:3-20:5 16:22-478
 @ ./src/layout/header.vue?vue&type=style&index=0&lang=less&
 @ ./src/layout/header.vue
 @ ./src/router/router.js
 @ ./src/main.js
 @ multi (webpack)-dev-server/client?http://192.168.50.43:8080&sockPath=/sockjs-node (webpack)/hot/dev-server.js ./src/main.js
```

我没有查这个问题的根源是什么，但是一个表象是less-loader的版本太高了，降低下less-loader的版本就可以了。比如我降低到6.2.0是可以的。

