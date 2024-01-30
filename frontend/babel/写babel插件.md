### AST

AST,抽象语法树.

**抽象语法树是什么?**

- 抽象语法树是源代码结构的一种抽象表示;

- 它以树状的结构表现编程语言的语法结构,树上的每个节点都表示源代码中的一种结构;

- 每个包含type属性的数据结构,都是一个AST节点;

以下是一个简单空函数的AST语法树:

```js
function test(){
	alert("Hello World!");
}
```

<img src="./images/i1.png" width="500" />