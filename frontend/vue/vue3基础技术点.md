<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. 组件导入](#1-%E7%BB%84%E4%BB%B6%E5%AF%BC%E5%85%A5)
  - [1.1 直接导入组件](#11-%E7%9B%B4%E6%8E%A5%E5%AF%BC%E5%85%A5%E7%BB%84%E4%BB%B6)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 1. 简介

#### 1.1 发布

2020.9.18 Vue3.0发布

RFC：请求修改意见稿

https://github.com/vuejs/rfcs/tree/master/active-rfcs  rfcs 

Vue3  https://github.com/vuejs/vue-next/

#### 1.2 Vue3带来了什么

打包大小减小了41%

初次渲染快了55%，更新渲染快133%

内存使用减少了54%

……

#### 1.3 源码的升级

使用Proxy代替Object.defineProperty实现响应式

重写虚拟DOM和Tree-Shaking

……

> Tree-Shaking,是一个术语，不是什么库。webpack本身支持treeshaking

#### 1.4 友好的兼容Typescript

Vue3可以更加友好的支持Typescript

#### 1.5 新特性

##### 1.5.1 Composition API(组合式API)

setup配置

ref与reactive

watch与watchEffect

provide与inject

##### 1.5.2 新的内置组件

Fragment

Teleport

Suspense

##### 1.5.3 其他改变

新的生命周期钩子

data选项应始终被声明为一个函数

移除keyCode支持v-on修饰符

### 2.创建Vue3项目

两种方式创建Vue3项目

#### 2.1 使用@vue/cli创建vue3项目

使用@vue/cli创建vue3项目，要求@vue/cli的版本是4.5.0以上版本

查看@vue/cli版本

```bash
PS D:\> vue -V
@vue/cli 4.5.14
PS D:\> vue --version
@vue/cli 4.5.14
```

两种方式都可以查看@vue/cli版本。从结果上来看，我的机器是满足要求的。

通过@vue/cli创建vue项目，就是使用webpack构建项目。

创建项目

```bash
vue create vue3projectname
```

通过@vue/cli创建好项目，可以直接进入项目启动服务运行，不需要单独安装npm包，因为在创建项目的时候，就已经把npm包都已经安装好了。

#### 2.2 使用vite创建vue3项目

```bash
# 使用npm创建项目
npm init vite

# 使用yarn创建项目
yarn create vite

# 使用pnpm创建项目
pnpm create vite
```



