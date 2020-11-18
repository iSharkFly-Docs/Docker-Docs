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

## Installation methods

You can install Docker Engine in different ways, depending on your needs:

- Most users
  [set up Docker's repositories](#install-using-the-repository) and install
  from them, for ease of installation and upgrade tasks. This is the
  recommended approach.

- Some users download the RPM package and
  [install it manually](#install-from-a-package) and manage
  upgrades completely manually. This is useful in situations such as installing
  Docker on air-gapped systems with no access to the internet.

- In testing and development environments, some users choose to use automated
  [convenience scripts](#install-using-the-convenience-script) to install Docker.

### Install using the repository

Before you install Docker Engine for the first time on a new host machine, you need
to set up the Docker repository. Afterward, you can install and update Docker
from the repository.

#### Set up the repository

{% assign download-url-base = "https://download.docker.com/linux/centos" %}

Install the `yum-utils` package (which provides the `yum-config-manager`
utility) and set up the **stable** repository.

```bash
$ sudo yum install -y yum-utils

$ sudo yum-config-manager \
    --add-repo \
    {{ download-url-base }}/docker-ce.repo
```

> **Optional**: Enable the **nightly** or **test** repositories.
>
> These repositories are included in the `docker.repo` file above but are disabled
> by default. You can enable them alongside the stable repository.  The following
> command enables the **nightly** repository.
>
> ```bash
> $ sudo yum-config-manager --enable docker-ce-nightly
> ```
>
> To enable the **test** channel, run the following command:
>
> ```bash
> $ sudo yum-config-manager --enable docker-ce-test
> ```
>
> You can disable the **nightly** or **test** repository by running the
> `yum-config-manager` command with the `--disable` flag. To re-enable it, use
> the `--enable` flag. The following command disables the **nightly** repository.
>
> ```bash
> $ sudo yum-config-manager --disable docker-ce-nightly
> ```
>
> [Learn about **nightly** and **test** channels](index.md).

#### Install Docker Engine

1.  Install the _latest version_ of Docker Engine and containerd, or go to the next step to install a specific version:

    ```bash
    $ sudo yum install docker-ce docker-ce-cli containerd.io
    ```

    If prompted to accept the GPG key, verify that the fingerprint matches
    `060A 61C5 1B55 8A7F 742B 77AA C52F EB6B 621E 9F35`, and if so, accept it.

    > Got multiple Docker repositories?
    >
    > If you have multiple Docker repositories enabled, installing
    > or updating without specifying a version in the `yum install` or
    > `yum update` command always installs the highest possible version,
    > which may not be appropriate for your stability needs.

    Docker is installed but not started. The `docker` group is created, but no users are added to the group.

2.  To install a _specific version_ of Docker Engine, list the available versions
    in the repo, then select and install:

    a. List and sort the versions available in your repo. This example sorts
       results by version number, highest to lowest, and is truncated:

    ```bash
    $ yum list docker-ce --showduplicates | sort -r

    docker-ce.x86_64  3:18.09.1-3.el7                     docker-ce-stable
    docker-ce.x86_64  3:18.09.0-3.el7                     docker-ce-stable
    docker-ce.x86_64  18.06.1.ce-3.el7                    docker-ce-stable
    docker-ce.x86_64  18.06.0.ce-3.el7                    docker-ce-stable
    ```

    The list returned depends on which repositories are enabled, and is specific
    to your version of CentOS (indicated by the `.el7` suffix in this example).

    b. Install a specific version by its fully qualified package name, which is
       the package name (`docker-ce`) plus the version string (2nd column)
       starting at the first colon (`:`), up to the first hyphen, separated by
       a hyphen (`-`). For example, `docker-ce-18.09.1`.

    ```bash
    $ sudo yum install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING> containerd.io
    ```

    Docker is installed but not started. The `docker` group is created, but no users are added to the group.

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

Docker Engine is installed and running. You need to use `sudo` to run Docker
commands. Continue to [Linux postinstall](linux-postinstall.md) to allow
non-privileged users to run Docker commands and for other optional configuration
steps.

#### Upgrade Docker Engine

To upgrade Docker Engine, follow the [installation instructions](#install-using-the-repository),
choosing the new version you want to install.

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
