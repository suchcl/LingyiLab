## npm和npx的区别

npm，就是node package manager，包管理器，它的作用很加单，没有理解上的歧义。

在后来学习React的时候，发现了npx，那么npx是什么呢，它和npm又有什么关系呢？

### npx

npx是一个npm5.2版本引入的一条指令，一个npm的包执行器。因为npm是node的自带模块，所以正常情况下，npx也是可以直接使用的，只要正常安装了node。在特殊场景下npx不能正常使用的时候，重新安装下就可以了。

```bash
npm install npx -g 需要全局安装
```

### npx主要解决2个问题

1. 调用项目内安装的模块

npx想要解决的第一个重要的问题，就是调用项目内安装的模块。这里我没有找到合理的案例，就直接使用了网上给出的案例，加入我们的项目中安装了mocha这个模块

```bash
npm install mocha --dev
```

那么如果我们想调用mocha这个模块，比如我想查看下mocha这模块的版本，一种方式是在package.json的scripts字段中添加相应的执行脚本

```javascript
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject",
    "mocha": "node_modules/.bin/mocha --version"  //新增查询mocha版本的脚本，在命令行执行npm run mocha即可
  }
```

执行下效果：

```bash
PS D:\reactpro> npm run mocha

> reactpro@0.1.0 mocha D:\reactpro
> mocha --version

8.3.2
```

这种方式我们得到了预期的效果。

如果我们不在package.json中的scripts字段中添加相应的执行脚本，那么就需要直接到node_modules目录下找到mocha去执行：

```bash
PS D:\reactpro> .\node_modules\.bin\mocha --version
8.3.2
```

> 我使用的windows，斜杠是反的，如果大家在linux或者mac下会自动是相反的方向，只是平台差异

如果我们使用npx来达到同样目标的话，既不用配置scripts脚本，也不用找node_nodules目录：

```bash
PS D:\reactpro> npx mocha --version
8.3.2
```

干净整洁，简化了配置，也不需要找繁琐的目录，简化了我们的操作。

其实npx的原理也比较简单，就是在运行的时候，会去找node_nodules/.bin路径和环境变量$path，检查命令是否存在，如果存在，直接执行即可。

所以，在执行终端命令的时候，也可以直接使用的，如ls和npx ls效果等同。

```bash
xxx@DESKTOP-EH6OH7F:/mnt/d/WebStudy/vue2/src$ ls
App.vue  assets  components  main.js

xxx@DESKTOP-EH6OH7F:/mnt/d/WebStudy/vue2/src$ npx ls
App.vue  assets  components  main.js
```

> linux环境下测试正常执行没问题，在windows终端下，没有正常执行，提示没有发现命令。由于npx重点不是执行终端命令，所以没有继续深究，也许在windows上也有合适的执行方式。

2. 避免全局安装模块

npx除了可以调用项目内部安装的模块下，还可以避免全局安装的模块。比如我们想使用create-react-app来创建管理react项目的时候，一般的情况下，我们的操作顺序大概是这样的：

```bash
npm install create-react-app -g  // 全局安装create-react-app工具

create-react-app reactprojefct //使用create-react-app创建一个react项目
```

就是一般情况下我们使用npm需要2个步骤才能创建一个react项目，同时还全局安装了create-react-app。如果我们使用npx，则是下面的方法：

```bash
npx create-react-app reactproject  //一步就创建完了react项目
```

执行上面的命令时，npx先将create-react-app下载到了一个临时目录中，等使用结束后会会删除掉。如果再次使用时会重新下载。

### npx不能找到本地模块则会自动下载该模块

当我们在使用npx指定一个使用模块的时候，如果npx后面跟的模块在本地没有发现，那么就会自动下载一个该模块，以便该模块也可以正常使用。如在一个目录中直接通过npx来启动http-server的时候，但是本地并没有这个模块，那么npx是先下载该模块并启动的：

```bash
PS D:\fb\react> npx http-server
npx: installed 23 in 3.449s
Starting up http-server, serving ./
Available on:
  http://174.0.1.84:8080
  http://192.168.56.1:8080
  http://192.168.74.1:8080
  http://192.168.50.118:8080
  http://127.0.0.1:8080
Hit CTRL-C to stop the server
```

> 虽然npx自动下载了http-server模块，但是该模块并不会保存在当前目录内。

npx在下载远程模块的时候，还可以指定版本，格式如下：

```bash
npx pkg@1.0.0 
```

给个案例：

```bash
PS D:\fb\event> npx uglify-js@3.10.0 .\event.js -o .\js\event.min.js
npx: installed 1 in 1.674s
```

npx指定了3.10.0版本的uglify-js去压缩event.js并输出到了指定目录下。

npx的这种自动模块识别的功能很好，很人性化，但有的时候我们可能就是希望使用本地模块而不进行自动安装，或者就是希望自动安装最新版本而忽略本地模块。

1. --no-install 强制使用本地模块而不进行自动安装，如果本地没有该模块则报错

```bash
PS D:\fb\react> npx --no-install http-server
not found: http-server
```

2. --ignore-existing  忽略本地模块，强制使用远程模块

```bash
PS D:\fb\react> npx --ignore-existing http-server
npx: installed 23 in 2.838s
Starting up http-server, serving ./
Available on:
  http://174.0.1.84:8080
  http://192.168.56.1:8080
  http://192.168.74.1:8080
  http://192.168.50.118:8080
  http://127.0.0.1:8080
Hit CTRL-C to stop the server
```

### 管理node版本

<font color="#f00">利用npx可以下载模块的这个特点，可以通过npx指定node版本的方式进行node版本切换。这里有问题，留待解决</font>

```bash
npx node@15.10.0 -v
```

这里没有给出运行结果，正常情况下应该打印出当前指定的node的版本的，我本地是windows环境，网上查询是权限问题，我尝试了使用管理员权限运行命令行，也没有解决问题，预留问题吧，应该是权限问题。

```bash
C:\Users\xxx> npx node@15.0.0 -v
v15.0.0
internal/fs/utils.js:307
    throw err;
    ^

Error: EPERM: operation not permitted, unlink 'D:\NodeJs\node_cache\_npx\33596\node_modules\node\bin\node.exe'
    at Object.unlinkSync (fs.js:1210:3)
    at fixWinEPERMSync (C:\app\nvm\v14.15.4\node_modules\npm\node_modules\rimraf\rimraf.js:219:13)
    at rimrafSync (C:\app\nvm\v14.15.4\node_modules\npm\node_modules\rimraf\rimraf.js:319:28)
    at C:\app\nvm\v14.15.4\node_modules\npm\node_modules\rimraf\rimraf.js:350:5
    at Array.forEach (<anonymous>)
    at rmkidsSync (C:\app\nvm\v14.15.4\node_modules\npm\node_modules\rimraf\rimraf.js:349:26)
    at rmdirSync (C:\app\nvm\v14.15.4\node_modules\npm\node_modules\rimraf\rimraf.js:342:7)
    at fixWinEPERMSync (C:\app\nvm\v14.15.4\node_modules\npm\node_modules\rimraf\rimraf.js:217:5)
    at rimrafSync (C:\app\nvm\v14.15.4\node_modules\npm\node_modules\rimraf\rimraf.js:319:28)
    at C:\app\nvm\v14.15.4\node_modules\npm\node_modules\rimraf\rimraf.js:350:5 {
  errno: -4048,
  syscall: 'unlink',
  code: 'EPERM',
  path: 'D:\\NodeJs\\node_cache\\_npx\\33596\\node_modules\\node\\bin\\node.exe'
}
```

然后我在WSL的ubuntu上测试效果，也失败了。

```bash
xxx@DESKTOP-EH6OH7F:/mnt/c/Users/ya596$ node -v
v10.19.0
xxx@DESKTOP-EH6OH7F:/mnt/c/Users/ya596$ npx node@15.10.0 -v
v10.19.0
```