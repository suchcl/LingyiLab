<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1.认识lerna](#1%E8%AE%A4%E8%AF%86lerna)
- [2.快速开始](#2%E5%BF%AB%E9%80%9F%E5%BC%80%E5%A7%8B)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1.认识lerna

lerna是一个用于管理多个软件包(packages)的javascript项目的包管理工具.

lerna是一个可以对使用git和npm管理多软件包代码仓库的工作流程进行优化的工具。

### 2.快速开始

1. 全局安装lerna

```bash
npm install lerna -g  # 现在推荐2.x版本
```

2. 创建一个新的lerna项目

指令：

lerna init

进入到lerna项目目录后，执行lerna init，可以将当前目录初始化为一个lerna项目

```bash
mkdir lerna
lerna init
```

将当前的lerna目录初始化成了一个lerna项目目录，最初的lerna项目目录结构：

```markdown
axxx@xxxxx lerna % tree ./
./
├── README.md
├── lerna.json
├── package.json
└── packages
```

到现在为止，一个简单的lerna项目，已经创建完成。