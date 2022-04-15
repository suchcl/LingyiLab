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

参数：

--independent / -i 使用独立的版本控制方式

```bash
lerna init -i # 初始化一个一个lerna项目，且使用独立的版本控制方式
```

参数可以省略，不是必须的

指令：lerna bootstrap

lerna bootstrap 在当前的Lerna仓库中执行引导流程(bootstrap).安装所有依赖项并链接任何交叉依赖。

这个命令比较重要。

> 补充个小知识点：repo：看到这个单词的时候，意识很明确的就是仓库、代码库的意思了，但是在一些技术群中、社区中发现有人在问repo是什么？其实这就是个英文单词，汉语我们直接说代码库，有的人喜欢说英语，就说repo，感觉和国际接轨了，就是这个意思。