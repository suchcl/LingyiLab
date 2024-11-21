Hook是使用javascript函数定义的，它们代表了一种特殊的可重用的UI逻辑，并且对它们可以被调用的位置有限制。

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



React开发中，有很多的hooks，但是对于刚接触react的开发者来说，可以先从以下几个hooks入手，比较常用。

### 1. react内置的10个hooks

1. useState

2. useEffect

3. useContext

4. useReducer

5. Memo

6. useMemo

7. useCallback

8. useRef

9. useImperativeHandle

10. useLayoutEffect

### 2. Hooks的使用规则

Hooks就是javascript函数，使用的时候有2个需要特别注意的规则：

1. 只能在函数的最外层调用hooks。不能在