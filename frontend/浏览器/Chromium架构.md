### Chromium架构

我们知道js是一门单线程语言，但是浏览器是一个多线程的，同理，Chromium作为chrome的体验版，Chromium也是多线程的工作机制。参考链接：https://www.chromium.org/developers/design-documents/multi-process-architecture/。

![Chromium多线程工作机制](./images/i3.png)

Chromium多进程的管理机制，在这个机制中，我们将运行UI并管理其他渲染器的进程称之为主进程或者浏览器进程，也称为浏览器；处理web网页内容的进程，称为渲染进程，有时也被称为渲染器。渲染器使用Blink开源布局引擎来解释和布局HTML。

Chromium的多进程模式主要由三大部分组成：浏览器端、渲染器端和浏览器与渲染器之间的通信方式(IPC).

