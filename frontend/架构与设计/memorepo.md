### 1. 什么是memorepo？

Memorepo是项目管理的一种方式，指在一个项目仓库(repo)中管理多个模块/包(package)，和现在常见的每个模块、小项目、模块都创建一个项目仓库的代码管理方式不同。

目前有很多项目都采用了Memorepo的项目管理方式，如Vue(vue2、vue3)、react、react-react-app、babel等

> 还有其他一些项目，接下来需要再调研、详列。

一般情况下，使用memorepo代码管理方式的目录结构为：

```markdown
projectName
├─lerna.json
├─package.json
├─tree.md
├─packages
|    ├─pkg2
|    |  └package.json
|    ├─pkg1
|    |  └package.json
```

与memorepo代码管理方式相对的就是multirepo(多repo项目，以及现在的微前端)，会将一个大的项目根据职责、业务模块进行划分，然后创建不同的代码仓库进行管理。不同的团队可以专注于负责某个具体的代码仓库进行代码的提交、编译、发布等代码管理工作。

### 2. memorepo的优势

1. 可以看到所有代码，其他项目有了新的提交后就立刻可以被看到；

2. 便于协同工作；

### 3. memorepo的不足