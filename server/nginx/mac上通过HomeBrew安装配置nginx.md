### mac上通过HomeBrew安装配置nginx

通过HomeBrew安装nginx

> 有的时候通过Homebrew安装应用的时候速度有点慢，或者压根就下载不下来，可以参考：[Homebrew安装的常见问题](../../devTools/Homebrew.md)

```bash
xxx@xxxxx xxxx % brew install nginx
==> Downloading https://mirrors.aliyun.com/homebrew/homebrew-bottles/pcre-8.45.arm64_monterey.bottle.tar.gz
######################################################################## 100.0%
==> Downloading https://mirrors.aliyun.com/homebrew/homebrew-bottles/nginx-1.21.5.arm64_monterey.bottle.tar.gz
######################################################################## 100.0%
==> Installing dependencies for nginx: pcre
==> Installing nginx dependency: pcre
==> Pouring pcre-8.45.arm64_monterey.bottle.tar.gz
🍺  /opt/homebrew/Cellar/pcre/8.45: 204 files, 4.6MB
==> Installing nginx
==> Pouring nginx-1.21.5.arm64_monterey.bottle.tar.gz
==> Caveats
Docroot is: /opt/homebrew/var/www

The default port has been set in /opt/homebrew/etc/nginx/nginx.conf to 8080 so that
nginx can run without sudo.

nginx will load all files in /opt/homebrew/etc/nginx/servers/.

To restart nginx after an upgrade:
  brew services restart nginx
Or, if you don't want/need a background service you can just run:
  /opt/homebrew/opt/nginx/bin/nginx -g daemon off;
==> Summary
🍺  /opt/homebrew/Cellar/nginx/1.21.5: 26 files, 2.2MB
==> Running `brew cleanup nginx`...
Disable this behaviour by setting HOMEBREW_NO_INSTALL_CLEANUP.
Hide these hints with HOMEBREW_NO_ENV_HINTS (see `man brew`).
==> Caveats
==> nginx
Docroot is: /opt/homebrew/var/www

The default port has been set in /opt/homebrew/etc/nginx/nginx.conf to 8080 so that
nginx can run without sudo.

nginx will load all files in /opt/homebrew/etc/nginx/servers/.

To restart nginx after an upgrade:
  brew services restart nginx
Or, if you don't want/need a background service you can just run:
  /opt/homebrew/opt/nginx/bin/nginx -g daemon off;
```

**通过brew info nginx查看nginx信息**

```bash
xxx@xxxx % brew info nginx
nginx: stable 1.21.5 (bottled), HEAD
HTTP(S) server and reverse proxy, and IMAP/POP3 proxy server
https://nginx.org/
/opt/homebrew/Cellar/nginx/1.21.5 (26 files, 2.2MB) *
  Poured from bottle on 2022-01-22 at 13:25:35
From: https://mirrors.aliyun.com/homebrew/homebrew-core.git/Formula/nginx.rb
License: BSD-2-Clause
==> Dependencies
Required: openssl@1.1 ✔, pcre ✔
==> Options
--HEAD
	Install HEAD version
==> Caveats
Docroot is: /opt/homebrew/var/www

The default port has been set in /opt/homebrew/etc/nginx/nginx.conf to 8080 so that
nginx can run without sudo.

nginx will load all files in /opt/homebrew/etc/nginx/servers/.

To restart nginx after an upgrade:
  brew services restart nginx
Or, if you don't want/need a background service you can just run:
  /opt/homebrew/opt/nginx/bin/nginx -g daemon off;
==> Analytics
install: 32,844 (30 days), 115,076 (90 days), 491,848 (365 days)
install-on-request: 32,779 (30 days), 114,867 (90 days), 490,762 (365 days)
build-error: 7 (30 days)
```

里面的信息，给出了nginx的安装目录、安装来源、根目录等信息。

### 服务的管理

**服务启动**

```bash
brew services start nginx
```

**服务重启**

```bash
brew services restart nginx
```

**服务停止**

```bash
brew services stop nginx
```

### nginx的常用目录

```bash
/opt/homebrew/Cellar/nginx/1.21.5  # 安装目录
/opt/homebrew/var/www  # 根目录
/opt/homebrew/etc/nginx/servers/  # 配置文件目录
```