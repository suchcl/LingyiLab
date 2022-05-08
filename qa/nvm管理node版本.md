### clang: error: no such file or directory: ‘CXX=c++‘

环境：Mac M1

情形：在使用nvm安装node的v14.19.2版本时，突然报错了，错误信息报了很长，没有将错误信息给保存下来，但是核心内容就是：clang: error: no such file or directory: ‘CXX=c++‘。

一看有C++，还以为我把机器中的xcode卸载了，卸载xcode的同时把一些基本的功能构件也给卸载掉了呢。后来查到了一些资料，具体的过程就不再赘述了，把参考链接附上：https://blog.csdn.net/H1101370034/article/details/123137360，然后简单说下解决过程：

1. 在应用程序中找到终端

[找到终端](./images/i2.png)

2. 右键，将“使用Rosetta”打开勾选

[勾选'使用Rosetta打开'](./images/i3.png)

重新打开终端，再次使用nvm安装node就一切都正常了。

安装的速度还非常的快

[nvm安装node正常了](./images/i4.png)