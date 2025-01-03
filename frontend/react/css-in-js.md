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

    2. Emotion

### 3. css-in-js的优缺点