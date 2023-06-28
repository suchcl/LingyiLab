### includes()

includes()是ES7中新增的方法，可以判断数组或者数组中是否包含某个元素，如果包含，返回true，否则返回false。

```js
const str = "The quick brown fox jumps over the lazy dog";
console.log(str.includes("bros")); // false
```

数组通过使用includes()判断是否包含一个数组项：

1. 可以使用includes()判断是否包含一个基本数据类型的元素；

2. 如果被判断的元素是一个非基础数据类型，如一个对象类型的数组项，则直接通过includes()会直接返回false

这是因为在使用includes()判断的时候，是使用的全等(===)判断，同时判断类型相等和值相等；

所以在数组判断是否包含一个普通数据类型元素的时候，可以直接使用includes()，如果是对象类型元素的时候，可以通过find()方法来实现。

```js
const user = [
    {
        id: 1,
        name: "Nicho",
        age: 12
    },
    {
        id: 2,
        name: "Herro",
        age: 13
    }
];

const tp = {
    id: 1,
    name: "Nicho",
    age: 12
};
console.log(user.includes(tp));
console.log(user.find(item => item.id === tp.id));
console.log(user);
const arr = [1, 2, 3];
console.log(arr.includes(1));
```

随着标准能力的完善，在实际开发中还是节省了不少的精力的。