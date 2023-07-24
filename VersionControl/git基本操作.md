1. 拉取代码

```bash
# 拉取代码
git pull
```

2. 提交代码

```bash 
# 提交代码 在git做提交操作的时候， 必须要有注释
git commit -m "提交注释"
```

3. 撤销git merge

```bash
# 查看提交日志
git log

# 回退到某个某个指定的版本号
git reset --hard [版本号]
```

4. 通过git命令行查看当前git仓库的远程仓库地址

```bash
git remote -v # 查看当前git仓库远程仓库的地址

git remote get-url <remote> # remote是远程仓库的名称，大多数情况下为origin，所以可以直接通过下面指令查看当前git仓库的远程服务器地址

git remote get-url origin
```

