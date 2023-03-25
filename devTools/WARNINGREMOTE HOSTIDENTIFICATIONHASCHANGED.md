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

> 刚开始遇到这个问题的时候，我没有认真看提示信息，就直接去网上查解决方案了，尝试了网上给出的很多解决方案，但是没有一个方案解决我的问题的，有的是可以操作一次，只有一次的操作时正常的，之后问题就再次出来，有的压根是一次都不生效。由于我本地连接了多个个git服务器，还一直担心如果修改了git的全局配置，会影响到其他git服务器的连接和使用，每次修改git本地配置的是好，都要先记住之前的配置，如果不生肖，再还原回来原来的配置，再把其他的git服务器的连接重新验证一遍，看是否影响到了其他的git服务器的使用，真的是费时费力，还没有解决问题。

> 今天是周末，没有其他的开发任务，孩子也睡觉了，就想着一定要解决这个问题。于是就认真的看了下报错信息，然后发现了关键信息：Add correct host key in /Users/a58/.ssh/known_hosts to get rid of this message.这不就是解决方法吗？提示信息都给了解决方案了，而且是针对该问题给出的方案，这应该是最有价值的信息了，于是就按照提示信息，将信息中给出的key添加到了known_hosts文件中，然后正常的进行git的pull操作，根据提示键入yes，继续连接git服务器，问题解决。根据异常信息提示的方式解决问题，用时5分钟，精准高效。

> 所以，对于一个从事技术岗位的工作人员，不应该抵触、害怕报错信息，而是应该认真、静心的去看报错信息，也许，问题的解决方案，报错信息中就给出了解决方案。
