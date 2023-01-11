### Object.freeze()

我们都知道在es6以后，js中也有了常量和变量的区分了，通过const关键字定义常量，通过let关键字定义变量(var也可以，只是在现在的前端工程项目中不太建议使用var了)。

既然通过const定义的基本类型的变量，也就是常亮，值不能被修改，但是通过const定义的对象字面量，虽然对象本身不能被修改，但是对象中的属性是可以被修改的，也可以新增属性、删除属性(通过delete操作符)，原来的对象属性也可以改变值。

```js
const obj = {
    name: "Nicholas Zakas",
    age: 18
};

obj.name = "Jenn Lukas";
obj.job = 'Teacher';
console.log("age1:",obj.age); // 18
delete obj.age;
console.log("name:", obj.name); // Nicholas Zakas
console.log("job:", obj.job); // Teacher
console.log("age2:", obj.age); // undefined

obj = { // Uncaught TypeError: Assignment to constant variable. 报错了
    height: 182
};
```

demo中，通过const声明的对象字面量，对象字面量本身是不能被修改的，但是对象中的属性值是可以被修改的，对象属性也可以被删除和新增。

那么有没有办法让对象字面量也像常规数据类型的常量一样不能被修改呢？

可以通过Object.freeze()方法实现对对象字面量的冻结，从而实现对象的属性，具体为：

1. 不能新增属性；

2. 不能删除已有的对象属性；

3. 不能修改已有属性的值；

4. 不能修改原型；

5. 不能修改已有属性的可枚举性、可配置性和可写性；

```js
const obj = {
    name: "Nicholas Zakas",
    age: 16
};

// 冻结obj对象
Object.freeze(obj);
delete obj.age;
console.log("age:", obj.age); // 16,说明delete obj.age没有成功，因为obj对象被冻结了
obj.name = "Jenn Lukas";
console.log("name:", obj.name); // Nicholas Zakas, age属性也没有被修改成功
```

### Object.freeze()冻结数组

Object.freeze()除了可以冻结对象字面量外，也可以冻结数组。

```js
const arr = [1,2,3];
arr[3] = 4;
console.log("arr:", arr); // 1,2,3,4,arr数组成功的新增了一元素

// 冻结数组
Object.freeze(arr);
arr[4] = 5;
console.log("arr2:", arr); // 1,2,3,4   arr[4]新增元素5没有打印出来，说明该元素没有新增成功
```
