### Chromium架构

我们知道js是一门单线程语言，但是浏览器是一个多线程的，同理，Chromium作为chrome的体验版，Chromium也是多线程的工作机制。参考链接：https://www.chromium.org/developers/design-documents/multi-process-architecture/。

![Chromium多线程工作机制](./images/i3.png)

Chromium多进程的管理机制，在这个机制中，我们将运行UI并管理其他渲染器的进程称之为主进程或者浏览器进程，也称为浏览器；处理web网页内容的进程，称为渲染进程，有时也被称为渲染器。渲染器使用Blink开源布局引擎来解释和布局HTML。

Chromium的多进程模式主要由三大部分组成：浏览器端、渲染器端和浏览器与渲染器之间的通信方式(IPC).

1. 主进程

主进程，也叫浏览器进程，一个应用中只有一个主进程。应用打开，主进程启动。主进程为每个渲染进程维护对应的RenderProcessHost，负责主进程与渲染进程的交互。

RenderViewHost则与RenderView对象进行交互，渲染网页内容，主进程与渲染进程通过IPC进行通信。

2. 渲染进程

每个渲染进程都有一个全局的RenderProcess对象，可以管理当前渲染进程和主进程之间的通信，并维护其全局状态。

3. view管理

每个渲染进程可以维护多个RenderView对象，当新开标签页或弹出窗口后，渲染进程就会创建一个RenderView对象，Renderview对象与它在主进程中对应的RenderViewHost和Webkit嵌入层通信，渲染网页内容。