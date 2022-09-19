### react组件化的组件中，怎么使用多个class？

在常规的DOM中，如果某个元素需要使用多个类名的时候，直接给class属性赋多个值就可以了，如:

```html
<didv class="box header"></div>
```

可在react中，怎么给react元素设置多个类名呢？

可以参考下例:

```tsx
<div className={`${styles['user-info']} ${styles.consultant}`}>
</div>
```