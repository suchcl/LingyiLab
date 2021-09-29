###　Uncaught (in promise) Error: Maximum recursive updates exceeded. This means you have a reactive effect that is mutating its own dependencies and thus recursively triggering itself. Possible sources include component template, render function, updated hook or watcher source function.

今天在修改一个项目时，突然发现select不能点了，以前是不是好的，没有注意，反正是现在不能点了。

查了一下，这是vue的bug，升级下vue就可以了。

我原来的vue版本是3.0.0，升级了下，升级到了3.2.19，问题解决了。