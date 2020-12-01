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

To build web applications that act in concert but do so securely, create a
network. Networks, by definition, provide complete isolation for containers. You
can add containers to a network when you first run a container.

Launch a container running a PostgreSQL database and pass it the `--net=my_bridge` flag to connect it to your new network:

    $ docker run -d --net=my_bridge --name db training/postgres

If you inspect your `my_bridge` you can see it has a container attached.
You can also inspect your container to see where it is connected:

    {% raw %}
    $ docker inspect --format='{{json .NetworkSettings.Networks}}'  db
    {% endraw %}

    {"my_bridge":{"NetworkID":"7d86d31b1478e7cca9ebed7e73aa0fdeec46c5ca29497431d3007d2d9e15ed99",
    "EndpointID":"508b170d56b2ac9e4ef86694b0a76a22dd3df1983404f7321da5649645bf7043","Gateway":"10.0.0.1","IPAddress":"10.0.0.254","IPPrefixLen":24,"IPv6Gateway":"","GlobalIPv6Address":"","GlobalIPv6PrefixLen":0,"MacAddress":"02:42:ac:11:00:02"}}

Now, go ahead and start your by now familiar web application. This time don't specify a network.

    $ docker run -d --name web training/webapp python app.py

![bridge2](bridge2.png)

Which network is your `web` application running under? Inspect the application to verify that it is running in the default `bridge` network.

    {% raw %}
    $ docker inspect --format='{{json .NetworkSettings.Networks}}'  web
    {% endraw %}

    {"bridge":{"NetworkID":"7ea29fc1412292a2d7bba362f9253545fecdfa8ce9a6e37dd10ba8bee7129812",
    "EndpointID":"508b170d56b2ac9e4ef86694b0a76a22dd3df1983404f7321da5649645bf7043","Gateway":"172.17.0.1","IPAddress":"10.0.0.2","IPPrefixLen":24,"IPv6Gateway":"","GlobalIPv6Address":"","GlobalIPv6PrefixLen":0,"MacAddress":"02:42:ac:11:00:02"}}

Then, get the IP address of your `web`

    {% raw %}
    $ docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' web
    {% endraw %}

    172.17.0.2

Now, open a shell to your running `db` container:

    $ docker container exec -it db bash

    root@a205f0dd33b2:/# ping 172.17.0.2
    ping 172.17.0.2
    PING 172.17.0.2 (172.17.0.2) 56(84) bytes of data.
    ^C
    --- 172.17.0.2 ping statistics ---
    44 packets transmitted, 0 received, 100% packet loss, time 43185ms

After a bit, use `CTRL-C` to end the `ping` and notice that the ping failed. That is because the two containers are running on different networks. You can fix that. Then, use the `exit` command to close the container.

Docker networking allows you to attach a container to as many networks as you like. You can also attach an already running container. Go ahead and attach your running `web` app to the `my_bridge`.

    $ docker network connect my_bridge web


![bridge3](bridge3.png)

Open a shell into the `db` application again and try the ping command. This time just use the container name `web` rather than the IP address.

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

The `ping` shows it is contacting a different IP address, the address on the `my_bridge` which is different from its address on the `bridge` network.

## Next steps

Now that you know how to network containers, see [how to manage data in containers](../../storage/volumes.md).
