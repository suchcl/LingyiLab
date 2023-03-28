### ts中的keyof

keyof是ts在2.1版本中引入的一个属性，用来遍历某个类型的所有键类型并由这些键组成一个新的联合类型。

Javascript可以通过Object.keys()方法获取一个对象的属性键值并由这些属性键值组成一个数组。

```js
const obj = {
    name: "Dave Herman",
    age: 12,
    height: 182,
    gender: 'male'
};
console.log(Object.keys(obj)); // ['name', 'age', 'height', 'gender']
```

**Typescript中的keyof可以用来做什么**

js中的Object.keys()可以用来获取对象的属性键值，那么ts中的keyof到底可以用来做什么呢？

ts中的keyof可以用来获取类型中的键值：注意是获取类型中的键值，不是对象中的键值。

ts中的类型可以通过interface和type定义。如下面的是自定义类型：

```ts
interface Student {
    username: string;
    age: number;
    mobile: string;
    code: string;
}

type Workers = {
    name: string;
    salary: number;
};
```

demo中的Student和Workers都是自定义的类型，都可以通过keyof获取到类型中的键值。

**获取到类型中的键值怎么使用呢？**

通过keyof获取到的键值，有什么用呢，可以怎么用呢？

通过keyof获取到的类型的键值的集合，可以组成一个由这些获得的键值组成的一个字面量的联合类型。

注意：这些键值就是字面量联合类型的类型值

```ts
type Workers = {
    name: string;
    salary: number;
};
type workerTye = keyof Workers;
const w:workerTye = 'salary';
```

这是一个简单的使用，workerTye的值一个由类型Workers的键值name和salary组成的联合类型:'name' | 'salary'.然后我们可以通过联合类型workerTye来约束变量了。如：

```ts
const w:workerTye = 'salary';
```

通过类型workerTye约束的变量w只有2个合法的值可选，分别为name和salary。

这就是ts中keyof的简单用法。

keyof的使用过程中也可以使用泛型来做简单的封装，可以有更好的适用性

> js中Object.keys()用来获取对象的属性，ts中的keyof用来获取类型的属性,都是获取的key。
> Object.keys()和keyof的操作对象不同，Object.keys()操作的是对象，keyof操作的是一个类型，不能操作对象。