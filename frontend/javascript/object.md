### object常用方法

1. Object.create():以一个现有对象作为原型,创建一个新的对象.

```js
const Person = {
    name: "Nicholas Zakas",
    age: 18,
    sayHello() {
        console.log(`Hello,${this.name}`)
    }
};

const p = Object.create(Person)
p.sayHello(); // Hello,Nicholas Zakas
```

以现有的对象Person为原型创建了一个新的对象p,新的对象p拥有已有对象Person的所有属性和方法.

**语法**

Object.create(proto)

Object.create(proto,propertiesObject)


**参数**

proto: 创建的新对象的原型对象,为Object或者null,否则会报异常TypeError

propertiesObject:可选,如果参数被指定且不为undefined,则传入对象可枚举的自有属性,然后这些枚举的自有属性将成为新创建对象的属性.

```js
const Person = {
  name: "Nicholas Zakas",
  age: 18,
  sayHello() {
    console.log(`Hello,${this.name}`);
  },
};

const cp = Object.create(Person, {
  job: {
    value: "Engineer",
    writable: true,
    enumerable: true,
    configurable: true
  },
  salary: {
    value: 1000,
    writable: true,
    enumerable: true,
    configurable: true
  }
});

console.log(cp.job); // Engineer
```