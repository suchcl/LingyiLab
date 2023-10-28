### mac下命令行查找软件的安装目录



#### 查找java的安装目录

```bash
/usr/libexec/java_home # 可用来查找当前系统下所有版本的java的安装目录
/usr/libexec/java_home -V # 可用来获取当前系统下所有已经安装的java的版本以及对应的安装目录
```

在mac下，java的默认安装目录为/Library/Java/JavaVirtualMachines。

**通过环境变量查找java的安装目录**

如果已经配置了环境变量，则可以通过环境变量的方式来查找

```bash
echo $JAVA_HOME
```

如果配置了环境变量JAVA_HOME，则可以通过这种方式去查找，如果没有配置就不行了。