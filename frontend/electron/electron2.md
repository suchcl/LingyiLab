### 1.再认识electron

electron的组成

electron = chromium + nodejs + Native API

可参考如下的图片：

![electron组成](./images/i6.png)

electron的能力和chromium和nodejs密不可分,因为electron的很大一部分的功能就是在chromium和nodejs的基础上实现的。

electron难点：

1. 技术栈较多：C++、多进程、rust

2. 工程化建设

与传统web开发的一些区别

1. 主进程和渲染进程

2. 进程间通信

3. Native能力和原生GUI

4. 释放前端的想象能力

需要进阶掌握的技能点

1. 打包

2. 软件更新

3. 质量监控

4. 保证应用安全

5. 提升用户体验

6. Electron bad part

**都谁在用electron**

**什么时候适合使用electron**

在做一些小范围项目，可快速验证效果的场景下；

一些特定领域，如开发者工具、效率应用工具的时候，可以尝试使用electron

**怎么使用electron**

### Electron进程间通信

**electron应用中进程之间通信的目的/为什么要通信**

事件通知

数据传输

数据共享

**IPC模块通信**

Electron提供了IPC通信模块，主进程的ipcMain和渲染进程的ipcRenderer

ipcMain、ipcRenderer都是EventEmitter对象

**进程间的通信，从渲染进程到主进程**

callback方式

    ipcRenderer.send(channel,...args)   渲染进程向主进程发送一个事件，并可以传递一些数据(参数，非必填，可选)

    ipcMain.on(channel,handler)   主进程监听从从渲染进程发送的事件，并向渲染进程返回一个结果

Promise写法(electron7.0之后，处理请求+响应模式)

    ipcRenderer.invoke(channel,...args);

    ipcMain.handle(channel,handle);
