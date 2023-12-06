### 1. 简单认识ESLint

文档：https://eslint.nodejs.cn/

ESLint常用在静态代码扫描中，通过设置eslint语法规则，对代码进行静态检查，通过规则来约束代码的风格，以此来提高代码的健壮性、可读性，可以有表避免一些由于代码不规范而导致出现bug的可能。

规则是自由的，每个团队都可以有自己的规则，也可以直接使用开源社区中一些比较热门的规则集合，如airbn、eslint-plugin-vue、eslint-plugin-react等等，社区中有很多非常优秀的、开源的eslint规则。

![社区中优秀的开源eslint规则](./images/i9.png)

### 2. ESLint配置

eslint的配置，通常是使用.eslintrc.js或者.eslintrc来配置的，也可以直接在package.json中定义eslintConfig的属性。

![eslint主要配置](./images/i10.png)

<img src="./images/i10.png" width="300" />

#### 2.1 parse

parse用来定义eslint所使用的解析器，eslint默认使用的是Espree(https://github.com/eslint/espree)