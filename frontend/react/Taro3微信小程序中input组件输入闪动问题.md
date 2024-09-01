### Taro3 React微信小程序input组件输入闪动问题

Taro3,在微信小程序中使用Input组件,有的时候会出现闪动现象,这个时候可以使用CustomWrapper将自定义组件包裹一层,然后就可以解决这个问题.如:

```jsx
import { CustomWrapper } from "@tarojs/components";
<CustomWrapper>
    <Call />
</CustomWrapper>
```

具体可以参考:
1. [https://taro-docs.jd.com/blog/2021-03-10-taro-3-1-lts#2-%E6%96%B0%E5%A2%9E%E5%B0%8F%E7%A8%8B%E5%BA%8F%E6%80%A7%E8%83%BD%E4%BC%98%E5%8C%96%E7%BB%84%E4%BB%B6-customwrapper](https://taro-docs.jd.com/blog/2021-03-10-taro-3-1-lts#2-%E6%96%B0%E5%A2%9E%E5%B0%8F%E7%A8%8B%E5%BA%8F%E6%80%A7%E8%83%BD%E4%BC%98%E5%8C%96%E7%BB%84%E4%BB%B6-customwrapper)

2. [https://github.com/NervJS/taro/issues/9664](https://github.com/NervJS/taro/issues/9664)