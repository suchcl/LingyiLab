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

**一个Electron应用只能有一个主进程，但是可以有多个渲染进程。**

electron应用中，不能在主进程中(可以简单理解不能在main.js)访问、编辑DOM，因为它无法访问渲染器文档上下文，它们存在于不同的进程中。

### 4. 常用功能

1. 获取设备mac地址

可以通过getmac获取mac

2. 多标签页功能

electron原生本身不提供多标签页功能，但是可以通过其他的一些变通的方式获取来实现多标签页功能。