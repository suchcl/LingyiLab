### Taro介绍

Taro是一个开放式的跨端跨框架解决方案，支持使用React、Vue、Nerv等框架来开发微信、京东、百度、支付宝、字节跳动、QQ、飞书等小程序以及H5、RN等应用。

如今市面上端的形态多种多样，Web、多家公司/端的小程序、微应用、RN等等，当业务需要在多个端下都需要展示时，如果完全针对各个端去开发，开发和维护成本都比较高，这时候如果只需要编写一套代码就可以实现多端统一展示的能力就及其重要。

### 特性

当前Taro可以支持转换到H5、RN以及各个端的小程序。目前官方支持的端、平台如下：

- H5

- React Native

- 微信小程序

- 百度小程序

- 支付宝小程序

- 支付宝LOT小程序

- 京东小程序

- 字节跳动小程序

- QQ小程序

- 钉钉小程序

- 企业微信小程序

- 飞书小程序

### 框架支持

在现在的Taro3种，可以使用完整的React、Vue、Nerv开发。

### 原理

Taro通过编译时的转换和封装、运行时的适配和代码分离，使得开发者可以使用一套开发代码，实现了跨端的开发，从而让开发者可以方便的开发更多的端的应用。

> Taro原理，可以参考这篇文章:[小程序框架开发的探索与实践](https://mp.weixin.qq.com/s?__biz=MzU3NDkzMTI3MA==&mid=2247483770&idx=1&sn=ba2cdea5256e1c4e7bb513aa4c837834)

Taro的原理主要体现在以下几个方面：

1. 编译时转换：Taro通过编译时的AST转换，将不同框架的开发代码如React、Vue、Nerv代码转换为不同平台上的代码。如在转换过程中，Taro会将开发代码中的DOM元素转换为小程序中中的WXML标签，并将React中的事件转换为小程序中的事件。

> 关于AST，可以参考这里：[AST介绍](../%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/AST.md)

2. 运行时封装：Taro通过封装一些底层API，使得开发者可以在不同的平台上使用类似的API接口，从而实现跨平台的开发。例如在小程序中，Taro封装了一些小程序的API，使得开发者可以通过类似React或Vue的组件和生命周期的方式来开发小程序。

3. 平台适配：Taro通过为不同的平台提供不同的适配层，使得开发者可以在不同的平台上享受类似的开发体验。例如在小程序平台上，Taro提供了一些适配小程序的组件和API，使得开发者可以方便的开发小程序应用。

4. 代码分离：Taro通过代码分离的方式，使得可以在不同的平台上只加载需要的代码，从而提高应用的性能和加载速度，从而提升用户的使用体验；

### 运行时

运行时(Runtime)指的是计算机程序在执行时所需要的支持库和环境。当一个程序被编写后，需要一个特定的环境来运行它，这个环境包含了程序所需要的所有资源和支持库，这个环境就是程序的“运行时”。

在程序开发中，编写代码只是程序的一部分，程序需要在一定的环境中运行，才能达到预期的效果。编写代码时，我们需要考虑代码被执行时所需要的支持库、操作系统、硬件等因素，这些因素都是程序的“运行时”的一部分。

例如在node.js的开发中，node.js就是程序的运行时环境。Node.js包含了javascript运行时、各种支持库、操作系统接口等，开发者可以在nodejs中编写和运行javascript程序。

在浏览器开发中，浏览器就是程序的运行时环境。浏览器提供了HTML、CSS、Javascript的运行环境，以及各种支持库和操作系统接口，开发者可以在浏览器中编写和运行web应用程序。

在移动应用程序开发中，移动操作系统就是程序的运行时环境。移动操作系统提供了各种操作系统接口、支持库和硬件接口，开发者可以在移动操作系统中编写和运行移动应用程序。

总的来说，“运行时”指的是程序执行所需要的支持库和环境，包括操作系统、支持库、硬件接口等。程序的运行时环境决定了程序可以运行的平台、可用的资源和性能等，对程序的开发和运行都有重要的影响。

### 编译时

编译时(Compile-time)指的是程序编译过程中进行的各种操作，包括语法检查、代码优化、代码生成等。程序开发中，编写代码只是程序的一部分，编写好的代码需要经过编译器的处理才能生成可执行代码，这个处理过程就是编译时。

在编译时，编译器会对代码进行语法分析和语义分析，检查代码的正确性和合法性，以及进行各种代码优化，最终生成可执行代码：

编译时的操作主要包括以下几个方面：

1. 词法分析和语法分析：编译器会将源代码解析成标记和语法树，以便进行后续处理；

2. 语义分析：编译器会检查代码的类型、作用域、语法错误等问题，并将代码转换为中间代码；

3. 代码优化：编译器会对中间代码进行各种优化，例如常量折叠、循环展开、函数内联等，以提高代码的性能和效率；

4. 代码生成：编译器会根据中间代码生成目标平台的机器码或字节码，以便程序在目标平台上执行。

在程序开发中，编译时非常重要，因为编译时可以检查代码的正确性和合法性，以及进行各种代码优化，从而提升代码的性能和效率。同时，编译时还可以将代码优化为目标平台最优化的代码，以便程序在目标平台上运行时达到最佳的性能和效率。

### 与原生混合

Taro3.x开始，Taro支持使用原生的小程序页面、组件和插件，但是需要注意的是，如果在Taro项目中使用了原生小程序的页面、组件和插件，那么该项目就不再具备多端转换的能力了。如在Taro项目中使用了微信小程序的原生组件，那么该Taro项目就只能转换成微信小程序，转为其他平台小程序时无效。同理，如果是用了其他平台小程序的组件也是同样的问题。

### 创建指定taro版本的taro项目

```bash
taro init proName@2.2.6 # 创建一个taro版本为2.2.6的taro项目
```
> 在通过上述方式创建指定taro版本的项目,依赖当前机器中安装的taro版本,如果机器中安装了多个版本的node,不同版本的taro可能会被安装到不同的node中,需要切换下node版本.

### 项目基本目录

```md
├─config
|   ├─dev.js
|   ├─index.js
|   └prod.js
├─src
|  ├─app.less
|  ├─app.ts
|  ├─index.html
|  ├─pages
|  |   ├─index
|  |   |   ├─index.config.ts
|  |   |   ├─index.less
|  |   |   └index.tsx
```

**config目录**

配置文件目录

dev.js：开发时配置

index.js：默认配置

prod.js：打包时配置

**全局样式**

app.js中引入的样式就是全局样式，局部样式会覆盖全局样式

### Taro开发规范

**文件命名**

taro项目中的js、ts文件以小写字母，多个单词之间使用下划线连接，如util_helper.js

组件名：组件以大驼峰格式命名

**标签**

当标签没有子元素时，始终使用自闭合标签

```jsx
<Food className="stuff" />
```

**jsx属性名始终使用小驼峰命名法**

```jsx
<Foo userName="Nicholas Zakas"
    phoneNumber="123345"
/>
```

**Taro中代码书写顺序**

Taro组件中会包含类静态属性、类属性、生命周期等类成员，其书写顺序遵循以下约定：

1. static静态方法

2. constructor

3. componentWillMount

4. componentDidMount

5. componentWillReceiveProps

6. shouldComponentUpdate

7. componentWillUpdate

8. componentDidUpdate

9. componentWillUnmount

10. 点击回调事件或者事件回调如onClickSubmit、onChangeDescription

11. render

**通用约束**

所有内置组件均需要先引入再使用

