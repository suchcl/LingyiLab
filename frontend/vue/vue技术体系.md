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

![计数器](../../public/images/i56.png)

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

![MVVM](../../public/images/i57.png)

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

![Vue生命周期](../../public/images/i58.png)

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

### Vue模板语法

1. 插值操作

2. 绑定属性

3. 计算属性

4. 事件监听

5. 条件判断

6. 循环遍历

7. 阶段案例

8. v-model

插值操作，指的是data中的一些数据，插入到DOM中，专业术语称为mustache，也称为双大括号({{}})语法。

**v-once**

v-once:该指令指定当前数据只能被渲染一次，标签上的数据不再随着数据的改变而改变了.也就是说，该指令指定的组件，只能被渲染一次，之后的数据的变化，都会跳过该组件或元素。在特殊场景下，可以用于优化渲染性能。

```html
    <div id="app">
        <h3>{{msg}}</h3>
        <h3 v-once>{{msg}}</h3>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                msg: "Hello World!"
            },
            methods: {}
        });
    </script>
```

渲染效果如下图：

![v-once渲染效果图](../../public/images/i59.png)

从渲染结果可以看到2条数据都被正常的渲染出来了，然后我们在开发者工具调试下：

![调试效果](../../public/images/i60.png)

虽然我们在开发者工具修改了msg的属性值，但是只有第一个h3随着数据的改变而改变了值，第二个h3并没有出现我们想像中的结果，没有随着数据的改变而自动重新渲染。这正是因为v-once指令起到了作用。

**v-html**

v-html指定的元素，vue会将其作为当前元素的innerHTML。插入的内容，会按照普通的HTML进行插入，vue不会将其作为vue模板进行编译。

> 在网页中动态插入HTML是很危险的，可能会导致XSS攻击，所以只可以在非常信任的元素上使用v-html,否则不要使用。

> 另外在单文件的模板组件文件中，scoped的样式不会作用于v-html内部，因为v-html部分的HTML没有被vue的模板编译器进行处理。

```html
    <div id="app">
        <h3 v-html="url"></h3>
        <h3>
            <a :href="surl">CSDN</a>
        </h3>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                msg: "Hello Vue!",
                url: '<a href="https://www.baidu.com">百度一下</a>',
                surl: "https://www.csdn.net"
            },
            methods: {}
        });
    </script>
```

如demo所示，两个链接都可以正常的显示出来。

**v-text**

v-text,和v-html类似，只是功能是替换当前元素的innerText，其功能在一些场景上，和mustache语法(双大括号语法)功能相同，都可以将文本渲染到DOM上，但是实际编码中很少使用v-text,因为v-text不够灵活，它会覆盖当前元素的文本，有些场景是需要拼接，而不能直接覆盖。

```html
    <div id ="app"> 
        <h3>{{msg}},Vue！</h3>
        <h3 v-text="msg">,Vue!</h3>
    </div>

    <script>
     //创建Vue实例,得到 ViewModel
     let app = new Vue({
        el: '#app',
        data: {
            msg: "Hello"
        },
        methods: {}
     });
    </script>
```

demo中就展示出了实际的问题，第一个h3通过mustache语法实现了data数据和静态数据的拼接，完美的实现了Hello Vue！的数据展示，但是第一个h3就直接将已经存在的Vue！覆盖了，只显示了Hello。很明显，这不是我们想要的。所以v-text知道这个属性就可以了，很少使用。

**v-pre**

原样输出，vue会跳过被这个指令指定的元素和它的子元素的编译过程。

跳过大量没有指令的节点会加快编译速度。

```html
    <div id="app">
        <h2>{{msg}}</h2>
        <!--原样输出了，没有对{{}}进行编译-->
        <h2 v-pre>{{msg}}</h2>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                msg: "Hello Vue!"
            },
            methods: {}
        });
    </script>
```

**v-cloak**

指令保持在元素上直到元素被Vue关联上。

vue项目中，在vue的el关联元素没有被vue关联上时，vue中的data是不不会被绑定到DOM上的，那么在网页中显示的可能就是一些没有数据的标签，如{{msg}}、{{username}}等等，就是没有data中的数据，如果实例化vue的代码执行的时间很长，在页面DOM被浏览器解析了很久才执行到实例化vue，那么网页就是很长的一段时间都在显示一些vue的指令，对用户来说体感不够友好。v-cloak的作用就是给el关联的元素在vue代码执行之前添加v-cloak这么一个属性，在DOM和vue做了关联之后该属性消失，然后配合css一起使用[v-cloak]{dislay:none;}，指定在DOM在关联vue之前是display:none；不被显示的状态的，使用体感会好很多。

> 在实际项目场景中，该指令一般不会用到。

```html
    <div id="app">
        <h3>{{msg}}</h3>
    </div>
    <script>
        //创建Vue实例,得到 ViewModel
        setTimeout(function () {
            let app = new Vue({
                el: '#app',
                data: {
                    msg: "Hello Vue!"
                },
                methods: {}
            });
        }, 3000);
    </script>
```

如代码，正常情况下是这样的效果：

![没有添加v-cloak属性效果](../../public/images/i61.png)

网页刚开始渲染的时候，直接显示出了vue数据模板，直到DOM和Vue做了关联之后。然后我们看给DOM添加上v-cloak指令后的效果：

```html
    <div id="app" v-cloak>
        <h3>{{msg}}</h3>
    </div>
    <!--style标签位置不一定要和DOM在一起-->
    <style>
        [v-cloak] {
            display: none;
        }
    </style>
    <script>
        //创建Vue实例,得到 ViewModel
        setTimeout(function () {
            let app = new Vue({
                el: '#app',
                data: {
                    msg: "Hello Vue!"
                },
                methods: {}
            });
        }, 3000);
    </script>
```

![添加v-cloak后的显然效果](../../public/images/i62.png)

网页刚开始渲染的时候，DOM和Vue没有关联，页面显示的是空白，直到DOM和Vue做了关联后，才正常的显示了正常需要渲染的内容，体感好了很多。

### v-bind 动态属性绑定

在实际项目中，很多地方的属性我们是不能直接在代码中写成固定的，比如一个图片列表中的图片src属性，文字列表中的href属性。不光是图片列表还是文字列表，一般情况下都是循环遍历出来的内容，所以我们需要给图片的src和a的href设置成动态属性。

```html
    <div id ="app">
        <ul class="list">
            <li><a href="https://www.baidu.com">百度</a></li>
            <li><a href="https://wwww.qq.com">QQ</a></li>
            <li><a href="https://www.163.com">163</a></li>
        </ul>    
    </div>
```

比如这样的列表，这里我们展示了3条内容链接，但是在很多场景下，并不是只展示3条，而是数量都是不固定的，每个地方需要显示的条数都不同，即便在同一个模块，不同的条件展示的数量也会有所不同，所以我们就不能写成固定数量的链接。我们希望在Vue项目中能够实现这样的功能，vue给我们提供了v-bind指令，可以实现动态属性绑定。

```html
<ul class="list">
    <li v-for="item in list"><a v-bind:href="item.url">{{item.title}}</a></li>
</ul>
<script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                list: [
                    {
                        title: "百度",
                        url: "https://www.baidu.com"
                    },
                    {
                        title: "163",
                        url: "https://www.163.com"
                    },
                    {
                        title: "QQ",
                        url: "https://www.qq.com"
                    },
                    {
                        title: "淘宝",
                        url: "https://www.taobao.com"
                    },
                    {
                        title: "搜狐",
                        url: "https://www.sohu.com"
                    }
                ]
            },
            methods: {}
        });
    </script>
```

实际的场景应该就是这样子的，有很多的链接，数量不固定，内容不知，服务端给客户端下发的内容，是在一定规则下的内容，客户端只要求服务端下发的内容是按照一定格式的即可。demo中，我们把ur通过v-bind指令给动态的绑定到了DOM元素上。

那么我们不给DOM的属性添加v-bind可以吗？肯定是不可以的，不添加v-bind指令，说明该属性就是一个普通的HTML属性，它是不会解析vue数据的，只有添加了v-bind指令后，vue在执行的过程中，就会解析该属性，属性值会被当作是一个变量从vue中去检索，然后赋值给该属性。另外，mustache语法也不可以赋值给v-bind指令指定的属性值。mustache语法是插入内容的，不是给属性赋值的。像<h2>{{msg}}</h2>这里的是内容，而<hr :title="msg">{{msg}}</h2>中的title是属性，且title被v-bind指令指定，它的值就是一个动态的值。

**v-bind动态绑定class**

专门介绍动态绑定class，并不是因为class和其他属性有什么特别的地方，而仅仅是因为class的使用频率较高。

v-bind:可以绑定任意类型的值，可以是字符串，也可以是对象。vue对class和style的解析，做了特别的增强，v-bind值除了可以是表达式、字符串外，也可以是对象、数组。

```html
    <div id="app">
        <h3 :class="{active:isActive,link:isLinked}">Hello Vue!</h3>
    </div>
```

demo中class属性的值就是一个对象，对象中属性的值是一个boolean类型值，当boolean类型值为true时，该class就生效，boolean类型值为false时，该class失效。

```html
    <div id="app">
        <h3 :class="{active:isActive,link:isLinked}">Hello Vue!</h3>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                isActive: true,
                isLinked: true
            },
            methods: {}
        });
    </script>

    <style>
        .active {
            font-size: 32px;
        }

        .link {
            color: #369;
        }
    </style>
```

我们可以添加按钮，来演示这个效果：

```html
    <div id="app">
        <h3 :class="{active:isActive,link:isLinked}">Hello Vue!</h3>
        <button @click="btnClick">active切换</button>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                isActive: true,
                isLinked: true
            },
            methods: {
                btnClick:function(){
                    this.isActive = !this.isActive; // 给isActive取反，就不用记录当前的状态了
                }
            }
        });
    </script>

    <style>
        .active {
            font-size: 32px;
        }

        .link {
            color: #369;
        }
    </style>
```

vue中，我们既可以给一个DOM元素添加一个普通的class属性，也可以通过v-bind动态绑定class类，实际项目上，这两种方式都是合法、有效的。一般情况下，当某个class是一定会有的，不会根据外部条件的变化而变化的部分，就可以直接给一个静态的普通的class，当有有些class可能会随着外部条件的变化而变化的，我们就通过v-bind来动态绑定class。静态固定的class和通过v-bind动态绑定的class是可以共存的，代码在解析的时候，是一个合并的操作，而不是覆盖。

vue中动态绑定class有两种方式，一种为对象语法，一种为数组语法。

对象语法，就是上面刚刚了解到的，数组语法，其实和对象语法基本相同，只是将{}改成了[].

数组语法，一般是用在class类名比较多的情况下，看demo：

```html
    <div id="app">
        <h2 v-bind:class='["active","line","vixited"]'>{{msg}}</h2>
    </div>
```

元素h2有多个class，这里将class放置到一个数组中管理。效果如下图：

![vue动态绑定class属性的数组语法](../../public/images/i63.png)

从新学一门技术上来讲，我们有了多种class的绑定形式，会有一定的新鲜感，但是一般不会用到。如果这些class是固定的话，我们可以直接这些class赋值给class属性就了，但是如果会根据外部场景切换class，我们可以将这些class封装到一个方法中，比现在直接在DOM中赋值要更加灵活些。

```html
    <div id="app">
        <h2 v-bind:class='["active","line","vixited"]'>{{msg}}</h2>
        <h2 v-bind:class="getClasses()">{{msg}}</h2>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                msg: "Hello Vue!",
                active: "active",
                line: "line",
                visited: "visited"
            },
            methods: {
                getClasses() {
                    return [this.active, this.line, this.visited];
                }
            }
        });
    </script>
```

两种class的绑定方式，效果是相同的：

![数组语法的class绑定](../../public/images/i64.png)

通过方法获取class列表的方式，对象语法也有同样的实现：

```html
    <div id="app">
        <h2 v-bind:class="{active:isActive,line: isLined,visited: isVisited}">{{msg}}</h2>
        <h2 v-bind:class="getClasses()">{{msg}}</h2>
        <button @click="btnClick">active切换</button>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                msg: "Hello Vue!",
                isActive: true,
                isLined: true,
                isVisited: true
            },
            methods: {
                btnClick: function () {
                    this.isActive = !this.isActive; // 给isActive取反，就不用记录当前的状态了
                    this.isVisited = !this.isVisited;
                },
                // 把class封装到方法中，通过方法来返回对象语法的class列表
                getClasses() {
                    return {
                        active: this.isActive,
                        line: this.isLined,
                        visited: this.isVisited
                    };
                }
            }
        });
    </script>
```

对象语法和数组语法的class绑定，基本是一致的，就是封装数据的时候注意下数据类型就可以了。

> 需要注意的是，动态绑定的class通过方法获取class列表的时候，方法名都加了小括号。但我们在其他的地方见到事件响应的方法的时候，方法名没有加小括号。那么什么时候方法名需要加小括号，什么时候不需要加？先留个悬念吧。

**动态绑定style**

v-bind可以动态绑定DOM属性，前面介绍了增强的class，除了增强了动态绑定class，也增强了style。增强的style和class基本相同，也同时支持对象语法和数组语法。和动态绑定class稍微不同的是，style的本身就是对象类型的，本身就是key:value形式的，不过这里的key，在css中有的是多个单词组成的，单词之间用-链接，在v-bind绑定的style的对象语法中，css属性中由多个单词拼接而成以-拼接的属性，可以使用驼峰形式，如fontSize，当然也可以像在普通的css中一样使用-链接。

```html
    <div id="app">
        <!--普通内联css-->
        <h2 style="font-size: 36px;">{{msg}}</h2>
        <!--动态绑定style的对象语法-->
        <h2 :style="{fontSize: '24px', color: 'red'}">{{msg}}</h2>
        <!--动态绑定style的数组语法-->
        <h2 :style="[color,fz]">{{msg}}</h2>
        <!--动态绑定style，通过方法获取对象语法-->
        <!--方法getStyleByObj的小括号后面不要有分号-->
        <h2 :style="getStyleByObj()">{{msg}}</h2>
        <!--动态绑定style，通过方法获取数组语法-->
        <h2 :style="getStyleByArray()">{{msg}}</h2>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                msg: "Hello Vue!",
                color: { color: "#369" },
                fz: { fontSize: "40px" }
            },
            methods: {
                getStyleByObj() {
                    return {
                        fontSize: "60px",
                        color: "#659"
                    };
                },
                getStyleByArray() {
                    return [this.color, this.fz];
                }
            }
        });
    </script>
```

**计算属性**

一般情况下，当需要使用的数据，需要经过一些计算、处理后的，或者是需要依赖其他的数据变化而变化的数据时，也就是说需要使用经过处理后的数据的返回值时，我们就可以使用计算属性。

计算属性，本质上是属性，但是形式上和方法相同，形式上就是一个函数。

因为计算属性本质上是一个属性，所以一般在给计算属性起名字时，不给名字加动词，而方法、函数名一边都会有一个动词；在mustache语法中使用时，也不需要给计算属性名加小括号，虽然它的表现是一个函数，但是在mustache语法中使用方法时就需要给方法名加上小括号。

```html
    <div id="app">
        <!--mustache语法除了可以变量插值，也可以使用方法，方法名需要加小括号-->
        <h2>{{getFullName()}}</h2>

        <!--计算属性：计算属性不需要加小括号-->
        <h2>{{fullName}}</h2>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                firstName: "Nicholas",
                lastName: "Zakas"
            },
            computed:{
                // 计算属性命名，不加动词，计算属性本质上还是属性，虽然表现上是一个函数
                fullName(){
                    // return this.firstName + " " + this.lastName;  // 这种方式也可以，也还只是变量的拼接方式不同
                    return `${this.firstName} ${this.lastName}`;
                }
            },
            methods: {
                getFullName(){
                    // return this.firstName+ " " +this.lastName; // 这种方式也可以，就是拼接变量
                    return `${this.firstName} ${this.lastName}`;
                }
            }
        });
    </script>
```

仅仅从上面demo来看，想了解下计算属性，已经有了大概的认识，但是计算属性的优势没有体现出来。实际场景中，可能使用计算属性就是一个非常优秀的实践，比如下面的demo，有很多书，我想显示这些书的总价。正常的思维应该是封装一个方法，让这个方法去给我计算这些书的总价。封装方法计算性价这个思路非常好。

但是我们刚刚了解到了计算属性，那么是不是使用计算属性比使用方法更优秀呢？这个得了解了计算属性和方法的区别后才能知道，但是现在可以说的是，计算属性，在依赖值没有变化的时候，那这个属性（也可以说是一个方法）无论被调用几次，它都只执行依次，但是方法就不同了，方法是调用一次就执行依次。计算属性有一个缓存的优势。

```html
    <div id="app">
        <h2>总价：{{totalPrice}}</h2>
        <h3>总价：{{allPrice}}</h3>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                books: [
                    {id: 1, name: "Javascript高级程序设计", price: 119},
                    {id: 2, name: "Es6标准入门",price: 89},
                    {id: 3,name: "Nodejs实战",price: 129},
                    {id: 4,name: "中国近代史纲要",price: 49}
                ]
            },
            computed: {
                // 两种计算总价的计算属性，只是使用了不同的js的基本功能
                // 这是最普通的一种遍历
                totalPrice() {
                    let result = 0;
                    for (let i = 0; i < this.books.length; i++) {
                        result += this.books[i].price;
                    }
                    return result;
                },

                // 这里使用了es6的reduce方法，数组变量，数据归并，
                allPrice() {
                    return this.books.reduce(function (prev, cur, index, arr) {
                        return prev + cur.price;
                    }, 0);
                }
            },
            methods: {}
        });
    </script>
```