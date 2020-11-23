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

希望了解更多 Docker 的信息和有关使用和实现的问题和回答，请参考 [overview page in "get started"](../get-started/overview.md) 页面中的内容。

## 安装指南

请参考 [installation section](install/index.md) 页面中的内容来针对不同平台的 Docker 安装指南。

## 发行日志

针对当前的版本的修改和历史版本的修改日志，请参考  [Release Notes page](release-notes/index.md) 页面中的内容。

## 特性丢弃策略

Docker 容器随着版本的改变和新特性的添加可能随着性能的变化和添加而过期而被替代掉。在已经存在的特性被删除之前，这个特性将会在文档中标记为 "deprecated"。
这个标记将会在 Docker 中至少保持 3 个稳定的版本，除非被明确的表示将会被删除掉。

针对需要删除的特性列表，用户将会被建议先记录下来，并且针对一些被删除的特性，用户在进行版本合并的时候尽量先合并这些新的特性，并尽可能的先替换掉。

完整的需要删除的特性列表，请参考页面：[Deprecated Features page](deprecated.md) 中的内容。

## 许可证

Docker 是基于 Apache License, Version 2.0. 许可证进行发布的，请参考 [许可证](https://github.com/moby/moby/blob/master/LICENSE) 来获得更多的信息。
