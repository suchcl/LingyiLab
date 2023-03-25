### umi项目中antd更改主题色

大多数的react项目都会使用antd这个UI库，antd这个UI库默认是蓝色的色调，有的时候我们的项目、产品可能不是这个色调，虽然颜色不会影响功能的使用，但是让产品的项目主题色调和公司主色调保持一致，能提升产品的规格和使用体感。

antd更换主题色，其实antd的文档中有说明，大概有3种方式，可以参考链接：https://4x.ant.design/docs/react/customize-theme-cn#%E5%AE%9A%E5%88%B6%E6%96%B9%E5%BC%8F

1. 在webpack中配置

因为antd在5版本(不包括antd5)之前是通过less来做样式控制的，所以可以在webpack中通过less-loader做一些相应的配置

由于在umi项目中，webpack的一些配置都被封装好了，所以不建议使用这种方式

2. 在umi项目的配置文件.umirc.ts或者config/config.ts中做配置

这种方式简单、不需要引入新的文件，只需要在theme这个配置项中配置一些元素的色调就可以了，简单、高效。只是配置好以后需要重启下服务，如果不生效就删除掉src/.umi目录，重新启动服务就可以了.

一些常用的配置项可参考如下：

```less
@primary-color: #1890ff; // 全局主色
@link-color: #1890ff; // 链接色
@success-color: #52c41a; // 成功色
@warning-color: #faad14; // 警告色
@error-color: #f5222d; // 错误色
@font-size-base: 14px; // 主字号
@heading-color: rgba(0, 0, 0, 0.85); // 标题色
@text-color: rgba(0, 0, 0, 0.65); // 主文本色
@text-color-secondary: rgba(0, 0, 0, 0.45); // 次文本色
@disabled-color: rgba(0, 0, 0, 0.25); // 失效色
@border-radius-base: 2px; // 组件/浮层圆角
@border-color-base: #d9d9d9; // 边框色
@box-shadow-base: 0 3px 6px -4px rgba(0, 0, 0, 0.12), 0 6px 16px 0 rgba(0, 0, 0, 0.08),
  0 9px 28px 8px rgba(0, 0, 0, 0.05); // 浮层阴影
```
全部可配置变量，可参考这里：https://github.com/ant-design/ant-design/blob/4.x-stable/components/style/themes/default.less

3. 在create-react-app中定制

umi项目，不使用cra这个脚手架工具，如果想学习下配置方式呢，可以参考https://4x.ant.design/docs/react/use-with-create-react-app-cn页中的自定义主题模块。