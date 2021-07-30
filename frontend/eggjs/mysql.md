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

### 编写CRUD语句

#### 插入数据


#### 读取数据

在只读取一条数据的时候，可以使用get方法，在获取多条数据的时候，需要使用select方法，不能使用get方法。

```javascript
// 读取单条数据
const user = await this.app.mysql.get("user", {  // 读取user表中username、password两个字段，条件为username=传递进来的参数uname
    where: { username: uname },
    columns: ["username", "password"]
});


// 读取多条数据，需要使用select方法，不能使用get方法
const results = await this.app.mysql.select('user', { // 搜索 post 表
    where: { username: uname }, // WHERE 条件
    columns: ['username', 'password'], // 要查询的表字段
});
```