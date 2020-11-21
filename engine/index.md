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

* A server with a long-running daemon process [`dockerd`](/engine/reference/commandline/dockerd).
* APIs which specify interfaces that programs can use to talk to and
  instruct the Docker daemon.
* A command line interface (CLI) client [`docker`](/engine/reference/commandline/cli/).

The CLI uses [Docker APIs](api/index.md) to control or interact with the Docker
daemon through scripting or direct CLI commands. Many other Docker applications
use the underlying API and CLI. The daemon creates and manage Docker objects,
such as images, containers, networks, and volumes.

For more details, see [Docker Architecture](../get-started/overview.md#docker-architecture).

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
