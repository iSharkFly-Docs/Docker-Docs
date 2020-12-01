---
description: How to network Docker containers.
keywords: Examples, Usage, volume, docker, documentation, user guide, data, volumes
redirect_from:
- /engine/userguide/containers/networkigncontainers/
- /engine/userguide/networkigncontainers/
title: 容器的网络（Network containers）
---

如果你通过 Docker 提供的用户指南，你应该已经完成了构建你的第一个 Docker 容器，并且运行了示例应用。
你已经构建了你自己的镜像（images）。本部分的内容将会指导你如何对你的容器进行网络配置。

## 使用默认网络来运行一个容器

Docker 能够支持通过  **network drivers** 来使用网络的容器。在默认的情况下，Docker 为你提供了 2 个网络驱动： `bridge` 和 `overlay` 驱动。
你也可以通过写一个网络驱动插件来创建你自己的网络驱动，但是这个属于比较高级的任务了。

在任何完成安装的 Docker 中将会自动包含有下面 3 个网络驱动，你可以通过下面的命令来列表出来：

    $ docker network ls

    NETWORK ID          NAME                DRIVER
    18a2866682b8        none                null
    c288470c46f6        host                host
    7b369448dccb        bridge              bridge

被命名 `bridge` 的网络是一个特殊的网络。除非你在运行的时候指定一个网络，否则 Docker 容器将会一直运行这个网络。尝试运行下面的命令：

    $ docker run -itd --name=networktest ubuntu

    74695c9cea6d9810718fddadc01a727a5dd3ce6a69d09752239736c030599741

![bridge1](bridge1.png)

通过检查网络，可以非常容易的找到你容器的 IP 地址。

```bash
$ docker network inspect bridge

[
    {
        "Name": "bridge",
        "Id": "f7ab26d71dbd6f557852c7156ae0574bbf62c42f539b50c8ebde0f728a253b6f",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "172.17.0.1/16",
                    "Gateway": "172.17.0.1"
                }
            ]
        },
        "Internal": false,
        "Containers": {
            "3386a527aa08b37ea9232cbcace2d2458d49f44bb05a6b775fba7ddd40d8f92c": {
                "Name": "networktest",
                "EndpointID": "647c12443e91faf0fd508b6edfe59c30b642abb60dfab890b4bdccee38750bc1",
                "MacAddress": "02:42:ac:11:00:02",
                "IPv4Address": "172.17.0.2/16",
                "IPv6Address": ""
            }
        },
        "Options": {
            "com.docker.network.bridge.default_bridge": "true",
            "com.docker.network.bridge.enable_icc": "true",
            "com.docker.network.bridge.enable_ip_masquerade": "true",
            "com.docker.network.bridge.host_binding_ipv4": "0.0.0.0",
            "com.docker.network.bridge.name": "docker0",
            "com.docker.network.driver.mtu": "9001"
        },
        "Labels": {}
    }
]
```

通过断开与容器的链接，你也可以将容器从网络中删除。
如果要将容器从网络中删除的话，你需要同时提供网络名（network name）和容器名（container name）。
你也可以使用容器 ID，但是使用容器名相对使用容器 ID 来说，更加快速。

    $ docker network disconnect bridge networktest

尽管你可以将容器从一个网络中断开连接，但是你不能删除 Docker 内部构建的被命名为 `bridge` 的 `bridge` 网络。
网络是将一个容器与其他容器独立开或者容器与其他网络独立开的最常规的方式。
因此，当你有更多使用 Docker 经验的时候，可以尝试创建你自己的网络。

## 创建你自己的桥接网络

Docker 引擎能够原生支持桥接网络（bridge networks）和覆盖网络（overlay networks）。

桥接网络被限制用于一个独立主机运行的 Docker 引擎。覆盖网络能够包含有多个主机，这个有更多的高级特性。

下面的例子显示了如何创建一个桥接网络： 

    $ docker network create -d bridge my_bridge

参数 `-d` 用于告诉 Docker 在新的网络中使用  `桥接（bridge）` 驱动。

名字 `bridge` 是默认使用的网络名字，在创建的时候可以不指定这个参数，那么将会使用默认的网络名字来创建。

当你创建成功后，可以使用下面的命令来查看你机器中的网络配置：

    $ docker network ls

    NETWORK ID          NAME                DRIVER
    7b369448dccb        bridge              bridge
    615d565d498c        my_bridge           bridge
    18a2866682b8        none                null
    c288470c46f6        host                host

如果你使用下面的命令检查网络的话，你会看到在这里面没有任何内容。

    $ docker network inspect my_bridge

    [
        {
            "Name": "my_bridge",
            "Id": "5a8afc6364bccb199540e133e63adb76a557906dd9ff82b94183fc48c40857ac",
            "Scope": "local",
            "Driver": "bridge",
            "IPAM": {
                "Driver": "default",
                "Config": [
                    {
                        "Subnet": "10.0.0.0/24",
                        "Gateway": "10.0.0.1"
                    }
                ]
            },
            "Containers": {},
            "Options": {},
            "Labels": {}
        }
    ]

## 添加容器到一个网络
要创建一个安全并且能够协同运行的 Web 应用程序，你需要创建一个网络。

通过网络，在默认情况下为容器提供了完全独立的环境。在你第一次运行一个容器的时候，你可以将容器添加到一个网络中。

例如，我们希望运行一个容器来运行 PostgreSQL 数据库，并且传递 `--net=my_bridge` 标记来到你新网络的连接中，可以运行下面的命令：

    $ docker run -d --net=my_bridge --name db training/postgres

如果你检查你的 `my_bridge` ，你可以看到已经有一个容器被添加（attached）上去了。

你也可以检查你的容器来查看连接在哪里：

    {% raw %}
    $ docker inspect --format='{{json .NetworkSettings.Networks}}'  db
    {% endraw %}

    {"my_bridge":{"NetworkID":"7d86d31b1478e7cca9ebed7e73aa0fdeec46c5ca29497431d3007d2d9e15ed99",
    "EndpointID":"508b170d56b2ac9e4ef86694b0a76a22dd3df1983404f7321da5649645bf7043","Gateway":"10.0.0.1","IPAddress":"10.0.0.254","IPPrefixLen":24,"IPv6Gateway":"","GlobalIPv6Address":"","GlobalIPv6PrefixLen":0,"MacAddress":"02:42:ac:11:00:02"}}

现在，你可以使用你熟悉的命令来启动一个 Web 应用程序了。这次不需要指定一个网络。

    $ docker run -d --name web training/webapp python app.py

![bridge2](bridge2.png)

你的 `web` 应用运行在哪个网络下呢？可以检查应用来确定这个应用运行在默认的 `桥接（bridge）` 网络。

    {% raw %}
    $ docker inspect --format='{{json .NetworkSettings.Networks}}'  web
    {% endraw %}

    {"bridge":{"NetworkID":"7ea29fc1412292a2d7bba362f9253545fecdfa8ce9a6e37dd10ba8bee7129812",
    "EndpointID":"508b170d56b2ac9e4ef86694b0a76a22dd3df1983404f7321da5649645bf7043","Gateway":"172.17.0.1","IPAddress":"10.0.0.2","IPPrefixLen":24,"IPv6Gateway":"","GlobalIPv6Address":"","GlobalIPv6PrefixLen":0,"MacAddress":"02:42:ac:11:00:02"}}

然后获得你 `web` 应用的 IP 地址。

    {% raw %}
    $ docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' web
    {% endraw %}

    172.17.0.2

现在，可以打开一个 shell 来运行 `db` 容器：

    $ docker container exec -it db bash

    root@a205f0dd33b2:/# ping 172.17.0.2
    ping 172.17.0.2
    PING 172.17.0.2 (172.17.0.2) 56(84) bytes of data.
    ^C
    --- 172.17.0.2 ping statistics ---
    44 packets transmitted, 0 received, 100% packet loss, time 43185ms

在过一段时间后，可以使用 `CTRL-C` 来终止 `ping` 命令，请注意 ping 显示终止了。

这是因为这个 2 个容器运行在不同的网络中，你可以使用 `exit` 命令来关闭容器进行修复。

Docker 网络运行你附件一个容器到多个你愿意的网络上。你甚至可以添加到一个正在运行的容器上。

运行下面的命令，将 `web` 应用添加到 `my_bridge` 网络上。

    $ docker network connect my_bridge web


![bridge3](bridge3.png)

打开 shell 然后再次进入 `db` 应用，然后尝试使用 ping 命令。这次你可以仅仅使用容器的名字 `web` 就可以了，而不需要使用 IP 地址。

    $ docker container exec -it db bash

    root@a205f0dd33b2:/# ping web
    PING web (10.0.0.2) 56(84) bytes of data.
    64 bytes from web (10.0.0.2): icmp_seq=1 ttl=64 time=0.095 ms
    64 bytes from web (10.0.0.2): icmp_seq=2 ttl=64 time=0.060 ms
    64 bytes from web (10.0.0.2): icmp_seq=3 ttl=64 time=0.066 ms
    ^C
    --- web ping statistics ---
    3 packets transmitted, 3 received, 0% packet loss, time 2000ms
    rtt min/avg/max/mdev = 0.060/0.073/0.095/0.018 ms

命令 `ping` 显示连接到了一个不同的 IP 地址，这个在 `my_bridge` 上的 IP 地址与 `bridge` 网络上的 IP 地址是不同的。

## 下一步

Now that you know how to network containers, see [how to manage data in containers](../../storage/volumes.md).
