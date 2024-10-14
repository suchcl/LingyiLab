umi4中,服务启动默认端口号为8000

### 修改端口号

如果由于某些原因,需要修改umi项目服务的端口号,可以参考如下几种方式:

1. 根目录下创建.env文件,可以通过.env文件来配置一些环境变量和功能.

```bash
PORT=3000
```

2. 通过修改scripts脚本来指定端口号

```json
"scripts": {
    "dev": "PORT=3002 umi dev", // mac、linux
    "dev": "set PORT=3002 && umi dev", // windows, 文档上这样介绍,没有实际测试
  },
```

3. 通过cross-env在scripts中指定端口号

```bash
# 安装cross-env依赖
npm install cross-env -D
"scripts": {
    "dev": "cross-env PORT=3002 umi dev"
},