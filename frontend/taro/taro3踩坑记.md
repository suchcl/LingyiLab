### 环境变量

之前版本: Taro.ENV_TYPE

Taro3中: process.env.TARO_ENV

[参考文档:https://taro-docs.jd.com/docs/envs#processenvtaro_env](https://taro-docs.jd.com/docs/envs#processenvtaro_env)

### 生命周期

componentWillMount(){}

该钩子函数只有在子组件中生效,页面组件中该钩子函数不生效.也就是说,页面组件没有componentWillMount这个周期,只有页面中的子组件才有.

另外,避免在该周期的这个钩子函数中引入任何的副作用或订阅,对于副作用或者订阅等操作,建议在constructor中去处理.