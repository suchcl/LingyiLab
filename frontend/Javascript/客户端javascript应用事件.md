<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. 事件介绍](#1-%E4%BA%8B%E4%BB%B6%E4%BB%8B%E7%BB%8D)
  - [1.1 事件类型](#11-%E4%BA%8B%E4%BB%B6%E7%B1%BB%E5%9E%8B)
  - [1.2 事件目标](#12-%E4%BA%8B%E4%BB%B6%E7%9B%AE%E6%A0%87)
  - [1.3 事件处理程序或事件监听器](#13-%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E7%A8%8B%E5%BA%8F%E6%88%96%E4%BA%8B%E4%BB%B6%E7%9B%91%E5%90%AC%E5%99%A8)
  - [1.4 事件对象](#14-%E4%BA%8B%E4%BB%B6%E5%AF%B9%E8%B1%A1)
  - [1.5 事件传播](#15-%E4%BA%8B%E4%BB%B6%E4%BC%A0%E6%92%AD)
- [2. 事件类别](#2-%E4%BA%8B%E4%BB%B6%E7%B1%BB%E5%88%AB)
- [3. 注册事件处理程序](#3-%E6%B3%A8%E5%86%8C%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E7%A8%8B%E5%BA%8F)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. 事件介绍

客户端 javascript 应用程序使用异步事件驱动的编程模型。在这种编程风格下，浏览器会在文档、浏览器或者某些元素或与之关联的对象发生的某些值得关注的事情时生成事件。

类似浏览器中这种有UI交互的事件模型，并不是web编程的专利，而是所有、任意具有图形用户界面的应用都是这样设计的。换句话说，界面就在那里等待用户与之交互，也或者可以说，这些UI就在那里等着事件发生，然后给出响应。

学习javascript事件，主要从事件类型、事件目标、事件处理程序或事件监听器、事件对象、事件传播这几个方面去关注、学习。

#### 1.1 事件类型

事件类型是一个字符串，表示发生了什么事情。如"mousemove"表示用户移动了鼠标，"click"表示用户点击了鼠标，"kehdown"表示用户按下了键盘上的某个键。因为事件类型是字符串，所以有时候也称它为事件名称，而且大多数时候，也确实在使用事件名称来讨论某种事件。

#### 1.2 事件目标

事件目标是一个对象，而事件就是发生在该对象上或者事件与该对象有关联。

说到某个事件，必须明确它的类型和目标，比如window对象上发生了加载(load)事件，按钮(button)上发生了点击(click)事件。

Window、Document、Element对象是客户端Javascript应用中最常见的事件目标，不过也有一些事件会发生在其他对象身上，如Worker对象是message事件的目标，这种事件在工作线程向主线程发送消息时会发生。

#### 1.3 事件处理程序或事件监听器

事件处理程序或事件监听器是一个函数，负责处理或响应事件。应用通过浏览器注册自己的事件处理程序，指定事件类型和事件目标。当事件目标上发生指定类型的事件时，浏览器会调用这个事件处理程序。当事件处理程序在某个对象上被调用时，我们说浏览器“触发”、“派发”或者“分配”了该事件。注册事件处理程序有不同的方式，具体注册事件处理程序的方式请看<a href="#注册事件处理程序">注册事件处理程序</a>

#### 1.4 事件对象

事件对象是与特定事件相关联的对象，包含有关事件的细节。事件对象作为事件处理程序的参数传入。

所有事件都具有type和target属性，分别表示事件类型和事件目标。

每种事件类型都为相关的事件对象定义了一组属性，比如有鼠标事件相关的事件对象包含鼠标指针的坐标，与键盘事件相关的对象包含与按下的键以及按住不放的修饰键的信息。

很多事件类型值定义几个标准属性，并没有其他有用信息，对这些事件，重要的是它们发生了，而不是它们发生的细节。

#### 1.5 事件传播

事件传播是一个过程，浏览器会决定在这个过程中哪些对象触发事件的处理程序。

对于Window对象上的load或Worker对象上的message等特定于一个对象的事件，不需要传播。

对于发生在HTML文档的某些事件，则会冒泡到根元素。

事件处理程序可以阻止事件传播，从而不让事件冒泡，也就不会在包含元素上触发处理程序。为此，事件处理程序需要调用事件对象上的一个方法，

除了事件冒泡形式，还存在另外一种事件传播形式，即事件捕获。注册在包含元素上的处理程序在事件被发送到实际目标之前，有机会拦截(捕获)事件。

有些事件有与之关联的默认动作，比如点击一个超链接，默认动作是让浏览器打开一个新的连接，加载一个新的页面。事件处理程序也可以调用事件对象的一个方法来阻止这个默认动作。有时阻止这个默认动作，也称为取消事件。

### 2. 事件类别

客户端Javascript支持的事件类别非常多，我们可以从常用的几种类别有重点的去学习

#### 2.1 设备相关输入事件

这类事件直接与特定的输入设备如鼠标或键盘相关，这类事件主要包括：

mousedown

mousemove

mouseup

touchstart

touchmove

touchend

keydown

keyup

……

#### 2.2 设备无关输入事件

这类事件并不与特定的输入设备直接相关：

click：一般来说是通过鼠标点击触发，但是也可能是通过键盘或轻击（移动设备）触发

input：是对keydown事件的设备无关的替代，既支持键盘输入，也支持剪切粘贴和文字的输入法等

pointerdown

pointermove

pointerup

#### 2.3 用户界面事件

UI事件的高级事件，通常在定义应用界面的HTML表单上触发。

focus：当文本域获得键盘焦点时触发

change：当修改了表单元素的显示的值时触发

submit：点击表单中的提交按钮时触发

#### 2.4 状态变化事件

这类事件不是直接由用户活动触发，而是由网络或者浏览器活动触发，这类事件表示某种声明周期或状态相关的变化。常用的事件有：

load

DOMContentLoaded

上面两个事件是Window和Document对象在文档加载结束时触发的。

online

offline

上述两个事件是在浏览器的网络连接变化时触发

popstate：浏览器的历史管理机制在浏览器做“后退”动作时触发

#### 2.5 API特定事件

有一些HTML及相关规范定义的Web API包含自己的事件类型。如HTML的<video>、<audio>元素定义了自己的一系列事件，waiting、playing、seeking、volumechange等，可以使用这些事件自定义媒体播放。

### 3. 注册事件处理程序

有两种注册事件处理程序的方法。

#### 3.1 设置作为事件目标的对象或文档元素的一个属性

这话说的有点绕，说的直白一点，就是给DOM元素设置一个事件属性，如onclick、onkeyup等等

按照惯例，事件处理程序属性的名字都是由“on”和事件类型名称组成，如onclick、onkeydown、onchange等等

注意：在原生的web中开发时，这些事件处理程序属性名是区分大小写的，必须全部为小写，即使事件属性名是由多个单词组成

> react中的事件处理程序属性是小驼峰的明明方式，如onClick、onChange等，这是原生的事件处理程序属性和react元素中事件处理程序属性的一个区别。
>
> 这里理解了，在学习或应用react时，就会很顺利，否则会感觉很蹩脚。

**设置事件处理程序：javascript**

```html
<button id="btn1">按钮1</button>
<script>
    window.onload = function () {
        console.log("文档已经全部加载完了");
    };

    const btn1 = document.querySelector("#btn1");
    btn1.onclick = function () {
        console.log("btn1触发了点击事件");
    };
</script>
```

设置事件处理程序属性，获取到DOM元素后，再给元素设置事件属性onclick，这种方式属于设置事件处理程序属性；

当事件目标是Window、Document、Element时，不用显示的获取DOM元素就可以直接给这些元素设置事件处理程序属性，这也是设置事件处理程序属性的一种方式。

**设置事件处理程序：HTML**

为文档元素的事件处理程序设置属性，就是直接在HTML文档中为对应的HTML标签设置事件属性，如：

```html
<button id="btn2" onclick="btn2Click()">按钮2</button>
```

现在的前端工程中，不推荐这样的事件处理技术，但是在一些场景中，仍然会使用，典型的代表是React。

在使用文档元素处理程序时，属性的值应该是一段js代码字符串。这段js代码应该是事件处理程序函数的函数体，不是完整的函数声明。也就是说这个事件处理程序函数代码，函数体没有外面的{}，也没有函数声明的关键字function。

```html
<button id="btn2" onclick="console.log('Hello,javascript!');">按钮2</button>
```

如果一个HTML事件处理程序属性包含多条js语句，则必须使用分号分隔这些语句，或者使用回车把这个属性值分成多行

```html
<button id="btn2" onclick="var name='Nicholas Zakas';console.log(name);">
    按钮2
</button>
<button
        onclick="var name='Hanmeimei';
                 var age=18;
                 console.log(name);
                 console.log(age);"
        >
    按钮3
</button>
```

在给HTML事件处理程序属性指定js代码字符串时，浏览器默认会把这个字符串转换为一个函数，大概的结构如下：

```javascript
function(event){
    // 函数体
}
```

这个event就是你的事件处理程序代码可以通过它去引用它去调用当前的事件对象。

严格模式下禁止使用with语句，但是在HTML属性中的Javascript没有严格模式。这样定义的事件处理程序将在一个可能会存在意外变量的环境中执行，因此可能会带来一些意外的bug或者安全隐患。这也是避免在HTML中编写事件处理程序的一个充分的理由。

#### 3.2 把处理程序传给这个对象或元素的addEventlistender()方法

任何可以作为事件目标的对象，包括Window、Document、Element对象以及所有的文档元素，都定义了一个名为addEventListener()的方法，可以用它来为目标对象绑定、注册事件处理程序。

addEventListener()接收3个参数：

第一个参数为事件类型，即事件名称。这个事件名称不包含作为HTML属性时的前缀on，仅仅就是事件名称，如click、change、keyup等

第二个参数为回调函数，即指定类型的事件发生时的处理函数。

第三个参数为一个布尔值或者对象：一般情况都是使用布尔值。默认是false，表示在事件冒泡阶段调用事件处理程序；true表示在事件捕获阶段调用事件处理程序。

```html
    <button id="btn">按钮1</button>
    <button id="btn2">按钮2</button>
    <script>
      const btn = document.querySelector("#btn");
      btn.addEventListener(
        "click",
        () => {
          console.log(this); // window
        },
        false
      );

      const btn2 = document.querySelector("#btn2");
      btn2.addEventListener(
        "click",
        function () {
          console.log(this); // <button id="btn2">按钮2</button>
        },
        false
      );
    </script>
```

一般情况下，不推荐使用设置事件处理程序属性的方式注册、绑定事件，因为使用事件处理程序属性有一个缺点，这种注册事件的方式只能绑定一个处理程序。

但是使用addEventListener()注册事件，可以绑定多个事件处理程序，且多个事件处理程序不会重写、覆盖之前的事件处理程序，更加灵活。
