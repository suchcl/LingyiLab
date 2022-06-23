### node、mysql，一次query操作执行多条sql语句

在一些业务开发中，有的时候为了一条数据，需要执行多条sql语句，才能得到语气的数据。我尝试了下query时执行多条sql语句，结果报错了。但是当我把sql复制到mysql命令行终端的时候，直接结果正常。

原来node和mysql配合使用的时候，默认是不支持在node中执行多条sql语句的，如果在实际业务场景中需要一次执行多条sql语句，那么需要在创建链接池的时候加一个配置项：multipleStatements。该项默认为false，不支持执行多条sql语句。我们可以看下源码中的注解：

```js
/**
 * Allow multiple mysql statements per query. Be careful with this, it exposes you to SQL injection attacks. (Default: false)
 */
multipleStatements?: boolean | undefined;
```

这个配置项的值是false，配置为true后可以实现同时执行多条sql语句。但是使用时应该谨慎，不要轻易使用，因为使用了后，可能面临着sql注入的风险。

```js
var pool = mysql.createPool({
    multipleStatements: true, // 允许每个query操作的时候执行多条sql语句
    host: "xxxxxx",
    port: xxxxxx,
    user: "xxxxxx",
    password: "xxxxxx",
    database: "xxxxxx",
    timezone: "08:00"
});
```