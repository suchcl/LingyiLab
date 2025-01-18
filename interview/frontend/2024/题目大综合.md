1. ts中any、never和unknown的区别

- any:最灵活的类型，表示任意类型的值

    使用any类型时，ts将绕过编译器的类型检查，允许其进行任何操作，包括赋值、函数调用、属性访问等，不会产生编译错误

- never:表示永远不会发生的值的类型

    never常用于表示函数的返回类型，表示函数永远不会返回(如抛出了异常或进入了无限循环)，或者表示类型无法达到如在联合类型中的穷尽性检查中

- unkown:TS3.0引入的一个类型，表示一个未知的类型

    与any不同，unkown类型的变量不能直接操作，需要先进行类型检查或者断言确保了操作的安全性以后才可以进行操作

    ```ts
    var value;
    value = 10;
    value = "hello";
    if (typeof value === "number") {
        var v = value.toFixed(2);
        console.log('%c [ v ]-6', 'font-size:13px; background:pink; color:#bf2c9f;', v);
    }else if (typeof value === "string") {
        console.log('%c [ value.toLocaleUpperCase() ]-9', 'font-size:13px; background:pink; color:#bf2c9f;', value.toLocaleUpperCase());
    }

    // unknown类型，需要断言后才可以操作
    let sv:unknown = "这是一个字符串";
    console.log((sv as string).length);
    ```

2. ts中的类型断言

    ts有多种类型断言方式：尖括号断言、as关键字断言、类型守卫断言、非空断言。

    - 尖括号类型断言

    ```ts
    let sv:unknown = "这是一个字符串";
    console.log((<string>sv).length);
    ```

    - as关键字断言

    ```ts
    let sv: unknown = "这是一个字符串";
    console.log((sv as string).length);
    ```

    - 类型守卫断言



    - 非空断言:后缀!

    当能够确认一个可能是null或者undefined的变量不是null或者undefined时，就可以使用非空断言操作符!.

    ```ts
    let na: string | null = null;
    let nna: string = na!;
    ```

    变量na是一个联合类型的变量，它可以是一个string类型，也可以是一个null值。有另外一个string类型的变量nna，需要把na赋值给nna，那么就只能在na是string类型的时候才可以，这个时候就可以给na后面加1个非空断言操作符!，这样就可以把一个string类型的值重新赋值给nna。

    > 使用非空断言时要非常小心，因为变量实际上是可以为null或者undefined的，如果变量的值真的是null或者undefined了，那么使用非空断言操作！就会报错了。

3. token无感刷新

4. 前端本地存储方案，区别，关闭浏览器后会消失吗？

5. 组件的通信方式有哪些？

6. React组件的通信方式

7. 防抖和截流

8. React中的Fiber架构

9. 判断是否为数组的方法

10. 什么是use strict?使用了它有什么好处和坏处？

11. 编写一个b继承a的方法

12. 判断一个字符串中出现次数最多的字符，并判断出现次数。

var str = "aaaaaaaassssssssdbbbbbbbddddssssdfffwwwwwwwwwww";

13. 