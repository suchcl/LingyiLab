### umit4导入antd

最近umi4升级了，默认的情况下，没有引入ant的引用，如果需要的话，就需要我们自己手动去导入一下了。

在config/config.ts文件中做相关配置：

```ts
// 先导入umi的配置函数
import {defineConfig} from "umi";

export default defineConfig({
    // 导入antd插件
    plugins:[
        require.resolve("@umijs/plugins/dist/antd")
    ],
    // 开启antd
    antd:{}
})
```

然后就可以正常使用了。

> 关于config/config.ts配置文件，之前有看到说可以通过exprot default{}，就是到处对象的方式进行相关配置，但是我好像没有配置成功过，一般都是在.umirc.ts文件中做配置，只有前几天尝试的时候，突然发现config/config.ts中的配置方式，也是需要导入umi的配置函数，通过配置函数去执行配置项，而并不是直接去导出一个配置对象就可以了。