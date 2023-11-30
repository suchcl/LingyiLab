### 开发工具

yeoman、generator-eslint，全局安装即可。

环境要求：
```js
Node.js ^14.17.0 || ^16.0.0 || >= 18.0.0
```

环境安装：

```bash
npm install yo generator-eslint -g
```

创建eslint插件项目

```bash
# 创建目录
mkdir eslint-plugin-et
# 初始化项目
yo eslint:plugin
```

创建新的eslint规则

```bash
yo eslint:rule
```

### 基础知识

通过yo创建的eslint项目的结构如下：

```markdown
eslint-plugin-et
├─.eslintrc.js
├─README.md
├─package-lock.json
├─package.json
├─tests
|   ├─lib
|   |  ├─rules
|   |  |   └no-html-tags.js
├─lib
|  ├─index.js
|  ├─rules
|  |   └no-html-tags.js
├─docs
|  ├─rules
|  |   └no-html-tags.md
```

主要的是lib目录中rules下的no-html-tags.js文件，该文件是规则的源文件,需要重点关注。

下面来主要分析下该规则文件:

```js
"use strict";
/** @type {import('eslint').Rule.RuleModule} */
module.exports = {
  meta: {
    // messages字段元信息是脚手架没有生成的，需要手动添加下，否则项目会提示：`meta.messages` must contain at least one violation,就是说至少要有一个异常提示信息
    messages: {
      someMessageId: "使用了html标签了",
    },
    type: "problem", // `problem`, `suggestion`, or `layout`
    docs: {
      description: "检测html标签的使用情况",
      recommended: false,
      url: null,
    },
    fixable: null,
    schema: [],
  },

  create(context) {
    return {
      // 下面代码是脚手架没有生成的，需要手动添加一下
      CallExpression(node) {
        context.report({
          node,
          messageId: "someMessageId",
        });
      },
    };
  },
};
```

可以从文件中看到规则主要就是包含了一个meta对象和一个create函数，mate主要包含了规则的元数据，create函数返回一个访问器对象,该对象的属性为选择器，ESLint在遍历Javascript代码的抽象语法树时会执行所有监听了该选择器的回调函数，