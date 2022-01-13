### complete:13: command not found: compdef

今天在修改.zshrc文件的时候，需要重新加载，于是我就正常的执行source ./.zshrc，结果报异常了：

```bash
axx@xxx ~ % source .zshrc 
complete:13: command not found: compdef
```

解决办法也很简单，只需要在.zshrc文件的最顶部加上两行代码就可以了：

```bash
# 添加下面两行代码，解决compdef报错的问题
autoload -Uz compinit
compinit
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
export PATH=/opt/homebrew/bin:$PATH
```

具体的解决办法已经给出，具体的原因，可以参考：

https://juejin.cn/post/6999433693626368013

https://apple.stackexchange.com/questions/296477/my-command-line-says-complete13-command-not-found-compdef