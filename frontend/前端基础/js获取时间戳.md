### js中获取时间戳的方式

在前端开发中，经常需要获取时间戳，那么在前端的开发中，都可以通过哪些方式获取时间戳呢？常用的有如下几种方式：

```js
// 通过+方式转换时间类型为时间戳
+new Date()

// 通过Date类型的valueOf()方法转换时间类型为时间戳
new Date().valueOf()

// 通过getTime()方法获取时间戳
new Date().getTime()

// 通过Date类型的now()方法获取当前时间戳
new Date().now()

// 通过Date类型和数值类型的计算得到时间戳
new Date() * 1
```

这几种方式都可以得到一个时间戳，都是简单有效的方式。

### +new Date()是什么意思？

js中，在某个数据类型前面使用+，这个操作的目的是为了将该数据类型转换为Number类型，如果转换失败，则返回NaN。

```js
+new Date()
```
案例的意思是将new Date()的值转换为Number类型，那么就会调用Date的valueOf()方法，获取到Date对象的原始值。所以，+new Date()获取到的值，和new Date().valueOf()的值，是一样的。

### 时间格式化

根据时间戳将时间格式化为：2023-04-14 16:41:52格式

```js
// 目标格式：2023-04-14 16:41:52
function timeFormat(timestamp) {
    // 处理下没有传值的情况
    if(!timestamp){
        return "";
    }

    //时间戳为10位需*1000，时间戳为13位的话不需乘1000 
    var date = new Date(timestamp);
    var year = date.getFullYear(),
        month = ("0" + (date.getMonth() + 1)).slice(-2),
        sdate = ("0" + date.getDate()).slice(-2),
        hour = ("0" + date.getHours()).slice(-2),
        minute = ("0" + date.getMinutes()).slice(-2),
        second = ("0" + date.getSeconds()).slice(-2);
    var result = year + "-" + month + "-" + sdate + " " + hour + ":" + minute + ":" + second;
    return result;
}
```