### node版本管理工具NVM

前端开发中，经常会有需要使用不同node版本的情况，使用nvm就很好的帮我们解决了整个问题

> 还有另外一个工具n也可以帮助我们实现管理不同node版本的问题，但是我还是喜欢使用nvm.想了解和n的不同请参考[node版本管理工具nvm和n的区别](nvm和n的不同.md)

nvm原来只有linux版本(Mac版本)，是没有window版本的，后来有了另外一个团队又开发了nvm的windows版本。

[linux版本nvm](https://github.com/nvm-sh/nvm)

[windows版本nvm](https://github.com/coreybutler/nvm-windows)

nvm常用命令

```bash
nvm ls 已经安装的nodejs版本列表

nvm ls-remote：linux(mac)版本的查看远程服务器可用的nodejs列表

nvm ls available：windows版本查看远程服务器的可用的nodejs列表
```