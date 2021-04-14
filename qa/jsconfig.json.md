### Vetur can't find `tsconfig.json` or `jsconfig.json` in d:\www.xxx.com.

vetur0.31.0版本新增了一个vetur.config.js的配置文件，在这个版本之后，会先检查项目中是否有jsconfig.json文件（js项目，如果是ts开发的，就是tsconfig.json）。如果这两个文件都没有找到，就会给出这个提示：

```
Vetur can't find `tsconfig.json` or `jsconfig.json` in d:\www.xxx.com.
```

我们知道在项目添加一个json文件不提示了就可以了，更多内容可以参考:[https://vuejs.github.io/vetur/](https://vuejs.github.io/vetur/)