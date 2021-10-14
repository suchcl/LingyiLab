### vue.config.js常用配置

从@vue/cli3.x版本开始，cli工具已经给出了很多默认的配置和工具，都已经给我们配置好了，可以在0配置的基础上实现基本的常用功能，如less预处理起到转换等，但还是有一些场景cli对于webpack的预配置不能满足我们的需求，针对我的常用需求，我梳理一个文件，给出一个完整的配置文件。

> vue.config.js在项目的根目录下，如果新增的配置项和预设的配置项相同了，就会覆盖掉预设置的配置项。

```javascript
module.exports = {
  // 编译的js不生成map文件
  productionSourceMap: false,
};
```