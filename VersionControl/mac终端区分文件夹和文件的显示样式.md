### mac终端区分文件夹和文件的样式

新mac设备，通过ls查看文件列表的时候，发现无论是文件夹还是文件，统统白乎乎的一片，没有办法区分哪个是文件夹哪个是文件，没有辨识度。所以得需要对我的环境进行一下配置，提升对我的设备的使用体验度。

<img src="./images/i13.png" width="600" />

```bash
# 如果使用的终端是bash，可以通过下面的指令
# 打开.bash_profile

vi ~/.bash_profile

# 在文件底部新增下面两行代码
export CLICOLOR=1
export LSCOLORS=CxFxExDxBxegedabagacad

# 重新加载.bash_profile
source ~/.bash_profile

# 如果使用的是终端是zsh

# 如果已经配置过.bash_profile,则可以直接在zsh的配置文件中导入.bash_profile
vi ~/.zshrc

# 在.zshrc文件底部导入.bash_profile
source ~/.bash_profile
# 重载配置文件
source ~/.zshrc

# 也可以直接在.zshrc中配置
export CLICOLOR=1
export LSCOLORS=CxFxExDxBxegedabagacad
# 重载配置文件
source ~/.zshrc
```

然后再执行ls的时候，文件夹和文件类型已经有了区分了

<img src="./images/i14.png" width="600" />