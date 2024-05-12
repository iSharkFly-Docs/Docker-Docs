Alpine 操作系统是一个面向安全的轻型 Linux 发行版。它不同于通常 Linux 发行版，Alpine 采用了 musl libc 和 busybox 以减小系统的体积和运行时资源消耗，但功能上比 busybox 又完善的多，因此得到开源社区越来越多的青睐。

在保持瘦身的同时，Alpine 还提供了自己的包管理工具 apk，可以通过 https://pkgs.alpinelinux.org/packages 网站上查询包信息，也可以直接通过 apk 命令直接查询和安装各种软件。

![](https://cdn.isharkfly.com/com-isharkfly-www/discourse-uploads/original/2X/a/a417e5b882442735abb1436afed5223f9d02d873.webp)

Alpine 由非商业组织维护的，支持广泛场景的 Linux发行版，它特别为资深/重度Linux用户而优化，关注安全，性能和资源效能。Alpine 镜像可以适用于更多常用场景，并且是一个优秀的可以适用于生产的基础系统/环境。

Alpine Docker 镜像也继承了 Alpine Linux 发行版的这些优势。相比于其他 Docker 镜像，它的容量非常小，仅仅只有 5 MB 左右（对比 Ubuntu 系列镜像接近 200 MB），且拥有非常友好的包管理机制。官方镜像来自 docker-alpine 项目。

目前 Docker 官方已开始推荐使用 Alpine 替代之前的 Ubuntu 做为基础镜像环境。这样会带来多个好处。包括镜像下载速度加快，镜像安全性提高，主机之间的切换更方便，占用更少磁盘空间等。


下表是官方镜像的大小比较：

```text
 
REPOSITORY          TAG           IMAGE ID          VIRTUAL SIZE
alpine              latest        4e38e38c8ce0      4.799 MB
debian              latest        4d6ce913b130      84.98 MB
ubuntu              latest        b39b81afc8ca      188.3 MB
centos              latest        8efe422e6104      210 MB
 ```
## 特点

###小巧
Alpine Linux是围绕musl libc和busybox构建的。这使得它比传统的GNU / Linux发行版更小，资源效率更高。容器不需要超过8 MB，最小的磁盘安装需要大约130 MB的存储空间。不仅可以获得完全成熟的Linux环境，还可以从存储库中获得大量的软件包。
二进制包被稀释和拆分，可以更好地控制安装的内容，从而使环境尽可能小而有效。

### 简单
Alpine Linux是一个非常简单的发行版，它会尽量避免使用。它使用自己的包管理器名为apk，OpenRC init系统，提供了一个简单，清晰的Linux环境。然后，您可以添加项目所需的软件包，无论是构建iSCSI存储控制器，薄薄的邮件服务器容器，还是坚如磐石的嵌入式交换机，没有别的办法阻碍。

### 安全
Alpine Linux的设计考虑了安全性。内核使用grsecurity / PaX的非官方端口进行修补，所有userland二进制文件都编译为具有堆栈粉碎保护的位置独立可执行文件（PIE）。这些主动安全功能可防止利用整个类的零日漏洞和其他漏洞。

正是基于上面的原因，我们才能看见在很多的 Docker 的镜像中有  alpine 的名称。

这表明这个镜像是基于 alpine 构建的。

## 获取并使用官方镜像

由于镜像很小，下载时间往往很短，读者可以直接使用 `docker run` 指令直接运行一个 `Alpine` 容器，并指定运行的 Linux 指令，例如：

```
PS C:\Users\yhu> docker run alpine echo '123'
Unable to find image 'alpine:latest' locally
latest: Pulling from library/alpine
4abcf2066143: Already exists
Digest: sha256:c5b1261d6d3e43071626931fc004f70149baeba2c8ec672bd4f27761f8e1ad6b
Status: Downloaded newer image for alpine:latest
123
```

![](https://cdn.isharkfly.com/com-isharkfly-www/discourse-uploads/original/2X/7/726eeabcfbc27195802cf97e8f4c5b847785372f.png)

如果通过容器管理查看容器的大小，也只有 50MB。

如果再加个 JDK 那可比这个大多了，操作系统的大小还不如一个 JDK。

![](https://cdn.isharkfly.com/com-isharkfly-www/discourse-uploads/original/2X/9/975f374bc9bfc84d701a2dfa4ec5dcff9a170fb0.png)

## 迁移至 Alpine 基础镜像

目前，大部分 Docker 官方镜像都已经支持 `Alpine` 作为基础镜像，可以很容易进行迁移。

例如：

* `ubuntu/debian` -> `alpine`
* `python:3` -> `python:3-alpine`
* `ruby:2.6` -> `ruby:2.6-alpine`

另外，如果使用 `Alpine` 镜像替换 `Ubuntu` 基础镜像，安装软件包时需要用 `apk` 包管理器替换 `apt` 工具，如

```bash
$ apk add --no-cache <package>
```

`Alpine` 中软件安装包的名字可能会与其他发行版有所不同，可以在 `https://pkgs.alpinelinux.org/packages` 网站搜索并确定安装包名称。

如果需要的安装包不在主索引内，但是在测试或社区索引中。

那么可以按照以下方法使用这些安装包。

```bash
$ echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories
$ apk --update add --no-cache <package>
```

由于在国内访问 `apk` 仓库较缓慢，建议在使用 `apk` 之前先替换仓库地址为国内镜像。

下面的命令使用的是阿里云的仓库地址来进行替代。

```docker
RUN sed -i "s/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g" /etc/apk/repositories \
      && apk add --no-cache <package>
```

## 相关资源

* `Alpine` 官网：https://www.alpinelinux.org/
* `Alpine` 官方仓库：https://github.com/alpinelinux
* `Alpine` 官方镜像：https://hub.docker.com/_/alpine/
* `Alpine` 官方镜像仓库：https://github.com/gliderlabs/docker-alpine