### remote: Support for password authentication was removed on August 13, 2021

今天在github上新建了一个项目，然后根据提示新建一个readme.md并且提交，但是提交的时候失败了，报错了，主要的报错信息是鉴权失败，原因是在2021年的8月13日移除了密码鉴权功能。

```bash
[xxxxxx xxxxx (master)]$ git push -u origin master
Username for 'https://github.com': xxxx
Password for 'https://xxxx@github.com': 
remote: Support for password authentication was removed on August 13, 2021.
remote: Please see https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories#cloning-with-https-urls for information on currently recommended modes of authentication.
fatal: 'https://github.com/xxxx/xxxxxxxx.git/' 鉴权失败
```

之前使用github，在命令行操作的时候，都是通过账号、密码鉴权，但是今天突然发现账号、密码鉴权不醒了，失败了，给出了报错，且提示鉴权失败。去年的时候有创建过新的项目，使用账号、密码鉴权是没有问题的，而我看到提示信息是从2021年的8月13号就已经移除掉了，也从网上看到一些信息有人从2021年的8月份就开始提示这个信息了。可能是github存在功能灰度期吧。

### 问题解决

根据提示，查看https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories#cloning-with-https-urls，原来鉴权机制变了，之前是密码鉴权，从2021年8月13日开始变成了个人访问令牌(personal access token)鉴权了，就是通过personal access token替换掉密码.

### 那么为什么要使用personal access token呢，它相对密码来说有什么优势吗？

更多的应该还是安全优势吧，虽然这个最重要，但是日常中我确实是没有怎么重视过，自己应该做个检查了。

1. 唯一: 令牌特定于github，

2. 可撤销:

3. 有限:

4. 随机:

### personal access token的类型

Github当前支持两种类型的personal access token：fine-grained personal access token和personal access token(classic).

Github建议尽可能的使用fine-grained personal access token，而不是去使用personal access token(classic).

所有的fine-grained personal access token和personal access token(classic)都和生成它们的用户相关联，如果用户失去了对资源的访问权限，则该token就会变成非活跃状态，也会失去对资源的访问权。

### 什么场景下才会需要个人令牌(personal access token)鉴权呢？

当使用HTTPS的方式连接远程仓库的时候，需要使用个人令牌(personal access token)的鉴权方式(2021年8月13日之后，之前可以使用账号、密码的鉴权方式)；当使用ssh的方式连接远程仓库的时候，不需要使用个人令牌的方式鉴权，ssh的连接方式使用ssh keys的鉴权方式。

现在可以回答我上面提到过的一个问题了，为什么我去年创建的github仓库没有使用个人令牌去鉴权，原因是我那会使用的ssh的连接方式。

### 生成个人令牌(personal access token)

