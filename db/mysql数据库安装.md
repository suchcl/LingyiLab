### 1. mysql数据库安装及环境配置

mac上安装mysql，我常用的有两种方式，一种方式是使用Homebrew，一种是直接下载dmg安装文件安装。

**安装文件安装**

下载链接：https://dev.mysql.com/downloads/mysql/

<img src="./images/i1.png" alt="mysql安装包有arm版本和x86版本的" width="650" />

最新的Mac M1芯片的是ARM架构的，如果有显示是Intel的，就下载x86版本的安装包。

下载后双击安装文件安装，一路“继续”就可以了

![mysql安装文件安装](./images/i2.png)

安装的过程中可能需要输入电脑账号，根据需要输入就可以了.

安装过程中还会让选择密码方案，是选择加强的加密方案，还是常规的加密方案，我选择了默认的加密方案：加强的加密方案，加强的加密方案，就是设置密码要复杂一点，同时使用数字、字母组合。没有把图片给截下来，遗憾了。

设置好密码后点击finish，继续下一步就可以了。

安装成功后，在设置面板中会有一个mysql的设置入口。

![设置中的mysql设置入口](./images/i3.png)

点击入口，打开mysql的管理窗口

![mysql管理窗口](./images/i4.png)

**通过Homebrew安装**

https://blog.csdn.net/weixin_34026997/article/details/113579589?utm_term=mac%E6%9F%A5%E7%9C%8B%E6%98%AF%E5%90%A6%E5%AE%89%E8%A3%85%E4%BA%86mysql&utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~all~sobaiduweb~default-1-113579589&spm=3001.4430

### 2. 服务管理

#### 2.1 查看服务状态

#### 2.2 开启服务


#### 2.3 停止服务

#### 2.4 重启服务

### 3. mysql客户端工具

常用的有Navicat，但是它收费的，如果是个人使用，网上有破解方法；如果是工作使用，就企业购买正版吧，支持正版。

如果使用vscode作为编辑器的话，可以安装mysql插件，因为我不是专职DBA，vscode插件已经基本满足了我的需求了。

### 4. mysql基础指令