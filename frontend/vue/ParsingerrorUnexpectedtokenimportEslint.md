### Vue报错：Parsing error: Unexpected token importeslint

vue项目开启了eslint，在一个js文件中，很正常的代码报错了：

```js
const User = () => import("../pages/User.vue");
```

就这么一行导入路由文件的代码，报错了：

```bash
Parsing error: Unexpected token importe slint
```
从报错信息可以看出来，异常时eslint在检查代码的时候的报错，但是正常来说，这行代码确实是没有问题的，而且还只有第一行代码有问题，如果删了第一行代码，那么同样的问题会抛给下一行。

```js
const User = () => import("../pages/User.vue");
const Profile = () => import("../pages/Profile.vue");
```

如果我删了第一行代码，那么同样的错误，就会到第二行身上。

这个错误时阻塞性的，这个错误存在，npm run dev的时候阻塞，

```bash
 ERROR  Failed to compile with 1 error                                                                                                                                                         下午5:02:01

 error  in ./src/router/index.js

Module Error (from ./node_modules/eslint-loader/index.js):

/xxxxpro/src/router/index.js
  4:20  error  Parsing error: Unexpected token import

✖ 1 problem (1 error, 0 warnings)


 @ ./src/main.js 6:0-36 12:8-14
 @ multi (webpack)-dev-server/client?http://10.240.36.223:8080&sockPath=/sockjs-node (webpack)/hot/dev-server.js ./src/main.js
```

但是这个阻塞性，有不是一直都是阻塞，比如我刚才有重新执行了下npm run dev,代码已经正常运行了，但是如果重新进行了文件编辑后，就又报错了。

