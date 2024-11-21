Hook是使用javascript函数定义的，它们代表了一种特殊的可重用的UI逻辑，并且对它们可以被调用的位置有限制。

参考链接：[https://zh-hans.react.dev/reference/rules/rules-of-hooks](https://zh-hans.react.dev/reference/rules/rules-of-hooks)

1. 只在顶层调用hook

在React中，以use开头命名的函数被称为Hook。

**不要在循环、条件语句、嵌套函数或try/catch/finally代码块中调用Hook。**只能在函数式组件的顶层使用Hook，且在任何提前返回之前。只能在React渲染函数组件时调用。

```tsx
function add(a,b){
    return a + b;
    const c = useContext(ThemeContext); // 这是一种错误的使用hook的方式，不能载return之后使用Hook
}
```

2. 仅在React函数中调用hook

不能在普通的javascript函数中调用Hook。可以调用Hook的地方：

- React函数式组件中调用

```tsx
function setOnlineStatus() {
  const [isOnline, setIsonline] = useOnlineStatus(); // 这里不能调用Hook，因为这不是一个React组件，也不是一个自定义Hook
}
```

- 在自定义的Hook中调用Hook

```ts
import { useEffect, useState } from "react";
function useOnlineStatus() {
    const [isOnline, setIsOnline] = useState(true);
    useEffect(() => {
        const handleOnline = () => {
            setIsOnline(true);
        };
        const handleOffline = () => {
            setIsOnline(false);
        };
        window.addEventListener("online", handleOnline);
        window.addEventListener("offline", handleOffline);

        return () => {
            window.removeEventListener("online", handleOnline);
            window.removeEventListener("offline", handleOffline);
        };
    }, []);
    return isOnline;
}

export { useOnlineStatus };
```

这种在自定义hook的实现中，也可以调用Hook。
