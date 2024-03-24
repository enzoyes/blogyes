---
title: namespace原理剖析
date: 2024-03-24 19:38:00
categories: 
- 容器runtime
tags:
- namespace
---

## namespace是什么？

说到容器技术，尤其是以lxc和runc等为runtime的操作系统层云原生隔离环境，难以跨过的几大内核特性包括namespace和cgroup。那么namespace何时出现的，又有什么用呢？

首先，namespace是用来给进程做资源隔离的，很多编程语言如C++也有自己的namespace，包括k8s也有namespace一说，本质上都是为了资源的域间互相不可见。在linux上，通过 namespace 可以让进程A只能看到A相关的一部分资源，而进程B也只能看到与B相关的资源，这两个进程互相感觉不到对方的存在。具体的实现方式是把一个或多个进程的相关资源指定在同一个 namespace 中。

如下表所示，包括ipc、network、pod、uts等资源，大部份在很早的内核版本都已经支持了。

| 名称    | 隔离的资源                      | 支持的内核版本 |
| ------- | ------------------------------- | -------------- |
| IPC     | 共享内存、消息队列、信号量等IPC | 2.6            |
| Network | 网络设备、网络栈、端口          | 2.6            |
| Mount   | 文件挂载点                      | 2.4            |
| PID     | 进程编号                        | 2.6            |
| User    | 用户和用户组                    | 3.8            |
| UTS     | 主机名或者NIS域名               | 2.6            |
| Cgroup  | cgroup的根目录                  | 4.6            |



## namespace的使用？

namespace是针对于进程而言的，包括设置/修改进程的namespace。

### 命令行

lsns: 查看当前系统中的namespace

unshare:让进程进入一个新的namespace。

nsenter: 进入某个namespace下运行某个进程





### Go函数



## namespace的内核实现

namespace是针对于进程而存在的，那么在代表进程的task_struct里必然需要有相关的记录。



## 目前的局限性
