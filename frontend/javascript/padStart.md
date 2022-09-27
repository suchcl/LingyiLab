padStart是ES2017版本中引入的一个方法，其功能是用指定的字符串填充到一个字符串中，以让当前的字符串达到预期的长度。

通过指定字符串拼接当前字符串到指定长度的方法，有2个，分别为：

padStart: 拼接的字符串从左侧开始拼接，一直拼接到指定的长度，如果长度不够，则拼接的字符可以循环、重复多次使用

padEnd: 拼接的字符串从当前字符串的结尾(也就是右侧)开始拼接，直到拼接到指定的长度，如果长度不够，则拼接字符串可以循环、重复使用

```js
let str = "hello";
console.log(str.padStart(10,"GaGa")); // yanyahello
console.log(str.padEnd(10,"GaGa")); // helloGaGaG
```

语法：

```markdown
padStart(targetLength) 从左侧开始拼接到指定的长度   因为没有指定要拼接的字符串，所以拼接的字符是空字符串

padEnd(targetLength,padString)：通过指定的字符串拼接到指定的长度
```

如果只指定了长度参数，如padStart(targetLength)，那么和将第二个参数指定为空字符串的效果相同，如:padStart(targetLength, "");

和padStart()从字符串起始位置开始拼接对应的，还有一个padEnd()方法，参数类型和功能相同，就是拼接的位置不同。

```markdown
padEnd(targetLength)

padEnd(targetLength, padString);
```

> pad:在英语中是衬垫的意思，用在字符串拼接，也是表示垫衬位置的意思吧。