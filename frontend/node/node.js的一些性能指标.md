<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [服务端开发关注的性能指标](#%E6%9C%8D%E5%8A%A1%E7%AB%AF%E5%BC%80%E5%8F%91%E5%85%B3%E6%B3%A8%E7%9A%84%E6%80%A7%E8%83%BD%E6%8C%87%E6%A0%87)
  - [1. CPU使用率](#1-cpu%E4%BD%BF%E7%94%A8%E7%8E%87)
  - [2. CPU负载](#2-cpu%E8%B4%9F%E8%BD%BD)
  - [3. 内存指标](#3-%E5%86%85%E5%AD%98%E6%8C%87%E6%A0%87)
  - [4. 磁盘空间指标](#4-%E7%A3%81%E7%9B%98%E7%A9%BA%E9%97%B4%E6%8C%87%E6%A0%87)
  - [5. I/O指标](#5-io%E6%8C%87%E6%A0%87)
- [总结](#%E6%80%BB%E7%BB%93)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 服务端开发关注的性能指标

Node.js属于一门服务端开发语言(这里不要纠结很细致的精准的定义，node.js也可以说是js的一个运行时环境，我们这篇文章不说这些，主要介绍基于node.js的服务端开发)，那么服务端开发需要关注哪些性能指标呢？

- CPU使用率

- CPU负载(load)

- 内存

- 硬盘

- I/O

- 吞吐量(Throughput)

- 每秒查询率QPS(Query Per Second)

- 日志监控/真实 QPS

- 响应时间

- 进程监控

### 1. CPU使用率

CPU使用率是一个衡量计算机中央处理单元(CPU)在给定时间内有多忙碌的指标。它表示在CPU能适用的时间里，CPU实际上被使用的时间百分比。简单来说，CPU使用率反映了计算机的处理能力被消耗的程度。

1. 100%CPU使用率意味着CPU在该时刻完全处于工作状态，没有闲置

2. 0%CPU使用率意味着CPU完全闲置，没有任何任务在运行

CPU使用率通常是通过以下几种方式计算的：

1. 用户Time(User Time):CPU执行用户级程序的时间

2. 系统Time(System Time):CPU执行内核操作的时间

3. 空闲Time(Idle Time):CPU没有执行任何任务的时间

4. 中断时间(IRQ Time):处理硬件中断的时间

CPU使用率的计算公式 = (总时间 - 空闲时间)/总时间 * 100%

其中，总时间是从上次采样以来的CPU总时间，空闲时间是从上次采样时间以来的CPU空闲时间。

Node.js提供了OS模块来获取操作系统的相关信息，包括CPU使用情况。虽然OS模块本身没有直接提供获取CPU使用率的API，但是我们可以通过os.cpus()获取每个CPU核心的详细信息，并通过计算差值来获取CPU使用率。

- model：CPU型号

### 2. CPU负载

### 3. 内存指标

### 4. 磁盘空间指标

### 5. I/O指标

## 总结