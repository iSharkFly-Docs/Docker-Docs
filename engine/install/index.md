---
title: 安装 Docker 引擎（Docker Engine）
description: Lists the installation methods
keywords: docker, installation, install, Docker Engine, Docker Engine, docker editions, stable, edge
redirect_from:
- /engine/installation/linux/
- /engine/installation/linux/frugalware/
- /engine/installation/frugalware/
- /engine/installation/linux/other/
- /engine/installation/linux/archlinux/
- /engine/installation/linux/cruxlinux/
- /engine/installation/linux/gentoolinux/
- /engine/installation/linux/docker-ce/
- /engine/installation/linux/docker-ee/
- /engine/installation/
- /en/latest/installation/
---


## 支持的平台

Docker 引擎可以在一系列服务器上进行安装，比如说  [Linux 平台](#server)，
[macOS](../../docker-for-mac/install.md) 和 [Windows 10](../../docker-for-windows/install.md)
需要通过 Docker 的 [静态二进制安装程序](binaries.md) 来进行客户端进行安装。

访问下面的链接访问可以支持的操作平台列表。

### 桌面系统

{% assign yes = '![yes](/images/green-check.svg){: .inline style="height: 14px; margin: 0 auto"}' %}

| 平台                                                          | x86_64 / amd64                                   |
|:------------------------------------------------------------------|:------------------------------------------------:|
| [Mac (macOS) Docker 桌面客户端](../../docker-for-mac/install.md) | [{{ yes }}](../../docker-for-mac/install.md)     |
| [Windows Docker 桌面客户端](../../docker-for-windows/install.md) | [{{ yes }}](../../docker-for-windows/install.md) |

### 服务器

Docker 针对下面的 Linux 分发平台和架构提供 `.deb` 和 `.rpm` 安装包：

| 平台              | x86_64 / amd64         | ARM                      | ARM64 / AARCH64        |
|:----------------------|:-----------------------|:-------------------------|:-----------------------|
| [CentOS](centos.md)   | [{{ yes }}](centos.md) |                          | [{{ yes }}](centos.md) |
| [Debian](debian.md)   | [{{ yes }}](debian.md) | [{{ yes }}](debian.md)   | [{{ yes }}](debian.md) |
| [Fedora](fedora.md)   | [{{ yes }}](fedora.md) |                          | [{{ yes }}](fedora.md) |
| [Raspbian](debian.md) |                        | [{{ yes }}](debian.md)   | [{{ yes }}](debian.md) |
| [Ubuntu](ubuntu.md)   | [{{ yes }}](ubuntu.md) | [{{ yes }}](ubuntu.md)   | [{{ yes }}](ubuntu.md) |

### 其他 Linux 分发包

> **Note**
>
> 下面的安装指南可能是工作的，Docker 没有对下面的安装平台进行测试和校验。

- 使用基于 Debian 衍生版本，例如： "BunsenLabs Linux"， "Kali Linux" 或 "LMDE" (Debian-based Mint) 请按照
  [Debian](debian.md) 的安装过程和帮助来进行安装, 并且使用相应的 Debian 的替代版本来进行进行安装。请参考你使用的操作系统版本的文档来找到与 Debian 版本对应的衍生版本。
-  使用基于 Ubuntu 衍生版本，例如： "Kubuntu", "Lubuntu" 或 "Xubuntu" 请按照 [Ubuntu](ubuntu.md) 的安装过程和帮助来进行安装, 
  并且使用相应的 Ubuntu 的替代版本来进行进行安装。请参考你使用的操作系统版本的文档来找到与 Ubuntu 版本对应的衍生版本。
- 一些 Linux 的发行版本会在这些操作系统的仓库中自行提供针对 Docker Engine 引擎的安装包。这些安装包是是这些 Linux 操作系统进行开发并且维护的，
  可能与你从基于源代码的编译结果来看有所不同。Docker 的官方与上面的发布版本没有任何关系也不会为其提供支持和缺陷修复。如果你发现有使用的问题，
  你应该向这些操作系统进行维护组织提出。

Docker 引擎针对手动进行安装，提供了 [binaries](binaries.md) 二进制安装包。这些二进制安装包应该可以使用在任何的 Linux 分发版本上。

## 发布渠道

Docker 引擎具有下面 3 个更新渠道： **stable**， **test** 和 **nightly**：

* **Stable** 渠道提供给你最新可用的稳定版本。
* **Test** 渠道提供了在发布之前的预览，被用于 general availability (GA) 之前的测试。
* **Nightly** 渠道在针对下一个主要发行版本的每天晚间自动构建包。

### 稳定版

年-月（Year-month） 的分支将会发布到 master 分支中。这个分支将会使用下面的格式 `<year>.<month>` 来创建，例如 `19.03`。
年-月的命名由 GA 版本的最早确定的日历数据来进行确定。所有随后的特性补丁将会通过在版本号的序列来进行发布。例如，一旦 `v19.03.0` 版本发布后，
所有的后续发布的版本将会在基于 `19.03` 这个分支下来发布。

### 测试

在计划进行新的 year-month 的发布之前，一个分支将会从 master 分支进行创建，并被命名为 `YY.mm`。这个表明的是基于 Docker 里程碑的开放已经完成了。
一个预发布的测试版本的发布版本进行发布。发布的补丁和相关预发布的发布内容将会发布到发布的分支中。

### 晚间构建

晚间构建将会给个你一个基于下一个主要发布版本的最新构建，这个最新的构建有最新的特性和版本的修复。

    0.0.0-YYYYmmddHHMMSS-abcdefabcdef

版本提交的 UTC 时间戳将会添加到发布版本的名称中，同时还会添加一个提交版本的哈希代码。如下：`0.0.0-20180720214833-f61e0f7`.

这个构建将会允许你使用最新的 master 分支来进行测试和构建。我们不能保证所有晚间构建能够正常的工作并且符合所有的安全性要求。

## 支持

基于 年-月（Year-month） 格式的 Docker 引擎发布通常能够被支持一个月直到下一个月的 GA 版本发布。

这个意味着缺陷报告和可能的反向一致发布将会被评估知道达到发布版本的生命周期。

当基于 年-月（Year-month）发布格式的发布达到生命周期后，Git 仓库的分支有可能会被删除。

### 反向移植（backport）

反向移植是 Docker 公司针对 Docker 进行优先处理的问题。一个 Docker 公司的雇员或者代码仓库的维护人员将会进行评估和确定这些问题的修复能够被支持，
并确定呢能够放到下一个 _发布_ 的版本中。leases.

如果你在提交代码的时候发现这个问题是一个比较重要的问题并且有可能面临反向移植（backport）问题。请确定在你提交的时候在提交内容高亮显示，你也可以在提交中明确说明。

### 升级路径

补丁的发布在升级的时候总是与基于 年-月（Year-month） 发布的版本是兼容的。

### 许可证

Copyright 2013-2020 Docker, inc, 文件的发布是基于 Apache 2.0 license 下进行发布。

Docker 是基于 Apache License, Version 2.0 许可证进行发布的。请查看 
[许可证](https://github.com/moby/moby/blob/master/LICENSE) 页面来获得更多的信息。

## 报告安全性问题

Docker 的维护者针对平台可能出现的安全问题非常重视。如果你在使用 Docker 的时候发现了任何问题，请马上与 Docker 的维护团队进行联系。

请 **不要** 将这些安全问题公开发布，请将这个安全问题发送邮件到 security@docker.com 邮箱中。

安全报告对我们来说非常重要，Docker 的维护团队将会公开的感谢您对安全问题的贡献。

## 开始使用

当你设置好 Docker 后，你可以开始学习 Docker 的一些基本使用了。
[Getting started with Docker](../../get-started/index.md).
