### 不包含某个class的css选择器

在写css样式的时候，经常会需要排除某个class的一些元素设置特定样式

```css
.box div:not(.title) {
  width: 100px;
  height: 100px;
}
```
意思是查找class为box的容器中但是class属性没有title的div元素

### 索引为某个数倍数的元素

```css
.list > li:nth-child(3n){
  color: #f20;
}
```

查找list中li元素的索引为3的倍数的元素