### 为什么React组件中没有用到React也要导入呢?

在React17版本之前使用的babel便衣方式是classic,这个编译方式会将页面的每个元素都是用React.createElement()方法转换成对应节点,而在React17之后使用的是automatic编译模式,这种编译模式采用jsx-runtime方法转换节点,且这种编译模式会自动将jsx-runtime引入到文件中,所以在React17之后,如果React组件中没有显示的使用React,那么就不需要在页面顶部导入React了. 

```jsx
import Reract from "react";
```