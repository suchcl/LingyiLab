### volta,node版本管理工具,允许在不同的项目中使用不同的node版本,且支持node版本切换

volta是一个node的版本管理工具,允许我们在不同的项目中使用不同版本的node,且支持node的版本切换的工具.

**相关文档**

官网: [https://docs.volta.sh/](https://docs.volta.sh/)

Github:[https://github.com/volta-cli/volta](https://github.com/volta-cli/volta)

### 开始使用

```bash
# 安装
curl https://get.volta.sh | bash
# 安装后重启命令行工具生效

# 安装指定版本的node
volta install node@18.18.0

# 在当前项目中锁定包版本
volta pin node@14.16.0 # 当前项目将会锁定14.16.0这个版本,并且会在package.json中添加volta配置项
volta pin yarn@1.22.18
```

```json
	"volta": {
		"node": "14.16.0",
		"yarn": "1.22.18"
	}
```

### 使用volta管理包的依赖

项目中使用了volta以后,项目中npm包的管理就可以通过volta来管理

```bash
# 安装
volta install package
# 卸载
volta uninstall package

# 安装不需要指定精确版本的包
volta install node@14 # volta会装一个大版本为14的node,但是精确版本volta会根据自己的判断来选一个合适的版本
# 安装精确的版本
volta install node@14.16.0 # 安装一个精确的指定版本

# 查看当前项目中使用volta管理的工具列表
volta list
```

项目中没有安装volta,则会使用最新的全局的包来进行项目的管理.

**切换node版本**

volta并没有提供显示切换node版本的指令,不过可以通过volta pin指令来实现版本切换的目的.

> volta就是指定package版本的作用,随说不是切换版本的功能,但实现了版本切换的目的.

### 和nvm的区别

|                              | nvm                                                       | volta                                                    |
| ---------------------------- | --------------------------------------------------------- | -------------------------------------------------------- |
| 默认安装                     | 当前标签页生效                                            | 全局生效                                                 |
| 对其他标签命令行是否时时生效 | 默认只对当前标签页生效,打开的新标签会使用新安装的node版本 | 已经打开的标签也会时时生效,使用新安装的node版本          |
| 范围                         | 全局生效                                                  | 项目级别的node版本管理                                   |
| 支持package.json配置         | 不支持                                                    | 支持,通过package.json中的配置,实现项目级别的node版本管理 |

volta感觉是比nvm更加灵活,nvm管理全局,volta可以精确到当前项目.

### 默认版本

通过volta install node@16.16.0 方式安装的node版本就是node的全局版本

具体的项目中node版本,可以通过前面介绍的pin指令来锁死当前项目需要使用的node的版本.