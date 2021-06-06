Vue项目，配置DllPlugin的时候，在执行编译动态库的时候报错：[webpack-cli] Error: Unknown option '-p'

Vue项目的webpack和webpack-cli版本如下：

```bash
PS D:\www.xxx.com> npm ls webpack-cli -g
D:\NodeJs\node_global
`-- webpack-cli@4.7.0

PS D:\www.xxx.com> npm ls webpack -g
D:\NodeJs\node_global
`-- webpack@5.1.3
```

webpack.dll.config.js配置代码如下：

```javascript
const { CleanWebpackPlugin } = require("clean-webpack-plugin");
const path = require('path');
const Webpack = require('webpack');
const { library } = require('./dll.config');

module.exports = {
    entry: {
        // 第三方库
        ...library
    },
    output: {
        filename: '[name].dll.js',
        path: path.join(__dirname, 'dist/dll'),
        library: '[name]_dll_[hash]'
    },
    plugins: [
        new CleanWebpackPlugin(),
        new Webpack.DllPlugin({
            name: '[name]_dll_[hash]',
            path: path.join(__dirname, 'dist/dll', '[name].manifest.json')
        })
    ]
};
```

这里我把需要提取的动态库给单独配置了一个文件，文件名是dll.config.js,配置内容如下：

```javascript
module.exports = {
    library: {
        Vue: ['Vue'],
        Antd:['ant-design-vue'],
        // Vendor:['Vue','ant-design-vue']
    }
};
```

这里的配置都比较简单，就是把需要提取的库从这里罗列了一下，也可以把这个文件的library直接放到webpack.dll.config.js中的entry（入口）属性中，效果是一样的。

我在package.json文件配置的命令脚本如下：

```javascript
"dll": "webpack -p --progress --config ./webpack.dll.config.js"
```

问题就出在了这行命令中的-p参数。一加上-p参数，就报异常了：

```bash
PS D:\www.xxx.com> npm run dll

> www.xxx.com@0.1.0 dll D:\personProject\www.xxx.com
> webpack -p --progress --config ./webpack.dll.config.js

[webpack-cli] Error: Unknown option '-p'
[webpack-cli] Run 'webpack --help' to see available commands and options
npm ERR! code ELIFECYCLE
npm ERR! errno 2
npm ERR! www.xxx.com@0.1.0 dll: `webpack -p --progress --config ./webpack.dll.config.js`
npm ERR! Exit status 2
npm ERR!
npm ERR! Failed at the www.xxx.com@0.1.0 dll script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in:
npm ERR!     D:\NodeJs\node_cache\_logs\2021-06-01T03_52_56_827Z-debug.log
```

提示我未知的选项-p，我还专门看了下其他项目，也是有这个参数的，但是命令可以正常执行，没有任何问题。

> 其实出现问题的主要原因是对webpack知识的了解的不够详细，经过查询文档，原来到了webpack的高级版本中个，去掉了-p这个参数。具体是webpack的哪个版本，我现在没有确认，不过我查询webpac5文档，已经没有了-p这个参数。后续我确认了具体对应的版本后，我再同步信息。

