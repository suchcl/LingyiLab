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

#### 通过一种变通的方式

可以通过在{}内可以执行js的能力,去通过一种变通的方式去实现在一个元素中添加多个class的能力.

```tsx
<View className={["detail-page", isFlag ? "detail-show" : ""].join(" ")}></View>
```

实现了在一个元素中根据状态值去配置多个class的能力.

#### 总结

以上三种方式都可以实现在一个元素中添加多个class的能力，可以根据实际需求选择使用哪种方式。