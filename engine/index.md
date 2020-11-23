---
description: Engine
keywords: Engine
redirect_from:
- /edge/
- /engine/ce-ee-node-activate/
- /engine/misc/
- /linux/
- /manuals/ # TODO remove this redirect after we've created a landing page for the product manuals section
title: Docker 引擎概述
---

Docker Engine 是一个开源的容器技术，被用来对你的应用进行容器化构建。

Docker Engine 实际上是一个客户端服务器（client-server）应用：

* 一个在服务器上长期运行的被称为 [`dockerd`](/engine/reference/commandline/dockerd) 的进程。
* 一个指定结构的 APIs，这个 API 被用来与 Docker 守护进程进行通信。
* 一个命令行界面（CLI）客户端 [`docker`](/engine/reference/commandline/cli/)。

命令行界面（CLI）使用 [Docker APIs](api/index.md) 来控制和与 Docker 来互相作用。这个使用脚本或者 CLI 命令行来进行控制和执行。
其他 Docker 应用使用下层 API 和 CLI 来对 Docker 来进行控制。Docker 守护进程创建和管理 Docker 的对象（objects），
例如 镜像（images），容器（containers），网络（networks），卷（volumes）。

更多的信息和内容，请参考： [Docker Architecture](../get-started/overview.md#docker-architecture)。

## Docker 用户指南

To learn about Docker in more detail and to answer questions about usage and
implementation, check out the [overview page in "get started"](../get-started/overview.md).

## 安装指南

The [installation section](install/index.md) shows you how to install Docker
on a variety of platforms.

## 发行日志

A summary of the changes in each release in the current series can now be found
on the separate [Release Notes page](release-notes/index.md)

## 特性丢弃策略

As changes are made to Docker there may be times when existing features
need to be removed or replaced with newer features. Before an existing
feature is removed it is labeled as "deprecated" within the documentation
and remains in Docker for at least 3 stable releases unless specified
explicitly otherwise. After that time it may be removed.

Users are expected to take note of the list of deprecated features each
release and plan their migration away from those features, and (if applicable)
towards the replacement features as soon as possible.

The complete list of deprecated features can be found on the
[Deprecated Features page](deprecated.md).

## 许可证

Docker 是基于 Apache License, Version 2.0. 许可证进行发布的，请参考 [许可证](https://github.com/moby/moby/blob/master/LICENSE) 来获得更多的信息。
