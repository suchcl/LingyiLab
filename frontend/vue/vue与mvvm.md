### 1. MVVM

MVVM：Model、View、ViewModel

Model：模型层，负责和服务端的数据交互

View：视图层，负责将数据模型转化为 UI 展示出来，可以简单的理解为 HTML 部分

ViewModel：视图模型层，用来连接View和Model，是Model和View之间连接的桥梁

**MVVM 和Vue的对应关系**

view：对应template

Model：对应data

ViewModel：对应new Vue({……})

**MVVM 之间的关系**

view 通过事件绑定的方式影响 model，model 可以通过数据绑定的方式影响到view，ViewModel则是model和view之间的连接器、桥梁

#### 1.1 MVVM框架的三大要素

响应式：Vue如何监听到data每个属性的变化；

模板引擎：Vue的模板如何被解析，指令如何被处理的；

数据渲染：Vue的模板怎么被渲染成 HTML，中间的渲染过程是什么样子的；
