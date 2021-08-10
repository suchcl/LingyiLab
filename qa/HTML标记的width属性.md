### HTML标记的width属性

今天在测试canvas这个标记的时候，给canvas设置了width属性，发现实际的显示效果和我设置的尺寸不一致（问题已经发现并解决了,可参考[网页截图和实际设置尺寸不一致的问题](./网页截图和实际css设置尺寸不符.md)），突然想到了HTMl5标准中，很多样式控制属性都已经不再支持了，能通过css控制的样式、效果问题，对应的HTML属性就不再建议使用了。

记得之前是类似属性是不建议使用，如width、height等，但是使用了也还是生效的，但是今天写canvas案例的时候，由于实际的显示效果和我设置的效果不同，也替换了div来验证了一下。得到了一个意向不到的结果：canvas是和实际设置效果不同，而div设置的width和height属性则直接不生效，难道新标准有新的变化？因为很少直接这么使用了，之前也就没有关注过这些细节的变动。于是就查了下文档。

确实有了新的变动，HTML属性中的部分不建议使用的属性，在新的标准中已经废除了，不再支持了。比如width属性，现在只支持几个标签：canvas、embed、iframe、img、input(只有在type为image的时候)、object、video，其他的标签已经不再支持了，也正因此，才出现了我前面的div设置width、height属性无效的现象。对很多HTML标记移除这些可通过css设置的样式，但是canvas必须要设置width属性，当然了，也可以通过css来设置，效果等同。

可参考[HTML属性](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Attributes)