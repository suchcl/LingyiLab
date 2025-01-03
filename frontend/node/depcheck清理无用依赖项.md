### 使用depcheck清理无用的依赖项

文档：[https://github.com/depcheck/depcheck](https://github.com/depcheck/depcheck)

如果一个项目做了很长时间了，或者接手了别人的一个项目，看到package.json文件里面的依赖项很长，就总想清理下，但是又不确定哪些是在用，哪些是没有在用的，导致没有办法、干脆的清理。那么这个时候，我们就可以使用depcheck来检测没有使用的依赖，然后清理掉。

**使用depcheck**

1. 安装

```bash
npm install depcheck -g
```

2. 使用

```bash
depcheck path/to/project
```

案例：

```bash
vite-react (dev =)]$ depcheck
Unused dependencies
* lodash
Unused devDependencies
* @types/lodash
* gulp
```

没有使用到的dependencies有lodash，没有使用到的devDependencies有@types/lodash和gulp。

> 使用depcheck的时候，还有很丰富的配置，具体可以参考:[https://github.com/depcheck/depcheck](https://github.com/depcheck/depcheck)