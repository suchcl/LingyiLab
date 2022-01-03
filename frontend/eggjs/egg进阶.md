### 1. Egg基本介绍

Egg遵循“约定优于配置”的原则，适合团队开发。当然了，个人开发也可以用。

### 2. 项目创建

以npm为例

```bash
# 可以通过create指令
npm create egg --type=simple

# 也可以通过init指令
npm init egg --type=simple
```

使用npm创建egg项目的两种方式，都可以，创建出来的项目，是完全相同的。

运行项目：

根据项目创建完成后的提示信息

```bash
- cd D:\EggPro\egg1
- npm install
- npm start / npm run dev / npm test
```

也可以使用yarn来创建项目

```bash
yarn create egg --type=simple
```

使用yarn和npm没有太大的区别，我习惯使用npm，后面的案例，都以npm为例，不再单说yarn了。

### 3. egg和express/koa的区别

| 特征对比                    | Egg.js                                 | Express/Koa              |
| --------------------------- | -------------------------------------- | ------------------------ |
| 代码规范性：（MVC开发模式） | 符合MVC模式：Controller、Service、View | 灵活编码，没有明确的规范 |
| 学习成本                    | 中                                     | 易                       |
| 创建机制/扩展机制           | 有                                     | 无                       |
| 多线程管理                  | 有                                     | 无                       |
| HttpClient集成              | 有                                     | 无                       |

