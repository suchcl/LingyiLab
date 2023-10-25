### 使用css绘制箭头

项目中经常会出现一些箭头的icon，可以使用图片，但是无形中增加了项目质量和请求数，如果能通过代码实现的效果，还是尽量使用代码去实现它。

```css
.icon_row {
    display: inline-block;
    border-top: 2px solid;
    border-right: 2px solid;
    width: 12rpx;
    height: 12rpx;
    border-color: #b07146;
    transform: rotate(45deg);
}
```

DOM结构如下:

```html
<span class="icon_row"></span>
```

实现一个类似如下的效果: ![css实现的箭头](./images/i13.png)