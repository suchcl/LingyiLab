## css-in-js

### 1. 概述

1. 定义

   - css-in-js是一种技术，它允许将css写在js文件中。这种方式打破了传统的HTML、CSS和Javascript分离的模式，将样式的逻辑与Javascript代码紧密结合在了一起。

   - 这种技术在React的组件库中经常用到，可以使用css-in-js库来定义组件的样式，而不是在单纯的css文件中来定义组件的样式。

2. 目的

   - 组件封装：在现代的前端开发中，特别是在使用组件化框架(react、vue等)时，css-in-js有助于实现组件的高度封装。每个组件都可以拥有自己独立的样式，这些组件的样式不会轻易的影响外部的其他组件，同时自己也不会被外部的其他组件所影响。这就好像每个小组件都有自己特定的漂亮的小衣服，不会和其他组件的漂亮的衣服相互干扰。

   - 动态样式：可以根据组件的状态如激活、选中、加载等各种不同的状态轻松的动态生成和更新样式。比如一个按钮组件或导航组件，有鼠标划过效果、激活效果等，这些效果都可以通过js变量来实现。

3. 背景

    随着前端应用的发展、复杂度的不断增加，传统的css解决方案出现了一些问题，比如全局的css可能会带来命名冲突、大型项目中难以追踪样式的来源和作用范围，维护很困难。css-in-js就是为了解决这些问题而出现的，css-in-js的出现提供了一种灵活、可控的样式管理方案。

4. 应用场景

   - 组件库：在构建组件库时，css-in-js可以帮助开发者更好的封装组件的样式，提高组件的可维护性和可扩展性。

   - 动态样式：在需要动态生成和更新样式的场景中，css-in-js可以提供一种简单、灵活的方式来实现。

### 2. 常见的css-in-js库及使用方法

    1. styled-components

        - 安装

        ```bash
        npm install styled-components   // 安装styled-components库
        ```

        - 使用

        需要先导入styled-components依赖

        ```tsx
        import { FC } from "react";
        import styled from "styled-components";

        interface IProps {
            disabled?: boolean;
        }

        const ButtonComp:FC<IProps> = (props) => {
            const Button = styled.button`
            background: ${props.disabled ? '#999' : '#1e80ff'};
            height: 36px;
            color: #fff;
            font-size: 16px;
            cursor: pointer;
            border: 0;
        `;
            return (
                <>
                    <Button disabled={props.disabled}>css-in-js ButtonComp</Button>
                </>
            )
        }

        export default ButtonComp;
        ```

        css-in-js也可以继承已经定义好的样式：

        ```tsx
        import { FC } from "react";
        import styled from "styled-components";

        interface IProps {
            disabled?: boolean;
        }

        const ButtonComp: FC<IProps> = (props) => {
            const Button = styled.button`
            background: ${props.disabled ? '#999' : '#1e80ff'};
            height: 36px;
            color: #fff;
            font-size: 16px;
            cursor: pointer;
            border: 0;
        `;

            // styled-compoents样式继承
            const BigButton = styled(Button)`
                height: 48px;
                font-size: 26px;
                fweight: bold;
            `;

            return (
                <>
                    <Button disabled={props.disabled}>css-in-js ButtonComp</Button>
                    <BigButton>BigButton</BigButton>
                </>
            )
        }

        export default ButtonComp;
        ```
        
        效果如下：

        <img src="./images/i83.png" width="200" />

### 3. css-in-js的优缺点

1. 优点

    - 局部作用域

        样式只在组件内部生效，避免了全局的命名冲突。如果在一个大型项目当中，不同的开发成员分别开发不同的组件、模块，那么他们就可能会自由的定义类名，那么在使用了css-in-js的技术后，就不需要担心类名冲突的问题了。

        > 当然了，命名冲突问题，也可以通过协作、开发规范的方式去解决，但是人始终没有代码的执行力高。

    - 动态性和交互性

        能够方便的根据组件的状态来改变样式，比如当一个按钮、导航等组件被鼠标划过时，改变它的样式。
        
        > 这虽然是css-in-js的一个能力，但从我的认知，这不算是一个什么特别的优势，因为所有的css解决方案都有这个能力。

    - 代码组织紧密

        将样式和逻辑放在一起，使得代码的维护和理解更加方便，对于其他开发人员来说，在查看一个组件的代码时，不需要在多个文件之间进行切换，所有的代码均组织在一起。

        > 样式和逻辑放在一个文件之中，这是web开发最早的时候的做法。在技术的早起想尽了各种办法，才把样式和逻辑抽离开，现在又通过一些技术方案将样式和逻辑放到了一起，感觉是一种轮回。各有各的道理，样式和逻辑抽离有道理，放在一起也有道理，至于说好或者不好，这个得根据权衡取舍。最差的一点，取决于你的领导了。

2. 缺点

    - 学习成本

        对于习惯了传统的将CSS和HTML分离模式的开发者来说，css-in-js需要一定的学习曲线。需要学习怎么在js中定义css样式，以及怎么利用这些样式库来实现复杂的样式。

        > 这种说法就比较牵强了，传统的写css和html的开发者应该也早就不采用这种技术方案了。现在的前端开发者大多都是采用react、vue等类似的前端框架，或者小程序、快应用等也都是采用react、vue类似的语法格式，都是采用虚拟DOM的语法来声明DOM。而服务端开发者也只是需要维护好自己的接口即可，不需要关心css和html的表现问题。所以上面的观点学习成本来说，是可以忽略的。

    - 性能问题

        在一些复杂的应用中，如果大量的使用css-in-js，可能会导致性能下降。这是因为在组件每次重新渲染时，都需要重复计算和应用样式。不过，现在很多的css-in-js库都在不断的进行性能优化，比如通过缓存的方式来减少不必要的样式计算。

        > 也正是因为css和dom混杂在一起，性能低下才将样式和dom、js逻辑分离开的，通过多年的技术迭代、优化，终于实现了样式和逻辑抽离的目标，然后现在又通过其他的方式回归了。感觉是过了一个轮回。就是三十年河东，三十年河西，没有找到一个灵魂的归宿，而更像是一个kpi的结果。

        > 随着现在硬件的发展，在前端技术领域，个人认为前端的性能在整个项目上来说影响是微乎其微的，只要我们根据所使用的框架的规则去进行代码开发，更大的性能瓶颈应该是在服务端的数据处理。现在大量的、繁琐的、复杂的数据量，都需要服务端来处理，前端只需要服务端将处理好的数据进行展示即可。现在前端包括app都可归结为客户端，而客户端现在最大的问题应该是安全问题，这个安全问题还是需要和服务端共同处理的问题。现在人们的安全意识、隐私意识越来越高，从法律层面对数据安全的要求也是越来越高，所以客户端的安全问题才是现在的重中之重。

    - 可移植性差

        css-in-js通常是针对特定的js框架如react紧密结合，这样就使得这样的技术方案就很难与其他的框架进行兼容，进行代码的直接复用。如一个使用styled-components在react中定义的组件样式，就很难直接复用在vue的组件中。

        > 这是正常的现象，就像web早些年直接写内联样式一样，早年DOM中写的内联样式几乎是没有复用性的。

综合上述，我本人是没有发现css-in-js的优势，发现的全是不足的地方。所以我是极力反对这种方案的。