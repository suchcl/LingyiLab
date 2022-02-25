### nrm简单认识

nrm是一个js模块，一个可以通过命令行来切换npm镜像源的命令行工具。

```bash
# nrm安装----全局安装
npm install nrm -g

# 查看可选的nrm镜像源
nrm ls

# 切换npm镜像源
nrm use cnpm # 切换为使用cnpm镜像源

# 添加npm源
nrm add taobao https://registry.npmmirror.com  # 增加一个名为taobao源为https://registry.npmmirror.com的镜像

# 移除镜像源
nrm del taobao # del指令只能删除自定义的镜像源，如果是nrm内置的，则不能删除
```

### 常用指令

