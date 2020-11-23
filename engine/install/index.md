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

| Platform                                                          | x86_64 / amd64                                   |
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

- 使用基于 Debian 衍生版本，例如： "BunsenLabs Linux"， "Kali Linux" 或者 "LMDE" (Debian-based Mint) 请按照
  [Debian](debian.md) 的安装过程和帮助来进行安装, 并且使用相应的 Debian 的替代版本来进行进行安装。请参考你使用的操作系统版本的文档来找到与 Debian 版本对应的衍生版本。
-  使用基于 Ubuntu 衍生版本，例如： "Kubuntu", "Lubuntu" or "Xubuntu" 请按照 [Ubuntu](ubuntu.md) 的安装过程和帮助来进行安装, 
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

Year-month releases are made from a release branch diverged from the master
branch. The branch is created with format `<year>.<month>`, for example
`19.03`. The year-month name indicates the earliest possible calendar
month to expect the release to be generally available. All further patch
releases are performed from that branch. For example, once `v19.03.0` is
released, all subsequent patch releases are built from the `19.03` branch.

### 测试

In preparation for a new year-month release, a branch is created from
the master branch with format `YY.mm` when the milestones desired by
Docker for the release have achieved feature-complete. Pre-releases
such as betas and release candidates are conducted from their respective release
branches. Patch releases and the corresponding pre-releases are performed
from within the corresponding release branch.

### 晚间构建

Nightly builds give you the latest builds of work in progress for the next major
release. They are created once per day from the master branch with the version
format:

    0.0.0-YYYYmmddHHMMSS-abcdefabcdef

where the time is the commit time in UTC and the final suffix is the prefix
of the commit hash, for example `0.0.0-20180720214833-f61e0f7`.

These builds allow for testing from the latest code on the master branch. No
qualifications or guarantees are made for the nightly builds.

## 支持

Docker Engine releases of a year-month branch are supported with patches as
needed for one month after the next year-month general availability release.

This means bug reports and backports to release branches are assessed
until the end-of-life date.

After the year-month branch has reached end-of-life, the branch may be
deleted from the repository.

### Backporting

Backports to the Docker products are prioritized by the Docker company. A
Docker employee or repository maintainer will endeavour to ensure sensible
bugfixes make it into _active_ releases.

If there are important fixes that ought to be considered for backport to
active release branches, be sure to highlight this in the PR description
or by adding a comment to the PR.

### 升级路径

Patch releases are always backward compatible with its year-month version.

### 许可证

Docker is licensed under the Apache License, Version 2.0. See
[LICENSE](https://github.com/moby/moby/blob/master/LICENSE) for the full
license text.

## 报告安全性问题

The Docker maintainers take security seriously. If you discover a security
issue, please bring it to their attention right away!

Please DO NOT file a public issue; instead send your report privately
to security@docker.com.

Security reports are greatly appreciated, and Docker will publicly thank you
for it.

## 开始使用

After setting up Docker, you can learn the basics with
[Getting started with Docker](../../get-started/index.md).
