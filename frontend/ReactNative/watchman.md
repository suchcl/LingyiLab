### Watchman

Watchman是一个由Facebook开源的文件监视器，用于监视文件系统中文件的变化，并触发相应的操作。它可以监视文件的创建、修改、删除等操作，并支持文件过滤、规则匹配等功能，可以被用于各种自动化工具、构建工具和开发工具中，如webpack、babel、jest等。

watchman使用了一些高效的算法和数据结构，比如哈希表、位图索引等，可以快速地检测文件变化，并支持大规模的文件系统监视。watchman还提供了一个命令行工具，可以用于查看监视列表、设置监视规则、调试监视器等操作。

在前端开发中，watchman通常被用于监视文件变化并触发自动化构建、自动化测试等操作。例如在ReactNative中，watchman可以用来监视javascript代码的变化，并触发应用程序重新加载；在webpack构建中，watchman可用于监视源代码的变化，并触发自动化构建和大包操作。

总之，watchman是一个功能强大的文件监视器，可以帮助开发者快速的监测文件的变化，并触发相应的操作，从而提高开发效率和代码质量。

### watchman的安装

以mac平台为例。

在mac上可以通过Homebrew快速安装

```bash
brew install watchman
```

该命令会自动下载、编译和安装Watchman及其依赖库。

**安装结果的提示**

在安装完成watchman后可以通过检车版本号的方式来确认是否已经安装成功。

```bash
watchman --version
```
如果正常的输出了版本号，则说明已经安装成功，否则就是安装失败。

### watchman的常用指令

1. watchman watch <path>：添加一个监视器，监视指定的目录或文件。

如要监视当前目录下所有文件的变化，可以通过如下指令:

```bash
watchman watch .
```

2. watchman watch-list:用于查看当前所有监视器的列表和状态信息.

如要查看当前所有监视器的状态，可以使用下面的指令：

```bash
watchman watch-list
```

3. watchman trigger <path> <name> <rules> <command>:用于设置一个触发器，当监视器中的文件符合指定的规则时，会执行指定的命令。

例如要在当前目录下的所有js文件发生变动时，执行npm run build命令，可以执行下面的指令：

```bash
watchman trigger . js-build '*.js' -- npm run build
```

4. watchman query <path> <expression>:用于查询监视器中符合指定表达式的文件列表。

例如要查询当前目录下所有的.js文件，可以使用下面的指令:

```bash
watchman query . --expression=["match",".js"]
```

5. watchman version:用于查看watchman的版本信息

```bash
watchman version
```

watchman version，和watchman --version，都可以用来查看watchman的版本信息

6. watchman log：用于查看watchman的日志信息

如要查看最近的100条信息：

```bash
watchman log -n 100
```