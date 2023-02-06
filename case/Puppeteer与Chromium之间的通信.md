### Puppeteer与chromium之间的通信

参考链接:https://juejin.cn/post/7194745887011602487

#### 1. 什么是Puppeteer？

参考链接:https://puppeteer.bootcss.com/

Puppeteer是一个nodejs库，它提供了一个高级API来通过DevTools协议控制Chromium或Chrome。Puppeteer默认以headless模式运行，但是也可以通过配置来运行“有头”模式。

**Puppeteer能做什么？**

我们可以在浏览器中通过手动完成的大部分操作都可以通过Puppeteer来完成。如下面一些场景:

1. 生成页面PDF

2. 抓去SPA并生成预渲染内容

3. 自动提交表单，进行UI测试，键盘输入等

4. 创建一个时时更新的自动化测试环境。使用最新的javascript和浏览器功能直接在最新版本功能的chrome中执行测试

5. 捕获网站的timeline trace，用来帮助分析性能问题

6. 测试浏览器扩展



