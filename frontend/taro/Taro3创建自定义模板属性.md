dataset是小程序的模板属性,Taro2中也支持在组件中支持使用dataset自定义属性,但是在Taro3中,个别场景就不能像Taro2或者原生小程序那样直接在组件中使用了.

dataset是一个特殊的模板属性,主要作用是可以在事件回调的event对象中获取到dataset相关的一些数据.这个基础的能力,Taro本身是支持的,也是可以通过一定的方法获取到dataset对象值,但是在页面节点中是不能直接看到的,该属性没有直接挂在到页面节点中.


### Taro1、Taro2可以直接在模板中使用dataset自定义属性

### Taro3中不能直接在组件中使用dataset自定义属性

### 让Taro3支持dataset模板属性

dataset是特殊的模板属性,