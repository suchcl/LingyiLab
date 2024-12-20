javascript判断一个变量是不是一个对象，在数据处理的时候经常遇到。那么可以通过什么方式判断一个变量是不是一个对象呢？

1. typeof关键字

2. instanceof关键字

3. Array.isArray()

4. Object.prototype.toString()方法

5. 使用第三方库如lodash提供的方法

**总结**

判断一个变量是不是对象，有多种判断方法，通常情况下，使用Object.prototype.toString方法可以准确的判断一个变量的类型。