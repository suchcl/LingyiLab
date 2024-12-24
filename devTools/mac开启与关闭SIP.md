### Mac开启与关闭SIP

参考链接：[https://blog.csdn.net/qq_42698421/article/details/138538340](https://blog.csdn.net/qq_42698421/article/details/138538340)

SIP(System Integrity Protection,系统的完整性保护)，是MacOS10.11引入的一项安全技术。其主要目的

1. 保护系统级的文件和目录不受侵害。如/system、/bin、/sbin/、/usr等，也会保护从/etc、/var、/tmp到/private/etc、/private/tmp、/private/var的符号链接，以及绝大多数在Application目录中的系统的预安装应用。

2. 保护进程安全：防止进程被代码注入、运行时附属(如调试)和DTrace攻击，确保系统进程的稳定性和安全性，避免恶意软件通过注入代码等方式篡改进程的正常执行。

3. 限制内核扩展：自MacOS Yosemite起，内核扩展(如驱动)需要被苹果授权和签名。系统的完整性保护会阻止未签名的内核扩展加载。如果存在未签名的扩展，内核则拒绝开机，并在屏幕上显示禁行标志。


### 查看SIP的状态

SIP的状态有且仅有2个，开启和禁用状态。

可以在命令行查看SIP状态

```bash
csrutil status # 查看sip状态
```

如果出现了类似System Integrity Protection status: disabled的标志性提示，则表示是SIP是禁用状态。如：

```bash
csrutil status
System Integrity Protection status: disabled
```

### 总结

系统的完整性保护(SIP)是MacOS的一项重要安全保护技术，可以保护系统不受外来、非正常的、未经授权的访问和修改，从而保证系统的安全性和稳定性，在能够不修改该项配置的情况下尽量不去修改。