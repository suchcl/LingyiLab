### curl: (7) Failed to connect to raw.githubusercontent.com port 443: Connection Refused

今天在安装nvm的时候，指令如下：

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```

结果提示我：curl: (7) Failed to connect to raw.githubusercontent.com port 443: Connection Refused。

解决方案：

可以参考下[https://blog.csdn.net/gitblog_06549/article/details/143383819](https://blog.csdn.net/gitblog_06549/article/details/143383819)

我是通过修改DNS，更改了DNS服务，更改为Google的公共DNS:8.8.8.8、8.8.4.4，或者阿里云的DNS:223.5.5.5、223.6.6.6