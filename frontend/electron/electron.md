### 1. 简单认识Electron

Electron是一个使用javascript、html、css构建桌面应用程序的框架。嵌入Chromium和nodejs到二进制的Electron应用程序，允许使用一套js代码库创建跨平台的桌面应用程序。

Electron应用程序的开发，需要本地有nodejs的支持，但是Electron应用程序的运行，不依赖本地的Nodejs和浏览器。

**Nodejs**

Electron应用程序的开发以来nodejs，所以在开发Electron应用之前，本地需要先安全nodejs，且建议是最新版本的TLS版本。

Electron应用程序，将nodejs打包到了Electron应用的二进制文件中，所以我们运行Electron应用时的nodejs和我们本地开发环境中的nodejs版本没有任何关系。

### 2. 管理窗口的生命周期

#### 2.1 关闭所有窗口时退出应用程序

在windows和linux中，关闭了所有的窗口后，通常就是退出了一个应用，但是在Macos中则有不同的表现，所以需要手动设置在关闭了所有的窗口后去退出一个应用程序。

```js
// 监听window-all-closed事件
app.on("window-all-closed", () => {
    if(process.platform !== "darwin"){
        app.quit();
    }
});
```

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