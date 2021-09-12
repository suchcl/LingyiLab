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

**计算属性的setter和getter**

> 计算属性是有缓存的

为什么计算舒心是按照属性的方式使用，而不是按照函数的方式去使用呢？

计算属性，本质上是属性，所以就会有获取属性值和设置属性值的情况,计算属性内部有getter和getter机制实现属性的设置值和获取值。可参考下面的demo：

```html
    <div id="app">
        <h2>{{fullName}}</h2>
    </div>
    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                firstName: "Nichoalas",
                lastName: "Zakas"
            },
            computed: {
                fullName: {
                    set(newValue) {
                        this.firstName = newValue.split(" ")[0];
                        this.lastName = newValue.split(" ")[1];
                    },
                    get() {
                        return this.firstName + " " + this.lastName;
                    }
                }
            },
            methods: {}
        });
    </script>
```

不过在一般的情况下，计算属性只需要获取值，很少有给计算属性赋值的情况，所以一般在实现getter和setter的时候，会省略setter，只留下getter。大多数场景会省略setter，但是不代表不能设置setter。

> 默认情况下，计算属性是没有实现setter方法的，也就是说，我们只能获取属性值，而不能给属性赋值。

```html
    <div id="app">
        <h2>{{fullName}}</h2>
    </div>
    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                firstName: "Nichoalas",
                lastName: "Zakas"
            },
            computed: {
                fullName(){
                    return this.firstName + " " + this.lastName;
                }
            },
            methods: {}
        });
    </script>
```

如demo所示，计算属性fullName是默认方式，默认方式只实现了getter，无论是从开发者工具中调试，还是代码中给计算属性fullName赋值，都不行，无论何种方式都不能给计算属性赋值，因为默认形式下的计算属性，实际上是getter方法，缺省了setter方法，所以没有办法重新设置值。那么我们有没有办法修改这个属性的值呢？当然有了，显示的实现setter方法。

```html
    <div id="app">
        <h2>{{fullName}}</h2>
    </div>
    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                firstName: "Nichoalas",
                lastName: "Zakas"
            },
            computed: {
                fullName: {
                    set(newValue) {
                        this.firstName = newValue.split(" ")[0];
                        this.lastName = newValue.split(" ")[1];
                    },
                    get() {
                        return this.firstName + " " + this.lastName;
                    }
                }
            },
            methods: {}
        });
    </script>
```

这样，我们就可以修改计算属性的值了。

**计算属性和methods对比**

基本上使用计算属性的地方，也都有使用methods实现，那么计算属性和methods有什么区别呢？看demo：

```html
    <div id="app">
        <!--我们分别执行计算属性和methods方法的获取全名的方法，执行计算属性就是注释掉methods部分，执行methods就注释掉计算属性部分，我们看到执行计算属性部分的时候，计算属性函数执行了1次，而methods执行了4次-->
        <!--计算属性-->
        <h2>{{fullName}}</h2>
        <h2>{{fullName}}</h2>
        <h2>{{fullName}}</h2>
        <h2>{{fullName}}</h2>
        <!--methods-->
        <h2>{{getFullName()}}</h2>
        <h2>{{getFullName()}}</h2>
        <h2>{{getFullName()}}</h2>
        <h2>{{getFullName()}}</h2>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                firstName: "Nicholas",
                lastName: "Zakas"
            },
            computed: {
                fullName() {
                    console.log();
                    console.log("计算属性：fullName");
                    return this.firstName + " " + this.lastName;
                }
            },
            methods: {
                getFullName() {
                    console.log("methods:getFullName()");
                    return this.firstName + " " + this.lastName;
                }
            }
        });
    </script>
```

从demo中，表面的现象是多次获取同样的值，计算属函数性执行了一次，methods执行了多次。说明了：计算属性的缓存能力，依赖值没有变化的时候，多获取同一个值只执行依次；而methods则会执行多次。

那么什么时候使用计算属性，什么时候使用methods呢？

在一些值需要经过处理后展示的时候，就可以使用计算属性，如需要显示一些商品的总价的时候，我们可以通过计算属性去计算；而需要相应监听事件的时候，我们就使用methods，如一个点击事件的处理函数、一个敲击回车键的响应事件等等，都可以使用methods。

**事件监听**

指令：v-on  绑定事件监听器  缩写：@   预期：function   参数：event

```html
    <div id="app">
        <h2>{{counter}}</h2>
        <!--正常的全拼写法-->
        <button v-on:click="increment">+</button>
        <button v-on:click="decrement">-</button>
        <hr>
        <!--语法糖写法-->
        <button @click="increment">+</button>
        <button @click="decrement">-</button>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                counter: 0
            },
            methods: {
                increment(){
                    this.counter++;
                },
                decrement(){
                    this.counter--;
                }
            }
        });
    </script>
```

**v-on参数**

1. 不需要参数的情况：

    - 在事件监听时，响应监听事件的方法后，可没有小括号，但是也可以有；
    - 但如果在mustache语法中做插值操作时，方法后的小括号不可省；

```html
    <div id ="app">
        <!--mustache中，方法小括号不可省-->
        <h2>{{initCounter()}}</h2>
        <!--响应监听事件的方法，没有参数的情况下，方法名后的小括号可以省略，也可以加上，效果相同-->
        <button @click="btn1Click()">button1</button>
        <button @click="btn1Click">button1-1</button>
    </div>

    <script>
     //创建Vue实例,得到 ViewModel
     let app = new Vue({
        el: '#app',
        data: {
            counter: 0
        },
        methods: {
            btn1Click(){
                console.log("按钮1被点击了");
            },
            initCounter(){
                let num = this.counter + 2;
                return num;
            }
        }
     });
    </script>
```

    - 在事件定义时，写方法时省略了小括号，但是方法本身是需要一个小括号的，这个时候，vue会默认将浏览器产生的event事件作为参数传递到方法中，这个时候再调用方法的时候，不加参数，就默认把event参数传递给方法了
      
      - 同样的场景，如果在方法调用时，给方法加上了小括号，那么传递给方法的就是一个undefined

```html
        <!--在事件定义时，写方法时省略了小括号，但是方法本身是需要一个小括号的，这个时候，vue会默认将浏览器产生的event事件作为参数传递到方法中，这个时候再调用方法的时候，不加参数，就默认把event参数传递给方法了-->
        <button @click="btn2Click">button2</button>

        <!--这个时候方法调用时加上了小括号，方法在执行时的参数就是undefined-->
        <button @click="btn2Click()">button2</button>
    </div>

    <script>
     //创建Vue实例,得到 ViewModel
     let app = new Vue({
        el: '#app',
        data: {
            counter: 0
        },
        methods: {
            btn1Click(){
                console.log("按钮1被点击了");
            },
            btn2Click(name){
                console.log(name); // name没有打印出来，PointerEvent {isTrusted: true, pointerId: 1, width: 1, height: 1, pressure: 0, …}  把当前的事件给打印了出来，说明在没有给命名方法传递参数的时候，vue就将浏览器的默认事件传递给了方法
            },
            initCounter(){
                let num = this.counter + 2;
                return num;
            }
        }
     });
    </script>
```

> 前端中，在响应事件监听的函数中，会默认传递给函数一个event

2. 方法定义时需要event（浏览器事件）参数，也需要一个其他的参数，那么在方法调用时怎么获取到浏览器的事件(event)呢？vue给我们提供了：$event,可以帮我们手动获取浏览器事件

```html
<!--方法定义时需要一个event参数，也需要一个其他的参数,这个时候可以通过$event手动获取浏览器事件-->
<button @click="btn3Click(abc,$event)">button3</button>
<script>
    //创建Vue实例,得到 ViewModel
    let app = new Vue({
        el: '#app',
        data: {
            counter: 0,
            abc: "Hello"
        },
        methods: {
            btn3Click(abc, event) { // 方法调用的地方，通过$event将事件传递给了方法
                console.log("+++++++", abc, event);
            }
        }
    });
</script>
```

**v-on修饰符**

* .stop 阻止事件继续传播，传播包括向上的冒泡和向下的捕获

```html
    <div id="app">
        <div @click="divClick">
            <!--不添加.stop修饰符，点击按钮的同时会触发div的点击事件，加上.stop修饰符，会阻止按钮的点击事件向上冒泡-->
            <button @click.stop="btnClick">button</button>
        </div>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {},
            methods: {
                divClick() {
                    console.log("Div被点击了");
                },
                btnClick() {
                    console.log("button被点击了");
                }
            }
        });
    </script>
```

在原生js中，阻止事件冒泡的方式需要调用js的stopPropagation()方法，可看demo：

```html
    <div class="box">
        <div class="btn-area" id="btnArea">我是button包裹元素
            <button id="btn">button</button>
        </div>
    </div>

    <script>
        let btnArea = document.getElementById("btnArea");
        let btn = document.getElementById("btn");
        btn.addEventListener("click", function (e) {
            console.log("按钮被点击");
            // 阻止调用相同事件的传播：传播包括向上的冒泡和向下的捕获
            e.stopPropagation();
        });
        btnArea.addEventListener("click", function () {
            console.log("div被点击");
        });
    </script>
```

* .prevent：阻止默认行为

一些DOM元素都是有默认行为的，如a元素点击后是会进行跳转的，form元素会默认向目标服务器提交数据等，但是在一些场景中，我们并不希望这些元素进行这些默认的行为，而是希望我们能够主动控制这些元素的行为，那么在vue项目中个，我们可以给这些元素的事件添加.prevent修饰符。

```html
<!--阻止默认事件:元素a，点击后默认是要跳转出去的，但是在点击事件中添加了.prevent修饰符后，就不会进行跳转动作了-->
<a href="https://www.baidu.com" target="_blank" @click.prevent="aClick">百度</a>
    <script>
//创建Vue实例,得到 ViewModel
let app = new Vue({
    el: '#app',
    data: {},
    methods: {
        aClick() {
            console.log("元素a被点击了");
        }
    }
});
</script>
```

原生js中阻止默认行为的方法,需要调用事件对象的preventDefault()方法，看demo：

```html
<a href="https://www.baidu.com" target="_blank" id="link">百度</a>
<script>
    let link = document.getElementById("link");
    link.addEventListener("click",function(event){
        console.log("元素a被点击了");
        event.preventDefault();
    });
</script>
```

* once:指定事件只执行一次

特殊的场景下，我们需要某个事件只能被执行依次，这个时候就可以使用.once修饰符。现在没有想到什么场景，就先把功能演示一下吧。

```html
<!--这个按钮只能执行一次点击事件-->
<button @click.once="btnClickOnce">.once修饰符</button>
    <script>
//创建Vue实例,得到 ViewModel
let app = new Vue({
    el: '#app',
    data: {},
    methods: {
        btnClickOnce(){
            console.log("这个按钮只能被执行一次点击事件");
        }
    }
});
</script>
```

* 按键修饰符：就是监听键盘上按键的事件，可以通过绑定按键码和按键别名来绑定按键，指定只有在绑定的按键在该事件才去执行响应函数。不过现在按键码（keyCode）已经废弃了，新版本的浏览器可能会不支持，我们只需要了解通过按键别名的方式就可以了。

```html
<!--默认情况下，所有按键的按键松开事件都会执行响应函数，加上了.enter修饰符后，只有在回车键松开的时候，才会执行响应函数-->
<input type="text" @keyup.enter="keyUp">
    <script>
//创建Vue实例,得到 ViewModel
let app = new Vue({
    el: '#app',
    data: {},
    methods: {
        keyUp(){
            console.log("keyUp事件执行了");
        }
    }
});
</script>
```

除了上面介绍的几个修饰符之外，还有其他的一些修饰符，可以参考下官方文档：[vue2中的事件修饰符https://cn.vuejs.org/v2/guide/events.html#%E4%BA%8B%E4%BB%B6%E4%BF%AE%E9%A5%B0%E7%AC%A6](https://cn.vuejs.org/v2/guide/events.html#%E4%BA%8B%E4%BB%B6%E4%BF%AE%E9%A5%B0%E7%AC%A6)、[vue3中的事件修饰符：https://vue3js.cn/docs/zh/guide/events.html#%E4%BA%8B%E4%BB%B6%E4%BF%AE%E9%A5%B0%E7%AC%A6](https://vue3js.cn/docs/zh/guide/events.html#%E4%BA%8B%E4%BB%B6%E4%BF%AE%E9%A5%B0%E7%AC%A6) 粗略的扫了一眼，没有发现什么差异。

### v-if

v-if，控制元素是否被渲染，和v-if配对使用的v-else-if、v-else，v-else-if用的场景很少，因为在DOM做条件判断，不如在js代码中做逻辑判断更顺畅。语法比较简单，直接看demo吧：

```html
<div id="app">
    <h2 v-if="score >= 90">优秀</h2>
    <h2 v-else-if="score >= 80">良好</h2>
    <h2 v-else-if="score >= 60">及格</h2>
    <h2 v-else>不及格</h2>
</div>

<script>
    //创建Vue实例,得到 ViewModel
    let app = new Vue({
        el: '#app',
        data: {
            score: 96
        },
        methods: {}
    });
</script>
```

demo中，我们使用了v-if、v-else-if、v-else，但是这并不是一种很好的实践，因为DOM中大量的逻辑判断，我们可以放在js中：

```html
<div id="app">
    <h2>{{results}}</h2>
</div>

<script>
    //创建Vue实例,得到 ViewModel
    let app = new Vue({
        el: '#app',
        data: {
            score: 46,
            result: "优秀"
        },
        computed: {
            results() {
                let score = this.score;
                let result = "优秀";
                if (score >= 90) {
                    result = "优秀";
                } else if (score >= 80) {
                    result = "良好";
                } else if (score >= 60) {
                    result = "及格";
                } else {
                    result = "不及格";
                }
                return result;
            }
        },
        methods: {}
    });
</script>
```

一个简单的逻辑切换的demo，切换用户的登录状态。现在需要登录的系统，一般都会优先使用手机号登录，或者再使用账号登录，我们看下简单的实现：

```html
<div id="app">
    <div class="login-mobile" v-if="isMobile">手机号登录</div>
    <div class="login-acc" v-else>账号登录</div>
    <button @click="changeLoginTYpe">{{loginType}}</button>
</div>

<script>
    //创建Vue实例,得到 ViewModel
    let app = new Vue({
        el: '#app',
        data: {
            loginType: "账号登录",
            isMobile: true
        },
        methods: {
            changeLoginTYpe() {
                this.isMobile = !this.isMobile;
                if (this.isMobile) {
                    this.loginType = "账号登录";
                } else {
                    this.loginType = "手机号登录";
                }
            }
        }
    });
</script>
```

vue中，如果有经过逻辑判断展示不同的DOM的时候，vue并不是直接切换不同逻辑需要展示的DOM，而是会先通过diff算法判断已经展示的DOM和即将要展示的DOM的区别，生成虚拟DOM，然后将即将要展示的DOM的和已经展示DOM的不同的地方，转换到已经展示的DOM上，然后再渲染到浏览器上。因为vue的这种操作原理，所以有的场景，比如前后两种逻辑都有输入框的时候，已经在前一个逻辑中输入了一些文字，在切换了逻辑后，那么这些已经输入的文字，会被原样的带到切换后的逻辑中的输入框中。

如登录方式的切换demo：

```html
    <div id="app">
        <!--手机号方式登录-->
        <div class="login-mobile" v-if="isMobile">
            <label for="mobile">手机号：</label>
            <input type="text" id="mobile" placeholder="请输入手机号">
        </div>
        <!--账号方式登录-->
        <div class="login-acc" v-else>
            <label for="acc">用户名：</label>
            <input type="text" id="acc" placeholder="请输入用户名">
        </div>
        <button @click="changeLoginType">切换为{{loginType}}</button>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                isMobile: true,
                loginType: "账号方式登录"
            },
            methods: {
                changeLoginType() {
                    this.isMobile = !this.isMobile;
                    if (this.isMobile) {
                        this.loginType = "账号方式登录";
                    } else {
                        this.loginType = "手机号登录";
                    }
                }
            }
        });
    </script>
```

效果如图：

![登录方式切换，输入框输入内容在切换了登录方式后原样带了过去](../../public/images/i68.png)

我们点了按钮后，效果如下：

![登录方式切换，输入框输入内容在切换了登录方式后原样带了过去](../../public/images/i69.png)

> 输入框输入的内容，在切换了登录方式后，原样带了过去，是因为vue的内部处理，有一个比较明显的表现：就是两种登录方式的DOM结构相同，只是内部的一些属性值不同。如果DOM结构不同了，vue的diff算法就不会认为它们相同了，值也就带不过去了。

虽然vue这样的处理，在性能上有了一定程度的提升，但是我们在实际的业务场景上，并不是我们想要的，我们并不想要它能够直接输入之前输入过的内容。那怎么办呢？

直接给输入框加一个属性key即可。

```html
    <div id="app">
        <!--手机号方式登录-->
        <div class="login-mobile" v-if="isMobile">
            <label for="mobile">手机号：</label>
            <input type="text" id="mobile" placeholder="请输入手机号" key="mobile">
        </div>
        <!--账号方式登录-->
        <div class="login-acc" v-else>
            <label for="acc">用户名：</label>
            <input type="text" id="acc" placeholder="请输入用户名" key="acc">
        </div>
        <button @click="changeLoginType">切换为{{loginType}}</button>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                isMobile: true,
                loginType: "账号方式登录"
            },
            methods: {
                changeLoginType() {
                    this.isMobile = !this.isMobile;
                    if (this.isMobile) {
                        this.loginType = "账号方式登录";
                    } else {
                        this.loginType = "手机号登录";
                    }
                }
            }
        });
    </script>
```

新的demo和原来的相比，只有在两个input空间中加了个key属性，就解决了我们当前的问题了。

**v-show**

v-show，控制元素是否显示，用法和v-if相同，属性值是一个Boolean值。

```html
    <div id ="app">
        <h2 v-show="isShow">{{msg}}</h2>
    </div>

    <script>
     //创建Vue实例,得到 ViewModel
     let app = new Vue({
        el: '#app',
        data: {
            msg: "Hello Vue!",
            isShow: true
        },
        methods: {}
     });
    </script>
```

**v-show和v-if的区别以及选用哪个**

1. v-if: 指定元素是否渲染，是否添加到DOM中；

2. v-show：指定元素是否展示，是否展示指的是元素已经被渲染到了DOM中，而已经渲染到DOM中的元素是否被看到；

3. v-show:指定的元素，本质上是通过css样式display：none/block来控制元素是否展示的，所以它控制的是样式；

```html
    <div id ="app">
        <!--当isShow被修改为false时，该元素直接没有被渲染到DOM中-->
        <h2 v-if="isShow" id="vif">{{msg}}</h2>
        <!--当isShow被修改为false时，该元素通过display：none；隐藏掉了-->
        <h2 v-show="isShow" id="vshow">{{msg}}</h2>
    </div>

    <script>
     //创建Vue实例,得到 ViewModel
     let app = new Vue({
        el: '#app',
        data: {
            msg: "Hello Vue!",
            isShow: true
        },
        methods: {}
     });
    </script>
```

效果可以在开发者工具中修改isShow来看效果。

那我们在项目中应该怎么选用v-if和v-show呢？

v-if:当一个模块中需要切换的频率很低，比如只有一次时，我们可以选择v-if。v-if指定元素是否被渲染，切换频率低，减少被渲染的元素可以减小页面的质量，减少初次渲染的代码量，一定程度上可以提升页面的加载性能；

v-show：当一个模块会被频繁的切换时，可以选择v-show。v-show指定的元素是是否被展示，它们已经被完全的渲染了出来，只是通过css样式的display属性来控制了是否展示。所以在选择v-show时，初次的渲染时可能会有一定的影响，但是后续不论多少次的模块切换，都不会重新加载，使用体验会更顺畅。

### v-for遍历属组和数组

v-for可以遍历数组和对象，语法比较简单。

**遍历数组**

格式：(item,index) 可以遍历到数组的项和当前数组项的索引.

遍历数组的时候，既可以遍历两个项，也可以遍历一个项:

遍历两个项的时候，则分别为数组项、当前数组项的索引;

当遍历一个项的时候，则为数组项

```html
    <div id="app">
        <ul>
            <!--如果遍历了两个值，则分别为数组项、当前项的索引-->
            <li v-for="(item,index) in fruits">{{index + 1}}-{{item}}</li>
        </ul>
        <ul>
            <!--如果只遍历了一个项，则为数组项-->
            <li v-for="item in fruits">{{item}}</li>
        </ul>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                fruits: ["Apple", "Pear", "Peach"]
            },
            methods: {}
        });
    </script>
```

**遍历对象**

v-for还可以遍历对象，有3重格式:

1. v-for="value in obj": 遍历的项为当前对象的各属性值

```html
    <div id="app">
        <!--只遍历一个值：则为当前对象的各属性值-->
        <ul>
            <!--遍历中使用了个item变量，名称可以自定义，这里实际表示的是当前对象的属性的value-->
            <li v-for="item in author">{{item}}</li>
        </ul>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                author: {
                    name: "Nicholas Zakas",
                    age: 26,
                    job: "Programmer"
                }
            },
            methods: {}
        });
    </script>
```

看效果：

![只遍历一个值：则为当前对象的各属性值](../../public/images/i70.png)

2. v-for="(value,key) in obj"：遍历的项分别为当前对象各属性值、各属性的key

```html
    <div id="app">
        <!--遍历2个值：则为当前对象的各属性值、各属性key-->
        <ul>
            <li v-for="(value,key) in author">{{key}}：{{value}}</li>
        </ul>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                author: {
                    name: "Nicholas Zakas",
                    age: 26,
                    job: "Programmer"
                }
            },
            methods: {}
        });
    </script>
```

看效果图：

![遍历2个值：则为当前对象的各属性值、各属性key](../../public/images/i71.png)

3. v-for="(value,key,index) in obj"：遍历的项分别为当前对象个属性的值、各属性的key、各属性的索引

```html
    <div id="app">
        <!--遍历对象3个值，分别为对象各属性值、个属性key、各属性索引-->
        <ul>
            <li v-for="(value,key,index) in author">{{index}}-{{key}}：{{value}}</li>
        </ul>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                author: {
                    name: "Nicholas Zakas",
                    age: 26,
                    job: "Programmer"
                }
            },
            methods: {}
        });
    </script>
```

效果图：

![遍历对象3个值，分别为对象各属性值、个属性key、各属性索引](../../public/images/i72.png)

**v-for绑定和不绑定key的区别**

> 在v-for遍历中，key要保持唯一性，一般不要使用index，使用index对性能的帮助几乎没有，不能保证key的唯一；

**检查数组的更新**

vue中数据是响应式的，那么数组中的哪些方法是响应式的，哪些数组的方法做不到响应式呢？

1. 通过push方法修改数组可以做到响应式

```html
   <div id="app">
        <ul>
            <li v-for="(item,index) in letters">{{item}}</li>
        </ul>
        <button @click="btnClick">动态添加元素</button>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                letters: ["a", "b", "c", "d"]
            },
            methods: {
                btnClick(){
                    this.letters.push("ffff");
                }
            }
        });
    </script>
```

当我们点击按钮的时候，添加的元素可以直接响应式的渲染到页面上，可以直接看到效果。

2. 通过数组索引值修改数组是不能响应式的

```html
    <div id="app">
        <ul>
            <li v-for="(item,index) in letters">{{item}}</li>
        </ul>
        <button @click="btnClick">动态添加元素</button>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                letters: ["a", "b", "c", "d"]
            },
            methods: {
                btnClick(){
                    // 通过数组索引修改数组，不能直接响应式的渲染到页面上，但是数据确实是已经修改过了
                    this.letters[0] = "修改了数组第一个元素";
                }
            }
        });
    </script>
```

通过数组索引的方式修改了数组后，修改后的数据没有响应式的渲染到页面上，但是数据确实是已经被修改了

![通过数组索引修改数组元素，修改后的数据没有响应式的渲染到页面上，但是数据已经被修改了](../../public/images/i73.png)

**那么我们还是想通过索引来修改数组，怎么办呢？**

有两种办法：

1. 使用splice方法

```javascript
this.letters.splice(0, 1, "qq"); // 通过元素替换的方式
```

> 虽然还有下面一种方法，但是推荐使用这种方法，因为还是更加直观的在修改数组。

2. 使用Vue.set()方法

```javascript
Vue.set(this.letters, 0, "vip");
```


**数组的下列方法，可以响应式的渲染到页面上：**

1. push：从数组尾部添加元素

2. pop：元素尾部移除，删除数组最后一个元素

```html
    <div id="app">
        <ul>
            <li v-for="(item,index) in letters">{{item}}</li>
        </ul>
        <button @click="btnClick">动态添加元素</button>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                letters: ["a", "b", "c", "d"]
            },
            methods: {
                btnClick(){
                    // pop 元素尾部移除
                    // this.letters.pop();
                }
            }
        });
    </script>
```

3. shift：元素头部移除，删除数组第一个元素

```html
    <div id="app">
        <ul>
            <li v-for="(item,index) in letters">{{item}}</li>
        </ul>
        <button @click="btnClick">动态添加元素</button>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                letters: ["a", "b", "c", "d"]
            },
            methods: {
                btnClick(){
                    // shift 元素头部移除
                    this.letters.shift();
                }
            }
        });
    </script>
```

4. unshift:在数组最前面添加元素

```html
   <div id="app">
        <ul>
            <li v-for="(item,index) in letters">{{item}}</li>
        </ul>
        <button @click="btnClick">动态添加元素</button>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                letters: ["a", "b", "c", "d"]
            },
            methods: {
                btnClick(){
                    // unshift 在数组头部添加元素
                    this.letters.unshift("kkk","lll","mmm"); // unshift可以头部添加多个元素，也可以添加1个元素
                }
            }
        });
    </script>
```

5. splice

这个方法，功能有点多，既可以插入元素、也可以删除元素，还可以替换元素。

splice(start,):

start：插入元素、删除元素、替换元素的起始位置

第2个参数：

- 要删除或者替换元素的个数，第2个元素为要删除元素的个数；如果第2个参数没有传，那么会从起始元素之后的元素全部删除；

如果只有1个参数，则参数表示起始位置，从起始位置之后的所有元素都要被删除；起始位置从索引0开始；

```html
    <div id="app">
        <ul>
            <li v-for="(item,index) in letters">{{item}}</li>
        </ul>
        <button @click="btnClick">动态添加元素</button>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                letters: ["a", "b", "c", "d", "e"]
            },
            methods: {
                btnClick() {
                    // 只有1个参数
                    this.letters.splice(2); // 留下a、b，之后的字母全部被删除

                }
            }
        });
    </script>
```

如果是有2个参数，在第一个参数是起始位置，第2个参数是要删除的元素的个数；

```html
   <div id="app">
        <ul>
            <li v-for="(item,index) in letters">{{item}}</li>
        </ul>
        <button @click="btnClick">动态添加元素</button>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                letters: ["a", "b", "c", "d", "e"]
            },
            methods: {
                btnClick() {
                    // 只有1个参数
                    this.letters.splice(1, 2); // 从b开始删除2个字母，最后结果为a、d、e

                }
            }
        });
    </script>
```

如果有2个以上的参数，则第一个参数为起始位置，第2个参数为要替换元素的数量，后面的参数为替换的元素(也可以理解为：第一个参数为起始位置，没有变化，第2个参数为要删除的元素的个数，后面的元素为要重新插入的元素)，无论是哪种描述和理解，最终的结果都是相同的，就是一些位置的元素成了新的元素，原来的元素没有了

```html
    <div id="app">
        <ul>
            <li v-for="(item,index) in letters">{{item}}</li>
        </ul>
        <button @click="btnClick">动态添加元素</button>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                letters: ["a", "b", "c", "d", "e"]
            },
            methods: {
                btnClick() {
                    // 只有1个参数
                    this.letters.splice(1, 2, "m", "n"); // "a", "m", "n", "d", "e"
                }
            }
        });
    </script>
```

只要splice的参数超过了3个，那么第1个参数，就是起始位置不会变，第2个参数是要变动的元素的个数，后面的元素无论多少，都会插入到从起始位置开始的地方，元素多了就多插入，元素少了就少插入

```html
   <div id="app">
        <ul>
            <li v-for="(item,index) in letters">{{item}}</li>
        </ul>
        <button @click="btnClick">动态添加元素</button>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                letters: ["a", "b", "c", "d", "e"]
            },
            methods: {
                btnClick() {
                    // 只有1个参数
                    this.letters.splice(1, 3, "m", "n", "k", "l"); // 'a', 'm', 'n', 'k', 'l', 'e'
                }
            }
        });
    </script>
```

6. sort

7. reverse

数组的这些方法，可以直接将修改后的数据渲染到页面上。


**数据遍历的一个小demo**

有一组数组，第一条数据永远展示为红色，其余数据点击的时候变为红色，点击后第一条数据也还是红色保持不变.

```html
<style>
    .active,
    .isFirst {
        color: #f20;
    }

    .fruits li {
        cursor: pointer;
    }
</style>
<div id="app">
    <ul class="fruits">
    <!--这里是用了动态class去绑定，去控制样式为红色的class是否绑定到元素上面-->
        <li v-for="(item,index) in fruits" :Key="item"
            :class="{active: currentIndex === index, isFirst: index === 0}" @click="liClick(index)">{{item}}</li>
    </ul>
</div>

<script>
    //创建Vue实例,得到 ViewModel
    let app = new Vue({
        el: '#app',
        data: {
            fruits: ["Apple", "Peach", "Pear", "Banana", "Potato"],
            currentIndex: 0
        },
        methods: {
            liClick(index) {
                this.currentIndex = index;
            }
        }
    });
</script>
```

**过滤器**

过滤器，也是个函数

> 过滤器，既然也是个函数，那么它和methods以及computed有什么区别呢？

### v-model

前面学过了mustache语法，将数据绑定到普通的DOM元素上的时候，我们通过v-bind指令，或者通过语法糖的形式，那么将数据和表单绑定的时候，可以通过专用指令v-model，v-model可以实现表单和数据的双向绑定。

> 数据和普通DOM元素绑定，用mustache语法；数据和表单绑定的时候，用v-model.

```html
    <div id="app">
        <input type="text" v-model="msg">
        <h2>{{msg}}</h2>
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

就这么简单的就实现了表单和数据的双向绑定。双向绑定，指的是表单数据的变化，会映射到data中数据的变化，同样，data中数据的变化也会在表单中体现出来。看demo：

![表单通过v-model的双向绑定](../../public/images/i74.png)

我们在表单输入框中输入文字的时候，下面对应的内容会跟着变化，说明表单中数据的变化已经响应到了data数据；我们在开发者工具中通过修改app.msg来修改值，修改后的值也直接在表单中体现了出来，说明表单通过v-model实现了和数据的双向绑定。

**那么表单是怎么通过v-model实现的双向绑定呢？**

表单通过v-model实现了表单和数据的双向绑定，其实是做了两件事情，我们也可以简单的认为v-model是做的这两件事的一个语法糖。

1. 首先通过v-bind质量将数据和表单的value属性进行绑定；

2. 通过监听表单（以输入控件input为例）的input事件，实现数据的变化。

通过上述两件事情，就实现了表单和数据的双向绑定。

```html
    <div id="app">
        <!--通过v-bind指令实现了数据和表单value属性的绑定，通过监听input控件的input输入事件，实现了input控件修改后的value和data的改变-->
        <!--通过v-bind和value属性的绑定、监听input控件的输入事件input实现了表单和数据的双向绑定-->
        <input type="text" :value="msg" @input="valueChange">
        <h3>换一种方式：@input="msg = $event.target.value"</h3>
        <input type="text" :value="msg" @input="msg = $event.target.value">
        <h2>{{msg}}</h2>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                msg: "Hello Vue!"
            },
            methods: {
                valueChange(event) {
                    this.msg = event.target.value;
                }
            }
        });
    </script>
```

v-model的双向绑定，除了可以应用到input，也同样适用textarea控件。

```html
    <div id="app">
        <textarea v-model="msg"></textarea>
        <textarea :value="msg" @input="valueChange"></textarea>
        <h2>{{msg}}</h2>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                msg: "Hello Vue!"
            },
            methods: {
                valueChange(event) {
                    this.msg = event.target.value;
                }
            }
        });
    </script>
```

**v-model和radio的配合使用**

v-model和radio配合使用的时候，同一组radio需要绑定同一个变量，这样就可以实现radio的单选效果。

如果我们期望有默认的选中值，如性别选择中期望默认选择“男”，我们就可以直接在数据中定义变量值为“男”就可以了。

另外就是在常规的HTML中，在同一个选项组中，需要使用name属性来标识，但是在vue中，如果使用了v-model绑定数据了，那么只需要这个选项组中绑定了同一个变量就可以了，那么属性可以省略。当然了，不缺省name属性也是完全可以的。

```html
    <div id="app">
        <ul>
            <li>
                <label for="male">
                    <input type="radio" name="gender" value="男" v-model="sex" id="male">男
                </label>
            </li>
            <li>
                <label for="female">
                    <input type="radio" name="gender" value="女" v-model="sex" id="female">女
                </label>
            </li>
        </ul>
        <h3>你选择了：{{sex}}</h3>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                sex: "男"
            },
            methods: {}
        });
    </script>
```

**v-model和checkbox的配合使用**

checkbox一般情况下，有两种使用场景，一种是单选的可反选形式，如是否同意隐私协议，然后才可以进行下一步之类的场景；另一种就是真正的多选了，如收集用户的爱好、多个可选条件中选择适合自己的选项等。

单选场景下，一般会通过v-model绑定一个Boolean值，来确认是否选中了；在多选的场景下，一般情况下会通过v-model绑定一个数组，来收集已经选择的项。

```html
    <div id="app">
        <!--单选复选，如是否同意协议、隐私协议之类的-->
        <div class="single">
            <label for="is-agree">
                <input type="checkbox" v-model="isAgree" id="is-agree">是否同意
            </label>
            <h2>你的选择：{{isAgree}}</h2>
            <button :disabled="!isAgree">下一步</button>
        </div>
        <!--多个项目选择-->
        <div class="multi">
            <h3>你有什么爱好？</h3>
            <div class="hobby">
                <input type="checkbox" value="足球" v-model="hobbies">足球
                <input type="checkbox" value="篮球" v-model="hobbies">篮球
                <input type="checkbox" value="羽毛球" v-model="hobbies">羽毛球
                <input type="checkbox" value="跳绳" v-model="hobbies">跳绳
                <input type="checkbox" value="看电影" v-model="hobbies">看电影
            </div>
            你选择的爱好：{{hobbies}}
        </div>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                isAgree: false,
                hobbies: []
            },
            methods: {}
        });
    </script>
```

**v-model之select**

select和checkbox基本相同，也有单选和复选的使用场景。

> vue中，select的默认选项，是通过数据来控制，通过v-model绑定的变量的默认值，就是select控件的默认值，而不是通过select控件的selected属性控制默认选项。

```html
    <div id="app">
        <!--单选场景-->
        <div class="single">
            <select v-model="city">
                <option value="全部">全部</option>
                <option value="河北">河北</option>
                <option value="山东">山东</option>
                <option value="北京">北京</option>
            </select>
            <h3>你选择的城市是：{{city}}</h3>
        </div>
        <!--多选场景-->
        <div class="multi">
            <select v-model="cities" multiple>
                <option value="全部">全部</option>
                <option value="河北">河北</option>
                <option value="山东">山东</option>
                <option value="北京">北京</option>
            </select>
            <h3>你选择了:{{cities}}</h3>
        </div>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                city: "全部", // 单选场景下，使用字符串，本demo中给了一个默认值，在vue中，给select一个默认值，是在数据中给定默认值，而不是通过select控件的selected属性
                cities: ["北京"] // 给一个默认的选项
            },
            methods: {}
        });
    </script>
```

**v-model之值绑定**

vue中有这么一个概念叫值绑定，看文档看的云里雾里，没有看的很明白，这里将我的一些理解，以案例的形式简单描述一下。

比如我们经常会见到图中的场景，就是选择城市区域。

![v-model之值绑定，选择城市区域](../../public/images/i75.png)

在做这样的技术实现的时候，如果我们不做好技术实现方案，可能就直接把这样的几个城市直接写死到代码中了，像这样：

```html
        <label for="北京">
            <input type="checkbox" id="北京" value="北京" v-model="cities">北京
        </label>
        <label for="石家庄">
            <input type="checkbox" id="石家庄" value="石家庄" v-model="cities">石家庄
        </label>
        <label for="天津">
            <input type="checkbox" id="天津" value="天津" v-model="cities">天津
        </label>
        <label for="成都">
            <input type="checkbox" id="成都" value="成都" v-model="cities">成都
        </label>
        <h4>你选择了的城市有：{{cities}}</h4>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                cities: []
            },
            methods: {}
        });
    </script>
```

这里先不要纠结id属性的合理性。然后绑定下v-model,我们就实现了选中城市数据的绑定，能获取到页面中选中的城市数据。效果看起来很完美。

但是很多时候，这些城市数据并不是固定的，而是这些城市数据都是从后台系统中配置的，我后台系统中配置了新的城市，新的城市就需要展示出来，已经展示的城市不需要了，就不需要在页面中展示了。那我们不能说每次有城市数据变化的时候，都要提新需求，来次代码开发上线流程吧。明显的不合理。我们更加期望的是城市从后台数据，在后台控制城市数据的展示与否。那么上面的实现方式就不那么灵活了。

我们直接看实现方式吧：

```html
    <div id="app">
        <!--v-model值绑定-->
        <div>
            <label :for="item" v-for="item in originCities">
                <input type="checkbox" :id="item" :value="item" v-model="cities">{{item}}
            </label>
            <h4>你选择了:{{cities}}</h4>
        </div>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                originCities: ["北京", "石家庄", "天津", "成都", "上海", "重庆", "武汉", "深圳", "广州"],
                cities: []
            },
            methods: {}
        });
    </script>
```

现在的实现方案，已经满足了业务方的需求。

我们通过一个变量保存原始城市数据（当然了，是从服务端获取的），然后以此为依据遍历出来所有的城市数据。然后再通过v-model绑定选中的城市，实现了选中的值和DOM元素的绑定。

可能我的这种理解不科学，但是理解起来更容易一些。

**v-model修饰符**

.lazy

默认情况下，通过v-model绑定的表单，和数据双向绑定，是时时响应的，好处是只要一方有了数据的变化，我在另一个端就能即刻发现数据的变动，但是也有一个不好的地方，就是有的场景下，我并不希望这种变化是时时的，而是希望能够在表单输入完成的时候，再发生一次表单和数据的绑定、交互。这个时候，只要给v-model添加一个修饰符.lazy就可以了。

```html
    <div id ="app">
        <input type="text" v-model.lazy="msg">
        <h2>{{msg}}</h2>    
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

v-model添加了.lazy修饰符后，只有在失去焦点或者敲击回车时才会发生数据的交互。

.number

在一些表单输入中，我们希望输入数字类型。我们知道，如果期望输入的值是number类型，那么将input的type属性设置成number就可以了。但是在vue中绑定了v-model属性后，就有问题了。v-model绑定的变量，默认都都是string类型，如果我们希望v-model绑定的变量是number类型的，那么给v-model添加.number修饰符就可以了。

```html
    <div id ="app">
        <input type="number" v-model="age">
        <h2>你的年龄：{{age}} - {{typeof age}}</h2>
    </div>

    <script>
     //创建Vue实例,得到 ViewModel
     let app = new Vue({
        el: '#app',
        data: {
            age: 12
        },
        methods: {}
     });
    </script>
```

![v-model默认绑定string类型](../../public/images/i76.png)

看demo，默认情况下，我们可以看到age字段是number类型，应该是没问题的，但是只要我们在输入框重新输入一个数字，那么这个修改后的数字，就变成了string类型了。这也印证了我们上面的结论，v-model绑定的变量，默认都是string类型。那么接下来就需要解决问题了，就是希望默认展示的是number类型的，修改后的数字，也是number类型的，只需要给v-model添加.number修饰符即可。

```html
    <div id ="app">
        <input type="number" v-model.number="age">
        <h2>你的年龄：{{age}} - {{typeof age}}</h2>
    </div>

    <script>
     //创建Vue实例,得到 ViewModel
     let app = new Vue({
        el: '#app',
        data: {
            age: 12
        },
        methods: {}
     });
    </script>
```

![v-model添加.number修饰符，绑定number类型](../../public/images/i77.png)

.trim

在input输入框输入内容的时候，有些时候可能由于输入的疏忽，或者操作失误，或者设备的原因，可能会在开始输入或者结束输入的时候，会多出来一些空格，如下案例：

![开始多出了空格](../../public/images/i78.png)

在输入的时候，多输出了一些空格，虽然在浏览器中展示的时候，只展示了一个空格的位置（如图中2的位置，浏览器在展示字符串的时候，默认给移除掉了开始和结尾的空格，当有多个空格的时候，只保留一个展示），但是实际上是多个空格存在的（如图中3的位置）。一些场景中，我们并不希望这些空格存在，而不仅仅是展示了一个就可以了。只需要给v-model添加.trim修饰符就可以了。

```html
    <div id="app">
        <!--trim-->
        <input type="text" v-model.trim="message">
        <h2>输入的信息:{{message}}</h2>
    </div>

    <script>
        //创建Vue实例,得到 ViewModel
        let app = new Vue({
            el: '#app',
            data: {
                msg: "Hello Vue!",
                age: 12,
                message: ""
            },
            methods: {}
        });
    </script>
```

添加了.trim修饰符后，输入框在开始和结束输入的空格，在输入框失去焦点后，都会自动消失，数据也不会保存这些开始和结束位置的空格。