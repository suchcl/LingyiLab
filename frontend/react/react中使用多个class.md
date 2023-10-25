### react组件化的组件中，怎么使用多个class？

#### 直接给class属性赋多个值

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

#### 通过classNames库

除了直接给class属性赋多个值外，也可以使用classNames库

```tsx
import classNames from "classNames";
<div className={classNames('icon_row', styles.icon_row)}></div>
```