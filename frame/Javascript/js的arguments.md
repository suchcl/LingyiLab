### 什么是arguments

arguments，是一个类数组对象，代表传递给一个function的参数列表。

看案例：

```javascript
function printArgs() {
  console.log(arguments);
}
printArgs("a", "A", 0, { foo: "Hello,arguments" });

// 执行结果： ["a", "A", 0, { foo: "Hello,arguments" }]
```

一看，就是一个数组，起码看起来像一个数组，但其实它不是一个数组，可以验证一下：

```javascript
function printArgs() {
  console.log(arguments);
  console.log(arguments instanceof Array); // false,说明arguments不是Array，不是数组
}
printArgs("a", "A", 0, { foo: "Hello,arguments" });
```

从内容上来看，可以很清晰的看出来，arguments就是函数执行时传入的所有的参数。这些参数，也可以按照数组的方式获取到：

```javascript
function printArgs() {
  console.log(arguments);
  console.log(arguments instanceof Array); // false,说明arguments不是Array，不是数组
  console.log(arguments[0], arguments[3]); // a, { foo: "Hello,arguments" },说明通过arguments对象的下标取到了值
}
printArgs("a", "A", 0, { foo: "Hello,arguments" });
```

### arguments操作

arguments是一个类数组对象，它有一些属性

#### length

可以通过length属性获取函数参数列表的个数。

#### arguments转数组

#### 修改arguments的值

#### 将参数从一个函数传递到另一个函数

#### arguments与重载


### ES6中的arguments

#### 扩展操作符...arguments

#### rest参数

#### 默认参数

#### arguments转数组

### 数组与类数组对象