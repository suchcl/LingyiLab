###  WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!

最近发现在向github.com提交或者拉取代码的时候，总是莫名其妙的报错。

```bash
[xxxx tt]$ git clone git@github.com:xxxx/xxxx.git
Cloning into 'ttt'...
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ED25519 key sent by the remote host is
SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
Please contact your system administrator.
Add correct host key in /Users/xxxxx/.ssh/known_hosts to get rid of this message.
Offending ED25519 key in /Users/xxxxx/.ssh/known_hosts:2
Host key for github.com has changed and you have requested strict checking.
Host key verification failed.
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

大概的意思就是说可能是github服务器上的公钥发生了变化，导致客户端在和github服务器连接的时候，验证失败，就提示了没有权限，没有办法从github服务器上拉取和推送代码。

遇到这个问题，提示信息已经给了我们解决方案：

```bash
Add correct host key in /Users/xxxxx/.ssh/known_hosts to get rid of this message.
```

把正确的key添加到/Users/xxxxx/.ssh/目录下的known_hosts文件。

解决问题的关键信息是已经明确了，但是也省略了一点，就是key对应的服务器也要添加上，所以需要添加的完整信息是：

```bash
github.com SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU
```

当把最新的key添加到了/Users/xxxxx/.ssh/known_hosts文件后，再进行pull、push或clone操作的时候，会提示没有建立对github.com服务器的真实性、可靠性还没有建立，是否要继续和github.com服务器建立连接？这是需要手动的键入yes，随后问题解决。

```bash
[xxxxx tt]$ git clone git@github.com:xxx/ttt.git
Cloning into 'ttt'...
The authenticity of host 'github.com (20.205.243.166)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])
```

