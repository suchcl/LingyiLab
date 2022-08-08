### 1. 简单认识Electron

Electron是一个使用javascript、html、css构建桌面应用程序的框架。嵌入Chromium和nodejs到二进制的Electron应用程序，允许使用一套js代码库创建跨平台的桌面应用程序。

Electron应用程序的开发，需要本地有nodejs的支持，但是Electron应用程序的运行，不依赖本地的Nodejs和浏览器。

**Nodejs**

Electron应用程序的开发以来nodejs，所以在开发Electron应用之前，本地需要先安全nodejs，且建议是最新版本的TLS版本。

Electron应用程序，将nodejs打包到了Electron应用的二进制文件中，所以我们运行Electron应用时的nodejs和我们本地开发环境中的nodejs版本没有任何关系。

### 2. 生命周期

Electron和vue、react应用程序类似，也有自己的生命周期。

