### Mac开发环境搭建

主要是前端开发环境搭建

#### Homebrew的安装

官网链接：[https://brew.sh/](https://brew.sh/)

安装:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

#### 编辑器安装

常用的编辑器有vscode和Cursor

1. vscode安装和配置

vscode是绿色应用，无需安装，下载解压后可直接使用。

mac中，最好是把下载后的应用移动到应用程序目录中，这样可以应用可以被添加到启动台中，之后就可以直接通过启动台来找应用去启动了。

**配置终端中通过code指令启动vscode**

mac作为开发者的利器，开发者离不开终端命令行工具，对于vscode来说，可以直接通过指令来启动。配置方式：

- 同时按下shift+command+p，打开命令面板,选择“Shell命令：在path中安装code命令”

<img src="./images/i24.png" width="600" />

然后就可以直接在终端命令行中通过执行code来启动vscode了。

也可以参考: [mac终端设置vscode快捷启动](./mac终端设置vscode快捷启动.md)

2. Cursor安装配置

#### host管理应用switchhosts安装


#### nvm安装

#### nrm安装

#### Git安装

1. git安装

git有多种安装方式，在mac中，最常用的是通过homebrew安装和安装包直接安装。

- 通过homebrew安装

- 下载安装文件直接安装

git没有提供单独针对M芯片的安装文件，而是通过集成xcode命令行工具去使用git。

2. 终端中显示分支名

- 在低版本的mac中，然后使用的bash，可以通过下列方式去修改

```bash
# 在bash的配置文件中末尾添加如下内容
vi ~/.bash_profile
function git_branch {
   branch="`git branch 2>/dev/null | grep "^\*" | sed -e "s/^\*\ //"`"
   if [ "${branch}" != "" ];then
       if [ "${branch}" = "(no branch)" ];then
           branch="(`git rev-parse --short HEAD`...)"
       fi
       echo " ($branch)"
   fi
}
export PS1='\u@\h \[\033[01;36m\]\W\[\033[01;32m\]$(git_branch)\[\033[00m\] \$ '
```

然后重载配置文件

```bash
source ~/.bash_profile
```

如果使用的是zsh，那么就在zsh的配置文件末尾添加上面的内容，然后重载下配置文件即可

```bash
vi ~/.zshrc
function git_branch {
   branch="`git branch 2>/dev/null | grep "^\*" | sed -e "s/^\*\ //"`"
   if [ "${branch}" != "" ];then
       if [ "${branch}" = "(no branch)" ];then
           branch="(`git rev-parse --short HEAD`...)"
       fi
       echo " ($branch)"
   fi
}
export PS1='\u@\h \[\033[01;36m\]\W\[\033[01;32m\]$(git_branch)\[\033[00m\] \$ '

# 重载配置文件
source ~/.zshrc
```

- 较新版本的mac系统中，上面的方式失效了，默认的终端也从bash改为了zsh，对于这些较新版本系统来说，可以使用下面的方式来修改配置

> 具体的系统版本好像是Big Sur吧

首先下载这个脚本到本地，可以存储到当前用户目录下，并命名为.git-prompt.sh

[https://gitcode.com/gh_mirrors/gi/git/blob/master/contrib/completion/git-prompt.sh](https://gitcode.com/gh_mirrors/gi/git/blob/master/contrib/completion/git-prompt.sh)

然后将下的配置添加到.zshrc文件的末尾

```bash
GIT_PS1_SHOWUPSTREAM="auto"
GIT_PS1_SHOWCOLORHINTS="yes"
source ~/.git-prompt.sh
setopt PROMPT_SUBST
PS1='[%n@%m %c$(__git_ps1 " (%s)")]\$ '
```

最后重载配置文件

```bash
bash ~/.zshrc
```

到此，mac终端应该就会正常显示分支名称了,看起来直观了，不用再担心修改错代码了。

<img src="./images/i25.png" width="300" />