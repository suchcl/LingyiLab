<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [vue-router新窗口打开](#vue-router%E6%96%B0%E7%AA%97%E5%8F%A3%E6%89%93%E5%BC%80)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


### vue-router新窗口打开

在使用HTML标签a链接时，我们知道新页面打开只需要在a标签中添加target="_blank"属性就可以了，那么vue-router中怎么打开新页面呢？

<router-link>标记也是支持target="_blank"属性的，也是可以新页面打开，其他方式暂时没有尝试，接下来找个时间逐一验证。

我本地vue和vue-router版本：

```javascript
    "vue": "^3.0.11",
    "vue-router": "^4.0.10",
```