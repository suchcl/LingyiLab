<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Mac开启与关闭SIP](#mac%E5%BC%80%E5%90%AF%E4%B8%8E%E5%85%B3%E9%97%ADsip)
- [查看SIP的状态](#%E6%9F%A5%E7%9C%8Bsip%E7%9A%84%E7%8A%B6%E6%80%81)
- [开启SIP](#%E5%BC%80%E5%90%AFsip)
- [禁用SIP](#%E7%A6%81%E7%94%A8sip)
- [总结](#%E6%80%BB%E7%BB%93)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

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

### 开启SIP和禁用SIP

SIP的开启和禁用，不能在常规使用的系统中去设置的，需要在还原系统也叫恢复模式中去操作。

进入恢复模式方式：Intel：开机时同时长按Command+R；M芯片：开机时长按开机键，直到出现Apple标志。

进入到恢复模式之后，会显示一些系统级别的实用工具，具体是哪几个，没有截图，忘记了，不重要。然后在顶部的菜单中找到“终端”并进入。

明确下步骤：

开机时长按开机键(M系列芯片)或者同时Command+R -> 直到出现Apple标志-> 进入到系统的恢复模式 -> 找到终端并进入，进行相应操作即可

这个终端进入后，和日常使用中的终端命令行是一样的，也可以通过csrutil status查看SIP的状态。

```bash
csrutil disable # 禁用SIP
csrutil enable # 开启SIP
```

设置完成后，可以查询下状态，设置成功后重启即可

```bash
csrutil status
```

### 为什么需要修改SIP呢？

不同的人使用电脑的目的是不同的，有的人是追剧，有的人是日常办公，有了浏览器和office就足够了，也有很多专业技术人员在使用，如软件开发人员、视频处理人员、图像处理人员等。

专业技术人员在使用的时候，总会有一些特殊的要求，在OS默认的安全机制下是没有办法使用的，那么就需要通过一些特殊的配置、操作来改变一些系统的默认行为，来满足自己的需要。

### 总结

系统的完整性保护(SIP)是MacOS的一项重要安全保护技术，可以保护系统不受外来、非正常的、未经授权的访问和修改，从而保证系统的安全性和稳定性，在能够不修改该项配置的情况下尽量不去修改。