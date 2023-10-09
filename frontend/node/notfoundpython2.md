### gyp verb `which` failed Error: not found: python2

在通过yarn安装node-sass的时候，报出了异常信息，其中有一条信息尤其值得关注：gyp verb `which` failed Error: not found: python2

还有一些关键信息，如下：

```bash
gyp verb check python checking for Python executable "python2" in the PATH
gyp verb `which` failed Error: not found: python2
gyp verb `which` failed     at getNotFoundError (/……/node_modules/which/which.js:13:12)
gyp verb `which` failed     at F (/……/node_modules/which/which.js:68:19)
gyp verb `which` failed     at E (/……/node_modules/which/which.js:80:29)
gyp verb `which` failed     at /……/node_modules/which/which.js:89:16
gyp verb `which` failed     at /……/node_modules/isexe/index.js:42:5
gyp verb `which` failed     at /……/node_modules/isexe/mode.js:8:5
gyp verb `which` failed     at FSReqCallback.oncomplete (fs.js:183:21)
gyp verb `which` failed  python2 Error: not found: python2
gyp verb `which` failed     at getNotFoundError (/……/node_modules/which/which.js:13:12)
gyp verb `which` failed     at F (/……/node_modules/which/which.js:68:19)
gyp verb `which` failed     at E (/……/node_modules/which/which.js:80:29)
gyp verb `which` failed     at /……/node_modules/which/which.js:89:16
gyp verb `which` failed     at /……/node_modules/isexe/index.js:42:5
gyp verb `which` failed     at /……/node_modules/isexe/mode.js:8:5
gyp verb `which` failed     at FSReqCallback.oncomplete (fs.js:183:21) {
gyp verb `which` failed   code: 'ENOENT'
gyp verb `which` failed }
gyp verb check python checking for Python executable "python" in the PATH
gyp verb `which` failed Error: not found: python
gyp verb `which` failed     at getNotFoundError (/……/node_modules/which/which.js:13:12)
gyp verb `which` failed     at F (/……/node_modules/which/which.js:68:19)
gyp verb `which` failed     at E (/……/node_modules/which/which.js:80:29)
gyp verb `which` failed     at /……/node_modules/which/which.js:89:16
gyp verb `which` failed     at /……/node_modules/isexe/index.js:42:5
gyp verb `which` failed     at /……/node_modules/isexe/mode.js:8:5
gyp verb `which` failed     at FSReqCallback.oncomplete (fs.js:183:21)
gyp verb `which` failed  python Error: not found: python
// ……
gyp ERR! stack Error: Can't find Python executable "python", you can set the PYTHON env variable.
// ……
```

信息的主要意思就是说找不到python2，没有发现python，以及需要配置下python的环境变量，那么就按照这个提示去安装python或者配置python的环境变量就可以了。

### 解决方案

1. 安装node-gyp

```bash
npm install node-gyp -g
```

