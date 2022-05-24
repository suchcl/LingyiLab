<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [TC39、ECMA262、ECMAScript各是什么东西，以及它们之间的关系是什么？](#tc39ecma262ecmascript%E5%90%84%E6%98%AF%E4%BB%80%E4%B9%88%E4%B8%9C%E8%A5%BF%E4%BB%A5%E5%8F%8A%E5%AE%83%E4%BB%AC%E4%B9%8B%E9%97%B4%E7%9A%84%E5%85%B3%E7%B3%BB%E6%98%AF%E4%BB%80%E4%B9%88)
  - [ECMA262](#ecma262)
  - [TC39](#tc39)
- [ECMAScript发展的历史](#ecmascript%E5%8F%91%E5%B1%95%E7%9A%84%E5%8E%86%E5%8F%B2)
- [向后兼容](#%E5%90%91%E5%90%8E%E5%85%BC%E5%AE%B9)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### TC39、ECMA262、ECMAScript各是什么东西，以及它们之间的关系是什么？

#### ECMA262

ECMA International，是个行业标准组织，它所通过的标准都是ECMA-<nnn>这样的编号，然后可以有另外的名字。最初Javascript语言有2个标准：

1. ECMA-262：主标准，由ECMA国际组织(ECMA International)负责管理。为了让最初的javascript与最初的JScript能遵循同一套标准而诞生的ECMAScript，正好排到了作为Ecma的262号标准，就得到了ECMA-262的编号。

2. ISO/IEC 16262：第二标准，由国际标准化组织(ISO,International Organization for Standardization)和国际电子技术委员会(IEC,International Electrotechnical Commission)负责管理。

出于版权的原因，规范中将这门语言称为ECMAScript，所以原则上Javascript与ECMAScript指的是同一语言，但有的时候也会加以区分：

- Javascript：指ECMAScript标准语言的实现；

- ECMAScript：指语言标准及语言版本，如ES6指ECMAScript语言的第6个版本

#### TC39

TC39指的是技术委员会(Technical Committee)的第39号，一个推动javascript发展的委员会。它是ECMA的一部分，ECMA是ECMAScript规范下的Javascript语言标准化机构。

TC39，由各个主流浏览器厂商的代表组成，国内一些科技大厂如阿里、字节也都加入了该组织，他们的主要工作就是制定ECMAScript标准，标准生成的流程，以及实现。

> 除了TC39外，ECMA国际组织还有很多其他的技术委员会，如TC43 Universal 3D(U3D)、TC45 Office Open XML Formats等。

### ECMAScript发展的历史

ECMAScript经过多年的发展，迭代了多个版本，大概的历史进程如下：

1. ECMAScript 1:

2. ECMAScript 2：

3. ECMAScript 3:

4. ECMAScript 4:

5. ECMAScript 5:

6. ECMAScript -5:

7. ECMAScrpt 6:

8. ECMAScript 2016:

9. ECMAScript 2017:

10. ECMAScript 2018:

11. ECMAScript 2019:

12. ECMAScript 2020:

13. ECMAScript 2021:

14. ECMAScript 2022:

### 向后兼容

ES每个新版本的规范，都会兼容前面低版本的所有特性，比如ES6版本中新增了let、const但是没有删除掉低版本的var。这是因为如果新版本标准中如果删除了低版本中的标准，那么就会在实际的编码中需要兼容多个版本的特性，也就带来了一些问题：

1. Javascript引擎、IDE、构建工具变的臃肿，因为需要支持多个不同的版本；

2. 开发者需要了解多个不同版本之间的差异，开发难度增加；

3. 或者是把项目所有的代码都重构为新标准的实现，但现在ECMAScript标准每年都更新，始终保持代码的最新标准成本太高；再就是不同的项目、不同的模块使用不同标准代码的实现，这样的代码，维护成本太高；

……

为了规避这些问题，ECMA采用了一种策略叫做One Javascript，该策略的大概内容是：

1. 新版本始终完全向后兼容(但是也不排除会有一些不明显的清理)

2. 旧特性不删除也不清理，而是引入新的版本，比如上面提到的let、const和var；

3. 如果语言的某些方面有变化，则只在新的语法结构内生效，即隐氏选用，如yield只在generator中才是关键字、模块和类中的代码都默认开启严格模式等；

> 向后兼容部分，可以参考：https://exploringjs.com/es6/ch_one-javascript.html


参考文档：https://cloud.tencent.com/developer/article/1822635