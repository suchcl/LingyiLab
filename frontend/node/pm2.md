### pm2

参考链接:[https://shipengqi.github.io/PM2-docs-Zh-CN/](https://shipengqi.github.io/PM2-docs-Zh-CN/)

pm2是一个node.js应用程序的进程管理器，通过pm2可以帮助开发人员轻松的管理和维护node.js在服务器环境中运行。

### 常用指令

```bash
pm2 list # 查看服务列表

pm2 start app # 启动一个服务, pm2 start bin/www

pm2 start app --name 'appname' # 启动一个服务并为该服务指定一个应用名，便于管理

pm2 restart app #重启服务，pm2 restart bin/www

pm2 stop app # 停止服务， pm2 stop bin/www

pm2 delete id # 删除指定id的服务

pm2 delete app # 删除指定应用名称的服务

pm2 logs # 查看日志,所有的

pm2 logs app # 查看指定服务的日志

pm2 monit # 服务监控

pm2 show app # 查看指定服务的状态信息
```

pm2的日志，可以保存本地文件，本地文件可以自定义配置，也可以使用默认文件。