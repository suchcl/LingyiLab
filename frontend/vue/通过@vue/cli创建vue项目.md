使用@vue/cli创建vue项目，需要先安装@vue/cli工具

理论上来说，安装@vue/cli工具，可以使用npm或者yarn，也可以使用pnpm等其他的包管理工具，但是我使用yarn全局安装@vue/cli的时候，创建项目提示找不到vue指令。于是我又通过npm全局安装了下，再次创建项目成功。

> 正常情况下，使用yarn应该是没有问题的，后来复盘了一下，原来是我在使用yarn安装依赖的时候，把global关键字的位置放错了

> 使用yarn的时候，关键字global需要紧跟着yarn，而不能放在依赖包名的后面，不像npm的-g参数那么灵活。



安装@vue/cli

```shell
yarn global add @vue/cli

npm install @vue/cli -g
```

创建vue项目

```shell
vue create projectName
```

通过@vue/cli创建项目的时候，可以选择vue的版本