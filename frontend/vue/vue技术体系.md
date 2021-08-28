### Vue技术体系

> 本文所有内容都是以Vue2为基础的，如果有内容和现在的Vue3有区别的，请大家注意。

1. 认识Vue.js

2. Vue基础语法

3. 组件化开发

4. Vue-cli详解：构建工具，基于webpack

5. vue-router：路由，前端路由，相对于后端路由

6. Vuex：状态管理

7. 网络封装

vue项目中常用axios，注意axios不是一个单词，它是由多个单词组成的缩写

8. 项目实践

9. 项目部署

10. vuejs原理

    1. 响应式原理(双向绑定原理)
    2. vuejs源码


###　简单认识vuejs

首先要安装vuejs，使用、学习任何一种框架，都首先要安装这个框架。

**vue是一个渐进式框架，那么什么是渐进式呢？**

可以将vue作为应用的一部分嵌入到应用中，可以带来丰富的交互体验：可以将一个老的项目逐步使用Vue重构；

**Vue全家桶：**

包括：Vue核心、Vue-router、Vuex

**Vue的特点**

1. 解耦视图和数据

2. 可复用的组件

3. 前端路由技术

4. 状态管理

5. 虚拟DOM

**怎么去学习Vue？**

可以没有React、jQuery、Angular的丰富知识；

但是需要CSS、HTML、Javascript的基础知识；

> jQuery正在逐渐退出历史舞台，github已经放弃了jquery了。

### vuejs安装

安装方式有很多种，我们可以根据项目实际情况去选择合适的方式：

1. CDN的方式：一般在重构老项目、或者本地学习的时候，会用，而在一个全新的vue项目中，是不会使用的；

2. 下载到本地，放到项目中去引入；

3. NPM安装：这是用的最多的、最理想的工具，功能也最强大

> 前面的2种方式，基本不会使用，了解下就可以了。

### 响应式，什么是响应式呢？

响应式就是数据发生了改变的时候，界面会自动跟着同步改变，这就是响应式。

### vue指令

v-for:遍历，vue语法

v-on: 监听事件，可简写为@,如v-on:click监听click事件，v-on:del 监听del事件

```html
 <h3>当前计数：{{counter}}</h3>
 <!--注意这里是直接操作变量++、--  -->
 <!--这种方式虽然可以实现数据的变化效果，但是不利于数据和展现的分离，具体可以看下面的一种方式-->
<button v-on:click="counter++">+</button>
<button v-on:click="counter--">-</button>

<script src="../js/vue.js"></script>
<script>
    let app = new Vue({
        el: "#app",
        data: {
            counter: 0
        }
    });
</script>
```

实现如下图所示的计数器效果：

![计数器](../public/images/../../../public/images/i56.png)

**实现计数器的另一种方式**

```html
    <div id="app">
        <h3>当前计数：{{counter}}</h3>
        <!--这里通过vue指令监听了按钮的点击事件，具体的操作在vue对象里面操作-->
        <button v-on:click="add">+</button>
        <button v-on:click="sub">-</button>
    </div>
    <script src="../js/vue.js"></script>
    <script>
        let app = new Vue({
            el: "#app",
            data: {
                counter: 0
            },

            //这里又学到了vue的一个新属性：methods
            methods: {
                add() {
                    this.counter++;
                },
                sub() {
                    this.counter--;
                }
            }
        });
    </script>
```

实现的效果和上图的一样，就不再贴效果图了。

> @click是v-on:click的语法糖，就是后者的一种简写形式，那为什么叫语法糖呢？就是给你一种简写的形式，让你体会到简写的甜头，就像吃了糖一样，因为这是写代码的语法，所以就是语法上给你一些甜头，就成了语法糖了。

### MVVM

M：Model，指代数据层，一般情况下都是从api请求来的数据，特殊场景下也有静态数据，如一个对象、一个数组，或者是一个json文件；

V：View，Dom，展示层，也可以简单的理解为就是HTML部分；

VM：ViewModel，视图模型层，是View和Model之间的桥梁，指的就是Vue。

MVVM之间的关系可以简单的理解为下图：

![MVVM](../public/images/../../../public/images/i57.png)

这张图不好看，大概意思到了。

从这张图上，我们可以看到，VM是View和Model之间的一个桥梁，它主要做了两件事情，一件事情是Data Listening（数据监听），另一件事情是Data Binding（数据绑定）。从前面我们可以了解到，VM其实主要就是指Vue，Vue在这里的两件事情，其实就是在监听View的数据变化，然后将变化的结果回传给Model；另外就是将Model的数据绑定到View上。Vue通过这种机制实现了数据的双向绑定。

> 一般情况下，Model都不会在VM中的data属性中，而是从api请求来的数据，或者是一个外部的变量，或者是一个json文件，但是在VM中可以通过this来调用这些数据，这是什么原因呢？这是因为在Model和VM之间有一层代理，做了这种关联关系，我们会在后面的知识中介绍这种关联关系。

### Vue对象实例化时的参数：options

通过上面的学习，我们已经熟悉了options中的3个参数：el、data、methods

el：String | Element，绑定要被Vue管理的元素

data：Object | function，在Vue实例中，需要是个Object，但是在组建中个，data就必须是个函数；

methods：{[key:string]: Function}，是一个对象，放置方法（函数）。

```javascript
methods: {
    // 可以是对象字面量的属性赋值的形式
    add: function () {
        this.counter++;
    },
    sub: function () {
        this.counter--;
    },

    // 也可以是ES6中新增的方式
    increament(){
        this.counter++;
    },
    subscribe(){
        this.counter--;
    }
}
```

> 这里需要注意，尽量不要在methods中使用箭头函数，因为箭头函数中的this指向的不是Vue实例，而是父级作用域的上下文。

data可以是对象，也可以是函数，当data在Vue实例中的时候，data就是一个对象；当data在一个组件中的时候，data就是一个函数。看demo：

```html
<!--如这样的场景，data在一个Vue实例中-->
    <div id="app">
        <h3>当前计数：{{counter}}</h3>
        <!-- <button v-on:click="counter++">+</button>
        <button v-on:click="counter--">-</button> -->
        <button v-on:click="add">+</button>
        <button v-on:click="sub">-</button>
    </div>
    <script src="../js/vue.js"></script>
    <script>
        // 实例化Vue实例
        let app = new Vue({
            el: "#app",
            data: { // data在Vue实例中，data值是一个对象
                counter: 0
            },
            methods: {
                add: function () {
                    this.counter++;
                },
                sub: function () {
                    this.counter--;
                }
            }
        });
    </script>
```

再来看一个组件demo：

```html
<!--这是一个Vue组件的例子-->
<template>
    <div class="hello">
        <h2>{{ uname }}</h2>
    </div>
</template>

<script>
export default {
    name: "HelloWorld",
    // data在一个vue组件中个，这里的data是一个函数，而不是一个对象
    data() {
        return {
            uname: "Nicholas",
        };
    },
};
</script>
```


#### 方法和函数有什么区别？什么时候叫方法，什么时候叫函数？

* 方法：method
* 函数：function

方法和函数，在js中的功能基本上一致的，没有什么实质性的区别。但是方法一般和类的实例有关联的，在类中定义的称为方法；不是在类中定义的，通过function关键词定义的具有一定目的功能的代码的组合，称为函数。

在一些语言中，是没有函数的概念的，如强类型语言java中，它是纯面向对象语言，在java中只有方法的概念，没有函数的概念。只有在js这门特殊的语言中，既有函数的概念，又有方法的概念，它们的区别就是定义的环境的不同。

### Vue的生命周期

Vue的生命周期，一个应用从诞生到销毁的整个周期。

> Vue的声明周期原理，和现在前端应用的生命周期概念很相同，如React、小程序。

生命周期的意义，就是说一个应用从诞生到结束，分为了多个阶段，每个阶段都有自己需要完成的事情，也有一些事情是只能在某个阶段去完成，其他的阶段完成不了该阶段才能做的事情。如在Vue应用中，DOM被挂载到Vue之前，Vue是不能操作DOM的，因为Vue还没有和DOM产生关联关系，Vue不具备操作DOM的能力。

**Vue有这样的生命周期**

我从vue文档中截取了一个生命周期的图例：

![Vue生命周期](../public/images/../../../public/images/i58.png)

从这张图中，我们可以看到Vue的生命周期分为了8个阶段，分别为：

beforeCreate、created、beforeMount、mounted、beforeUpdate、updated、beforeDestroy、destroyed，其中mounted和update、beforeUpdate这2个周期循环往复。这些周期，我们不需要一次性全部记住，但是需要有个生命周期的概念、印象，知道、了解Vue应用是有生命周期的，且在不同的阶段做不同的事情。

一般情况下，会在created阶段做网络请求。

Vue应用中，组件也是有生命周期的，其周期基本和Vue的生命周期相同，只是在实际应用中有一点稍微不同的是，Vue一般是不会有destroyed这个阶段的，但是组件基本都会有这个阶段。

> 这里不是说Vue不具有destroyed阶段，而是说应用场景比较少，组件应用场景比较多。

### vscode创建模板文件

这是一个快捷方式，和Vue没有什么关系，只是最近几天在学习vue，在学习的过程中总是多次创建带有vue一些公共代码的html文件。那么我有没有办法也像创建一个空的HTML文件那样，在新建的文件中输入一个!就可以快速生成一个带有一些公共代码的HTML文档呢？我使用vscode编辑器。

结果当然是有的。

打开vscode左下角设置，然后选择用户代码片段，会出现一个代码片段文件的选择列表，这里我们选择html，然后就会出现一个html.json文件，这个json文件有一大堆的英文,就是介绍怎么创建模板文件的方法，这部分代码可以留着，也可以删了，然后将我们的代码文件放进去就可以了。

> 贴我们自己代码片段的时候，主要要转下码。我们的代码只是一个属性值，否则就会被解析成html文档被渲染了。

这里我从网上找了一个demo，大家参考下吧：

```json
{
	"vue_learn_template":{
        "prefix": "vue",
        "body": [
            "<!DOCTYPE html>",
            "<html lang=\"en\">",
            "<head>",
            "\t<meta charset=\"UTF-8\">",
            "\t<meta name=\"viewport\" content=\"width=device-width, initial-scale=1.0\">",
            "\t<meta http-equiv=\"X-UA-Compatible\" content=\"ie=edge\">",
            "\t<title>Document</title>",
            "\t<script src=\"../js/vue.js\"></script>",     
            "</head>\n",
            "<body>",
            "\t<div id =\"app\"> </div>\n",
            "\t<script>",
            "\t //创建Vue实例",
            "\t var vm = new Vue({",
            "\t\tel: '#app',",
            "\t\tdata: {},",
            "\t\tmethods: {}",
            "\t });",
            "\t</script>",
            "</body>\n",
            "</html>"
        ],
        "description": "vue创建文件的模板" // 模板代码片段
    }
}
```

这样当我们在创建一个新的空html文件是输入vue就会出现我们刚才创建的模板，回车后就有了预设的文档了。提效了很多。