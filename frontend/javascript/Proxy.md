### Proxy

Proxy是javascript的一个内置对象，它允许我们创建一个对象的代理，用于拦截并自定义该对象的基本操作如属性查找、赋值和函数调用等。

```js
const target = { count: 0 };

const handler = {
    get(target, key, receiver) {
        console.log(`读取属性: ${key}`);
        return Reflect.get(target, key, receiver);
    },
    set(target,key,value, receiver){
        console.log('设置属性',key,value);
        return Reflect.set(target,key,value,receiver);
    }
};

const proxy = new Proxy(target, handler);
proxy.count; // 输出: 读取属性： count
proxy.count = 1; // 写入: 写入、设置属性： count

proxy.name = "Nicholas Zakas";
proxy.age = 16;
console.log('%c [  ]-21', 'font-size:13px; background:pink; color:#bf2c9f;', proxy.name); // Nicholas Zakas
```

**代码解释**

- target：是一个普通的对象，是想要代理的原始对象

- handler：一个处理器对象，包含各种拦截操作的处理函数，案例中用到了get和set

    * get函数会在访问属性时被调用，它接收3个参数：

        - target：被代理的原始对象

        - prop：正在访问的属性名称

        - receiver：通常是代理对象本身或者继承自代理对象的对象

    * set函数会在设置属性时被调用，它接收4个参数：
        - target：被代理的原始对象
        - prop：正在设置的属性名称
        - value：设置的值
        - receiver：通常是代理对象本身或者继承自代理对象的对象

- const proxy = new Proxy(target, handler);，使用Proxy的构造函数创建了一个代理对象

- proxy.count = 1设置属性值时触发set函数

- console.log(proxy.name) 读取属性时触发get函数

**Proxy支持13种拦截操作**

1. get(target, propKey, receiver)

2. set

3. has

4. deleteProperty

5. ownKeys

6. getOwnPropertyDescriptor

7. defineProperty

8. preventExtensions

9. getPrototypeOf(target)

10. isExtensible(target)

11. setPrototypeOf(target,prototype)

12. apply(target, object, args)

13. construct(target, args)