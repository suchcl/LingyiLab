### 基于一个指定分支创建一个新分支的过程

> 如果没有特殊说明，本文档所有的操作都指命令行操作，如果是客户端操作，客户端会帮助我们做完这些工作，我们可能会感知不到。

以案例的形式来讲解吧：如基于master分支创建一个开发分支dev。

1. 切换到master分支

```bash
git checkout master
```

2. 拉取代码，保证master分支代码为最新代码

```bash
git pull
```

3. 基于master分支创建新的分支dev(也称为复制master分支的副本)

```bash
git checkout -b dev
```

4. 将本地新创建的dev分支推送到服务器端

```bash
git push origin dev
```

5. 将本地dev分支和服务端dev分支做关联

```bash
git push --set-upstream origin dev
```

6. 测试是否连接成功（只要测试下是否可以正常拉取代码即可）

```bash
git pull
```


### branch的相关操作

```bash
git branch # 查看本地分支列表
git branch -r # 查看远程的服务器分支列表
git branch -a # 查看本地和远程所有分支列表
git checkout branchname  #切换到分支branchName
```