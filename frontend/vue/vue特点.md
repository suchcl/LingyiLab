## 认识Vue

1. Vue读音

2. Vue的渐进式

3. Vue的特点

    - 虚拟DOM

    - 数据和结构分离

4. Vue的安装方式

    - CDN的方式引入

    - 下载到本地引入

    - NPM的方式安装、管理

## Vue初体验

1. mustache语法，双大括号语法：插值

2. Vue列表展示：v-for

3. Vue计数器案例

   - 事件监听：v-on、@

## Vue中的MVVM

1. V:view，DOM，视图层

2. VM：ViewModel，视图模型层，Vue

3. M:Model，数据，基本都是从server请求过来的


## Vue实例化时参数：options

el

data

computed

methods

生命周期函数

## 插值语法

mustache语法：双大括号语法

v-once

v-html

v-text

v-pre

v-cloak:斗篷

## 指令

1. v-bind

    - 绑定基本属性
      - v-bind:str
      - :str   :href  :style  :class
    - 动态绑定class
      - 对象语法：{cls: boolean}
      - 数组语法：[]  使用的场景很少，了解下即可
    - 动态绑定style
      - 对象语法：{property:Value}  property是多个单词拼接时，既可以使用驼峰命名方式，也可以使用-链接的方式
      - 数组语法: [] 使用的场景很少，了解即可

## 计算属性

1. 本质上是一个属性，表现上是一个函数

2. 计算属性命名时，优秀的实践是不带动词，函数、方法的优秀的命名实践是动词