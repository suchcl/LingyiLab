<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. 简单认识Electron](#1-%E7%AE%80%E5%8D%95%E8%AE%A4%E8%AF%86electron)
- [2. 管理窗口的生命周期](#2-%E7%AE%A1%E7%90%86%E7%AA%97%E5%8F%A3%E7%9A%84%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F)
  - [2.1 关闭所有窗口时退出应用程序](#21-%E5%85%B3%E9%97%AD%E6%89%80%E6%9C%89%E7%AA%97%E5%8F%A3%E6%97%B6%E9%80%80%E5%87%BA%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F)
  - [2.2 如果没有窗口则打开一个新的窗口(MacOs)](#22-%E5%A6%82%E6%9E%9C%E6%B2%A1%E6%9C%89%E7%AA%97%E5%8F%A3%E5%88%99%E6%89%93%E5%BC%80%E4%B8%80%E4%B8%AA%E6%96%B0%E7%9A%84%E7%AA%97%E5%8F%A3macos)
- [3. Electron应用的工作机制](#3-electron%E5%BA%94%E7%94%A8%E7%9A%84%E5%B7%A5%E4%BD%9C%E6%9C%BA%E5%88%B6)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. 简单认识Electron

Electron是一个使用javascript、html、css构建桌面应用程序的框架。嵌入Chromium和nodejs到二进制的Electron应用程序，允许使用一套js代码库创建跨平台的桌面应用程序。

Electron应用程序的开发，需要本地有nodejs的支持，但是Electron应用程序的运行，不依赖本地的Nodejs和浏览器。

Electron应用和网页应用程序相比，因为是内置的chromium和Nodejs，所以Electron应用可以避免令人头疼的浏览器的兼容性问题。

**Nodejs**

Electron应用程序的开发以来nodejs，所以在开发Electron应用之前，本地需要先安全nodejs，且建议是最新版本的TLS版本。

Electron应用程序，将nodejs打包到了Electron应用的二进制文件中，所以我们运行Electron应用时的nodejs和我们本地开发环境中的nodejs版本没有任何关系。

### 2. 管理窗口的生命周期

#### 2.1 关闭所有窗口时退出应用程序

在windows和linux中，关闭了所有的窗口后，通常就是退出了一个应用，但是在MacOS中则有不同的表现

```js
// 监听window-all-closed事件
app.on("window-all-closed", () => {
    if(process.platform !== "darwin"){ // 在所有平台中都实现了统一，关闭了所有窗口后，引用程序不会完全退出
        app.quit();
    }
});
```

app.quit():不会完全退出一个应用程序，只是当前窗口关闭

#### 2.2 如果没有窗口则打开一个新的窗口(MacOs)

当linux和windows应用在没有窗口打开时退出了，则应用程序也就退出了，但是MacOs即使在没有任何窗口打开的情况下，程序也会继续运行，且在没有窗口可用的情况下激活新的窗口，虽然这个窗口不一定能被看到。

为了效果的统一，需要实现不同平台下的功能一致，可以通过监听app模块的activate事件，当监听到没有窗口时，则打开一个窗口来实现功能：

```js
// 应为打开窗口需要在应用的ready后才能创建，所以就需要将activate事件在app的ready回调中进行监听
app.whenReady().then(() => {
    createWindow();
    // 当没有窗口可用时打开新的窗口
    app.on("activate", () => {
        if (BrowserWindow.getAllWindows().length === 0) {
            createWindow();
        }
    })
});
```

### 3. Electron应用的工作机制

使用Electron开发桌面应用，就像是定制的一个简易版的chrome浏览器，只是这个浏览器不能随意输入url，只能是去渲染指定的url或者文件。

electron和浏览器类似，Electron应用程序分为主进程和渲染进程。

主进程负责控制应用程序的生命周期、创建和管理应用程序窗口，有着多种控制原生桌面功能的模块，如菜单、对话框以及托盘等；

渲染进程负责完成界面渲染、接收用户输入、响应用户交互等功能；

染进程和渲主进程之间进行交互，通过icpRenderer跟主进程进行数据交互。

**一个Electron应用只能有一个主进程，但是可以有多个渲染进程。**

electron应用中，不能在主进程中(可以简单理解不能在main.js)访问、编辑DOM，因为它无法访问渲染器文档上下文，它们存在于不同的进程中。

**主进程和渲染进程的console.log**

主进程的console.log()是打印到终端的，也就是说是打印到服务器上的；

渲染进程中的console.log()是打印到浏览器上的。

**预加载脚本**

预加载脚本在渲染器进程加载之前加载，并有权访问两个渲染器全局(如window和document)和nodejs环境。

### 4. 打包发布应用程序

Electron支持几种打包工具：

1. electron-forge

2. electron-builder

3. electron-packager

Electron建议使用Electron Forge，因为简单易上手，并使用Electron Forge的import指令设置Forge脚手架。

<font color="#f20">Electron-forge只能打本系统的包，比如mac上就只能打mac应用的包，而不能在mac上打包windows应用的包。这一点electron文档上没有告诉我们，明显的一个坑。</font>这个坑，害我用了1天的时间去调试、解决打包的问题。

```bash
npm install @electron-forge/cli --save-dev
npx electron-forge import
```

安装了electron-forge/cli后，项目的启动脚本就会被指定为electron-forge,package.json中的start指令由electron .变成了electron-forge start，然后添加forge的make指令。

**通过Forge的make指令打包可分发的应用程序**

```bash
npm run make
```

执行了make指令后，会在项目的根目录下创建一个out目录，打包后的应用呢程序就会被打包到这个目录。

在安装了electron-forge/cli后，package.json发生了一些变化，主要是electron-forge/cli的相关依赖和配置，大概的信息如下:

```json
  "devDependencies": {
    "@electron-forge/cli": "^6.0.0-beta.65",
    "@electron-forge/maker-deb": "^6.0.0-beta.65",
    "@electron-forge/maker-rpm": "^6.0.0-beta.65",
    "@electron-forge/maker-squirrel": "^6.0.0-beta.65",
    "@electron-forge/maker-zip": "^6.0.0-beta.65",
    "electron": "^20.0.2"
  },
  "dependencies": {
    "electron-squirrel-startup": "^1.0.0"
  },
  "config": {
    "forge": {
      "packagerConfig": {},
      "makers": [
        {
          "name": "@electron-forge/maker-squirrel",
          "config": {
            "name": "electron"
          }
        },
        {
          "name": "@electron-forge/maker-zip",
          "platforms": [
            "darwin"
          ]
        },
        {
          "name": "@electron-forge/maker-dmg",
          "platforms": [
            "darwin"
          ]
        },
        {
          "name": "@electron-forge/maker-deb",
          "config": {}
        },
        {
          "name": "@electron-forge/maker-rpm",
          "config": {}
        }
      ]
    }
  }
```
从代码中，我们看到了maker-zip、maker-deb、maker-rpm等依赖，配置(config)中有一个makers字段，这个字段是一个数组，配置了需要打包的终端类型，这是打包的核心配置。

**配置应用背景图片**

不应该叫背景图片，应该是应用的logo吧。

#### 4.1 打包dmg格式应用

我们在安装electron-forge/cli的时候，默认的安装了一些依赖，我用的是mac，我这默认安装了maker-zip、maker-rpm、maker-deb等，但是默认只能打包mac系统下的zip格式，在mac系统中，最有好的安装包格式是dmg格式，我们可以在安装一个maker-dmg依赖，然后配置下makers就可以实现

```bash
npm install @electron-forge/maker-dmg --save-dev
```
然后配置makers:

```json
        {
          "name": "@electron-forge/maker-dmg",
          "config": {
            "name": "An+" // 可以是中问,应用名
          },
          "platforms": [
            "darwin"
          ]
        },
```

然后就可以执行npm run make来打包应用了。

**打包生成不同平台的应用**

原本我是以为可以在一个开发平台如mac上可以直接生成各个平台终端的应用，如在mac上可以直接打包生成windows、linux上等各个不同终端的应用，最后了解到，这是不可能的，只能在各类的平台上打开项目的源代码，然后打包生成对应平台的可执行文件。

虽然这是一种解决办法，但是这是一种最低效、最没有技术含量的一种方案。

因为打包生成各平台的可执行应用，需要各种平台的环境支持，那么mac上就不会有windows的环境，同样，windows上也不会有mac上的应用的环境。即便同是mac的Intel芯片的终端和M1芯片的终端的环境都是不同的。

<font color="#f20">这些是存在的现象和问题，但是作为开发人员，公司也不太可能给我们每个人都配置多台设备，那么对于开发有好来说，还是希望能够在一台设备上可以打包成各个终端的不同应用。</font>

> 插播一个小知识：mac平台上Homebrew更新： brew update, brew自己本身更新

#### 4.2 使用electron-forge在mac上打包windows应用

上面已经了解到，mac上是不能直接打包windows应用的，因为需要windows应用的执行环境，所以我们需要在mac系统上安装一些windows应用的执行环境。

mac上需要的windows应用的执行环境有：wine、mono。

在mac上的electron应用中打包windows应用程序，需要先安装这2个依赖。

**wine**

wine，是Wine Is Not an Emulator首字母的缩写，Wine不是一个模拟器。它是一个能够在多个操作系统上运行windows应用的兼容层。wine不像虚拟机或者其他模拟器一样模仿内部的windows逻辑，而是将windows API调用翻译成为动态的POSIX调用，免除了性能和其他一些行为的内存占用，让我们能够让干净的集合windows应用到我们非windows系统的桌面。

总之，wine就是一个兼容层，可以在非windows系统上运行windows应用程序。

wine的安装:

```bash
brew install wine
```

通过brew安装wine正常情况下很少出问题，如果抱异常信息了，更新下brew就可以了。

更新brew的方式：

```bash
brew update # brew update 更新brew自己本身，不是更新通过brew安装的应用
```
> 因为很多源的服务器是国外的，部分情况下可能出现更新速度慢，或者失败的场景，这个是，就想办法解决下网络问题，或者更信下源。

**mono**

一个跨平台的.net运行环境，可以运行在mac、linux等终端上。

安装mono就有点麻烦了，在网上查到了也可以通过brew来安装mono，但是我尝试直接使用brew install mono，结果都失败了，提示需要将Homebrew的安装目录移动到/usr/local目录下(我使用的M1的mac，homebrew默认被安装到了/opt/homebrew,Intel版本的Mac好像是被安装到/usr/local目录下的)，或者是使用‘arch -arm64 brew install 应用名’的方式安装，我进行了尝试后，提示没有mono这个源。

![没有找到mono的源](./images/i2.png)

另外一种方式就是下载mono安装文件的方式安装，下载地址：https://www.mono-project.com/download/stable/#download-mac。

这种方式安装成功了。

> wine和mono都安装成功了，但是在通过electron-forge打包windows应用的时候，还是没有成功。

> 使用electron-forge只能在各自的平台上进行对应平台的应用程序，就是说在mac上只能打包mac系统的应用程序，在windows上只能打包windows平台的应用程序，而不能在mac上打包windows平台的应用程序.
### 5. 常用功能

1. 获取设备mac地址

可以通过getmac获取mac

2. 多标签页功能

electron原生本身不提供多标签页功能，但是可以通过其他的一些变通的方式获取来实现多标签页功能。

3. 预定义功能

在electron的菜单中，role属性包含了一些预定义功能，有些功能直接使用role就可以实现，不再需要触发click事件去实现了.具体的role属性，可参考：https://www.electronjs.org/docs/latest/api/menu-item#menuitemrole

![菜单role属性](./images/i3.png)

```js
    {
        label: '&Edit(E)',
        submenu: [
            {
                label: '剪切',
                role: 'cut'
            },
            {
                label: '复制',
                role: 'copy'
            },
            {
                label: '粘贴',
                role: 'paste'
            }
        ]
    },
```

4. 主菜单

在MacOS中，无论我们设置什么标签，应用菜单的第一个菜单项的标签始终是我们的应用的名字。要想修改的话，只能通过修改应用绑定的Info.plist文件来修改应用的名字。