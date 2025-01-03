<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [1. 构建工具webpack和vite的对比](#1-%E6%9E%84%E5%BB%BA%E5%B7%A5%E5%85%B7webpack%E5%92%8Cvite%E7%9A%84%E5%AF%B9%E6%AF%94)
  - [1.1 构建方式](#11-%E6%9E%84%E5%BB%BA%E6%96%B9%E5%BC%8F)
  - [1.2 启动速度](#12-%E5%90%AF%E5%8A%A8%E9%80%9F%E5%BA%A6)
  - [1.3 热模块替换(HMR)](#13-%E7%83%AD%E6%A8%A1%E5%9D%97%E6%9B%BF%E6%8D%A2hmr)
  - [1.4 配置复杂度](#14-%E9%85%8D%E7%BD%AE%E5%A4%8D%E6%9D%82%E5%BA%A6)
  - [1.5 插件生态](#15-%E6%8F%92%E4%BB%B6%E7%94%9F%E6%80%81)
  - [1.6 性能](#16-%E6%80%A7%E8%83%BD)
  - [1.7 支持的框架(兼容性)](#17-%E6%94%AF%E6%8C%81%E7%9A%84%E6%A1%86%E6%9E%B6%E5%85%BC%E5%AE%B9%E6%80%A7)
- [拷问：既然现在vite的优势那么多，也那么明显，那么vite会取代webpack吗？](#%E6%8B%B7%E9%97%AE%E6%97%A2%E7%84%B6%E7%8E%B0%E5%9C%A8vite%E7%9A%84%E4%BC%98%E5%8A%BF%E9%82%A3%E4%B9%88%E5%A4%9A%E4%B9%9F%E9%82%A3%E4%B9%88%E6%98%8E%E6%98%BE%E9%82%A3%E4%B9%88vite%E4%BC%9A%E5%8F%96%E4%BB%A3webpack%E5%90%97)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 1. 构建工具webpack和vite的对比

### 1.1 构建方式

- webpack:采用打包的方式，首先将所有的模块和资源进行静态分析，生成一个或多个包含所有依赖的打包后的文件。这个过程在开发阶段可能会感觉比较慢，因为代码每次修改后都需要重新打包。

- vite:使用原生的ES模块(ESM)，支持热模块替换(HMR)，在开发阶段不需要打包，而是通过服务器直接提供模块文件，速度更快。只有在生产环境中，vite才会打包代码(使用rollup进行打包)。因此在开发阶段，vite使用的是ESM，所以代码中不能够使用CommonJS。

### 1.2 启动速度

- webpack:首次构建较慢，尤其是在项目较大或者依赖较多的时候。增量构建时则会好一点，但整体来说，构建速度上，webpack不占据优势。

- vite:由于Vite使用的是ESM，不需要编译，不需要进行模块之间的依赖分析，所以启动速度较快，通常能够在几秒之内就够启动开发服务器。项目越负责、依赖越多，vite的优势就越明显。

### 1.3 热模块替换(HMR)



### 1.4 配置复杂度

### 1.5 插件生态

### 1.6 性能

### 1.7 支持的框架(兼容性)


## 拷问：既然现在vite的优势那么多，也那么明显，那么vite会取代webpack吗？

