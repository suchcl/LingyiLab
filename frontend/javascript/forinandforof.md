### for……in、for……of

for……in、for……of都用于数据的遍历，但是侧重点有所不同

**for……in**

for……in常用于遍历对象，遍历的关键字为对象的属性

```js
const student = {
    name: "John",
    age: 20,
    grade: "A"
};
for(const key in student){
    console.log(key); // name、age、grade
}
```

for……in也可以用于遍历数组，但是遍历的关键字为数组的索引，而不是数组的数据项

```js
const tempData = [
    {
        name: "John",
        age: 20,
        grade: "A"
    },
    {
        name: "Nicholas Zakas",
        age: 16,
        grade: "B"
    }
];
for(const idx in tempData){
    console.log(idx); // 0、1
}
```

**for……of**

for……of常用于遍历数组，遍历的数据为数组项

```js
const tempData = [
    {
        name: "John",
        age: 20,
        grade: "A"
    },
    {
        name: "Nicholas Zakas",
        age: 16,
        grade: "B"
    }
];
for(const item of tempData){
    console.log(item);
}
```

for……of除了遍历数组以外，也用来遍历字符串、Set和Map。