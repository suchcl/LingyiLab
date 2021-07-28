# Egg秉承的理念：约定优于配置

### egg中mysql应用

一个完整的web项目少不了对数据的存储、分析，mysql是最常见的、应用较为广泛的关系型数据库，很多优秀的网站也都选择mysql作为自己的数据库。

框架提供了egg-mysql插件来访问mysql的能力。

```bash
npm install egg-mysql --save
```

#### egg中开启与配置mysql

1. 开启插件

```javascript
// config/plugin.js
mysql:{
    enable: true,
    package: "egg-mysql"
}
```

2. 在config/config.$(env).js中配置各个环境的数据库链接信息

```javascript
// 单个数据库源的配置方式
exports.mysql = {
    client: {
        host: "localhost",
        port: "3306",
        user: "root",
        password: "",
        database: "lingyilab"
    },
    // 是否将mysql实例添加到app实例上，默认开启
    app: true,
    // 是否将mysql实例添加到agent上，默认关闭
    agent: false
};

// 多个数据库源的时候的配置方式
module.exports = {
    clients: {
        db1: {
            host: "localhost",
            port: "3306",
            user: "root",
            password: "",
            database: "lingyilab"
        },
        db2: {
            host: "localhost",
            port: "3306",
            user: "root",
            password: "",
            database: "test"
        },
        // 这里还可以配置更多的数据库，方法类似，
    },
    // 所有的数据库配置都相同的部分，可以当做默认值配置
    default: {
        
    },
    // 是否将mysql实例添加到app上，默认开始
    app: true,
    // 是否将mysql实例添加到agent上，默认关闭
    agent: false
};
```