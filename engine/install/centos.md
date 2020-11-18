---
description: Instructions for installing Docker Engine on CentOS
keywords: requirements, apt, installation, centos, rpm, install, uninstall, upgrade, update
redirect_from:
- /engine/installation/centos/
- /engine/installation/linux/docker-ce/centos/
- /install/linux/centos/
- /install/linux/docker-ce/centos/
- /engine/installation/linux/centos/
title: Install Docker Engine on CentOS
toc_max: 4
---

如果希望在 CentOS 操作系统上安装 Docker ，请确定你需要安装的操作系统
[满足安装需求](#prerequisites)，
[安装 Docker](#installation-methods) 
页面中的内容。

## 安装要求

### 操作系统（OS） 要求

要在 CentOS 上安装 Docker，最低的操作系统版本需要为 CentOS 7。其他的早期版本不能够获得支持。

`centos-extras` 仓库需要被启用。这个仓库在默认情况下是启用的，但是可能因为其他的原因被关闭了，请参考 [重新启用 centos-extras 仓库](https://wiki.centos.org/AdditionalResources/Repositories) 页面中的内容。

推荐使用 `overlay2` 存储驱动。

### 卸载老的版本

老的 Docker 版本可能被称为  `docker` 或 `docker-engine`。如果这些老的 Docker 版本被安装的话，请首先进行卸载，同时也请卸载关联的依赖。

````bash
$ sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
````

如果在使用 `yum` 的时候，提示没有任何上面的包被安装的话，也没有关系。你可以跳过这个卸载的过程。reports that none of these packages are installed.

路径  `/var/lib/docker/` 下的内容包含有 镜像（images），容器（containers），卷（volumes），网络（networks）这些内容。这些内容是 Docker 容器运行需要的必要配置。

Docker 引擎（Docker Engine）的包，当前被修改称为 `docker-ce`。

## 安装方法

基于你的需求，你可以使用不同的方法安装 Docker 引擎（Docker Engine）：

- 绝大部分用户使用
  [设置 Docker 的仓库](#install-using-the-repository) ，然后从设置成功后的仓库进行安装。为了更加容易进行安装和升级任务，Docker 的官方推荐使用这种安装方式来进行安装。

- 一些用户可以使用下载的 RPM 包 ，然后
  [手动进行安装](#install-from-a-package) 然后你需要手动来进行升级。这种方法主要针对一些系统不具有联网环境，你需要下载后进行安装。

- 在一些测试和部署环境中，一些用户采用自动化脚本来安装 Docker，请访问链接：
  [自动化安装脚本](#install-using-the-convenience-script) 来了解更多。

### 使用仓库进行安装

在你对新安装的机器安装 Docker 之前，你需要设置 Docker 仓库。当仓库设置好以后，你可以从设置的仓库中对 Docker 进行安装和更新。

#### Set up the repository

{% assign download-url-base = "https://download.docker.com/linux/centos" %}

安装  `yum-utils` 包（这个安装包将会提供 `yum-config-manager` 工具）然后设置 **稳定（stable**）的仓库。

```bash
$ sudo yum install -y yum-utils

$ sudo yum-config-manager \
    --add-repo \
    {{ download-url-base }}/docker-ce.repo
```

> **可选的**：启用 **晚间构建（nightly）** 或 **测试（test）** 仓库。
>
> 上面的这些仓库包含有  `docker.repo` 文件，但是在默认情况下是禁用的。你可以和稳定版本仓库地址一样来启用它们。下面的内容显示的是启用 **晚间构建（nightly）**仓库的命令。
>
> ```bash
> $ sudo yum-config-manager --enable docker-ce-nightly
> ```
>
> 希望启用 **测试（test）**仓库，请使用下面的命令：
>
> ```bash
> $ sudo yum-config-manager --enable docker-ce-test
> ```
>
> 你可以通过运行 `yum-config-manager` 命令，并在命令后面添加  `--disable` 标记来禁用 **晚间构建（nightly）** 或 **测试（test）**仓库。
> 下面的命令是表示禁用 **晚间构建（nightly）**仓库：
>
> ```bash
> $ sudo yum-config-manager --disable docker-ce-nightly
> ```
>
> [了解更多有关**晚间构建（nightly）** 和 **测试（test）**的通道](index.md)。

#### 安装 Docker 引擎

1.  安装*最新版本*的 Docker 引擎和容器，或者使用后续的步骤来为安装的指定特定的版本：

    ```bash
    $ sudo yum install docker-ce docker-ce-cli containerd.io
    ```

    如果按照的时候提示需要校验 GPG Key，请确定指纹与字符串 `060A 61C5 1B55 8A7F 742B 77AA C52F EB6B 621E 9F35` 是吻合的，然后选择接受。

    > 获得了多个 Docker 的仓库？
    >
    > 如果你有多个 Docker 仓库被启用了，在使用  `yum install` 或 `yum update` 命令对 Docker 进行安装和升级的时候，如果你没有指定版本，
    > 那么上面的命令将会尝试使用最新的版本进行安装。这有可能导致安装的版本不是你需要的。

    Docker 被安装了，但是没有启动。这是因为 `docker` 组已经被创建了，但是还没有用户添加到组中。

2.  针对 Docker 的安装*指定版本*的 Docker 引擎（Docker Engine），列出给定仓库中可用的 Docker 版本，然后选择需要的版本来进行安装：

    a. 分类列出你仓库中可用的 Docker 版本。下面的示例列出了通过版本好进行分类的结果，从高到低的分类：

    ```bash
    $ yum list docker-ce --showduplicates | sort -r

    docker-ce.x86_64  3:18.09.1-3.el7                     docker-ce-stable
    docker-ce.x86_64  3:18.09.0-3.el7                     docker-ce-stable
    docker-ce.x86_64  18.06.1.ce-3.el7                    docker-ce-stable
    docker-ce.x86_64  18.06.0.ce-3.el7                    docker-ce-stable
    ```

    上面的列表是基于你启用的仓库不同来指定你 CentOS 操作系统的版本（如上面所示，使用 `el7` 后缀来标记）。

    b. 通过提供完整的包的名字来安装指定的版本的 Docke 引擎。完整的路径包括有包的名字（`docker-ce`）并且加上第二列提供的版本字符串。
       从第一个冒号（`:`）后的字符开始计算，截止于分隔符（`-`）之前的字符。
       例如： `docker-ce-18.09.1`。

    ```bash
    $ sudo yum install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING> containerd.io
    ```

    Docker 被安装了，但是没有启动。这是因为 `docker` 组已经被创建了，但是还没有用户添加到组中。

3.  启动 Docker

    ```bash
    $ sudo systemctl start docker
    ```

4.  通过运行  `hello-world` 镜像（image）来确定 Docker 安装成功了。

    ```bash
    $ sudo docker run hello-world
    ```

    这个命令将会下载一个测试镜像并且在容器中运行。如果容器是运行的话，这个命令将会打印出一些信息后退出。

Docker 引擎已经安装并且运行了，你需要使用 `sudo` 来运行 Docker 的命令。请继续阅读页面 [Linux 安装 Docker 的后续步骤](linux-postinstall.md) 
中的内容来允许你操作系统中没有权限的用户来允许 Docker 命令和其他的一些配置选项。

#### 升级 Docker 引擎

希望对 Docker 引擎进行申请，请按照 [使用仓库进行安装](#install-using-the-repository)，步骤，来选择你希望安装的新版本。

### Install from a package

If you cannot use Docker's repository to install Docker, you can download the
`.rpm` file for your release and install it manually. You need to download
a new file each time you want to upgrade Docker Engine.

1.  Go to [{{ download-url-base }}/]({{ download-url-base }}/){: target="_blank" rel="noopener" class="_" }
    and choose your version of CentOS. Then browse to `x86_64/stable/Packages/`
    and download the `.rpm` file for the Docker version you want to install.

    > **Note**: To install a **nightly** or **test** (pre-release) package,
    > change the word `stable` in the above URL to `nightly` or `test`.
    > [Learn about **nightly** and **test** channels](index.md).

2.  Install Docker Engine, changing the path below to the path where you downloaded
    the Docker package.

    ```bash
    $ sudo yum install /path/to/package.rpm
    ```

    Docker is installed but not started. The `docker` group is created, but no
    users are added to the group.

3.  Start Docker.

    ```bash
    $ sudo systemctl start docker
    ```

4.  Verify that Docker Engine is installed correctly by running the `hello-world`
    image.

    ```bash
    $ sudo docker run hello-world
    ```

    This command downloads a test image and runs it in a container. When the
    container runs, it prints an informational message and exits.

Docker Engine is installed and running. You need to use `sudo` to run Docker commands.
Continue to [Post-installation steps for Linux](linux-postinstall.md) to allow
non-privileged users to run Docker commands and for other optional configuration
steps.

#### Upgrade Docker Engine

To upgrade Docker Engine, download the newer package file and repeat the
[installation procedure](#install-from-a-package), using `yum -y upgrade`
instead of `yum -y install`, and pointing to the new file.

{% include install-script.md %}

## Uninstall Docker Engine

1.  Uninstall the Docker Engine, CLI, and Containerd packages:

    ```bash
    $ sudo yum remove docker-ce docker-ce-cli containerd.io
    ```

2.  Images, containers, volumes, or customized configuration files on your host
    are not automatically removed. To delete all images, containers, and
    volumes:

    ```bash
    $ sudo rm -rf /var/lib/docker
    ```

You must delete any edited configuration files manually.

## Next steps

- Continue to [Post-installation steps for Linux](linux-postinstall.md).
- Review the topics in [Develop with Docker](../../develop/index.md) to learn how to build new applications using Docker.
