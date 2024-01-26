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
```


### 和nvm的区别

|                              | nvm                                                       | volta                                                    |
| ---------------------------- | --------------------------------------------------------- | -------------------------------------------------------- |
| 默认安装                     | 当前标签页生效                                            | 全局生效                                                 |
| 对其他标签命令行是否时时生效 | 默认只对当前标签页生效,打开的新标签会使用新安装的node版本 | 已经打开的标签也会时时生效,使用新安装的node版本          |
| 范围                         | 全局生效                                                  | 项目级别的node版本管理                                   |
| 支持package.json配置         | 不支持                                                    | 支持,通过package.json中的配置,实现项目级别的node版本管理 |

**volta**

默认全局安装

如果安装时默认打开了多个命令行标签,则其他标签也会同时使用最新安装的node版本