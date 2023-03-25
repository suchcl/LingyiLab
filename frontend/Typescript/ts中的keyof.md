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

