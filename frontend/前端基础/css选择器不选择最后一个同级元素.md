### css选择器选择当前元素列表的最后一个元素

```scss
.faq_item {
    &:not(:last-of-type) {
      margin-bottom: 40rpx;
  }
}
```

会选择class为faq_item的元素除最后一个元素的所有元素。