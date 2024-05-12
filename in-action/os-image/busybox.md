BusyBox是一个遵循GPL协议、以自由软件形式发行的应用程序。

Busybox在单一的可执行文件中提供了精简的Unix工具集，可运行于多款POSIX环境的操作系统，例如Linux（包括Android）、Hurd、FreeBSD等等。

由于BusyBox可执行文件的文件比较小，使得它非常适合使用于嵌入式系统。

作者将BusyBox称为“嵌入式Linux的瑞士军刀”。

![](https://cdn.isharkfly.com/com-isharkfly-www/discourse-uploads/original/2X/9/9476441a8d5ae2280eb7dfbdc1b26be085b314b2.png)

在以前，Docker 官方为了压缩容量，保证容器的启用，其实都在使用 busybox，但后期，Docker 官方开始使用 Alpine 来替代 busybox。

## 获取官方镜像

可以使用 `docker pull` 指令下载 `busybox:latest` 镜像：

```bash
PS C:\Users\yhu> docker pull busybox:latest
latest: Pulling from library/busybox
ec562eabd705: Pull complete
Digest: sha256:5eef5ed34e1e1ff0a4ae850395cbf665c4de6b4b83a32a0bc7bcb998e24e7bbb
Status: Downloaded newer image for busybox:latest
docker.io/library/busybox:latest

What's Next?
  View a summary of image vulnerabilities and recommendations → docker scout quickview busybox:latest
PS C:\Users\yhu>
```

下载后，可以看到 `busybox` 镜像只有 *4.26 MB*：

```bash
PS C:\Users\yhu> docker image ls
REPOSITORY                                        TAG               IMAGE ID       CREATED         SIZE
repo-docker.isharkfly.com/docker-hub/visatrack    latest            a329341dbaeb   3 days ago      522MB
repo-docker.isharkfly.com/docker-hub/visatrack    <none>            f5f9d8b3b410   3 days ago      522MB
alpine/git                                        latest            80ed206c002b   7 days ago      50.4MB
data-mq-service                                   0.0.1-SNAPSHOT    7eb277a365d6   3 weeks ago     475MB
docsify-docs                                      0.0.1             32062033284a   6 weeks ago     1.13GB
<none>                                            <none>            0ebfbefe1d52   6 weeks ago     1.13GB
alpine                                            latest            05455a08881e   3 months ago    7.38MB
zchub-crawler                                     latest            b20aa408fe8f   7 months ago    1.6GB
mq-service                                        0.0.1-SNAPSHOT    308dd50eb67a   7 months ago    441MB
reso-web-api-reference-server-odata-manager-app   latest            27cdaae03879   8 months ago    441MB
reso-builder                                      latest            cabba9a35a22   8 months ago    1.47GB
busybox                                           latest            65ad0d468eb1   11 months ago   4.26MB
tutor-service                                     0.0.1-SNAPSHOT    20d2f52a1fc4   13 months ago   521MB
sharkfly-wechat-service                           0.0.1-SNAPSHOT    0d3e7843994e   13 months ago   465MB
eclipse-temurin                                   17-jdk-alpine     9a0a4e74d117   13 months ago   358MB
rabbitmq                                          3.11-management   04a3a28a368b   13 months ago   255MB
framework-spring-docker                           0.0.1-SNAPSHOT    42e51829e8c7   15 months ago   379MB
adoptopenjdk/openjdk11-openj9                     alpine            b533cd6150ba   15 months ago   379MB
mysql/mysql-server                                latest            1d9c2219ff69   16 months ago   496MB
docker101tutorial                                 latest            e60bd4e10534   17 months ago   47MB
alpine/git                                        <none>            22d84a66cda4   17 months ago   43.6MB
PS C:\Users\yhu>
```

如果只说是大小来说，Alpine 也大不了多少，但 Alpine 提供了更多的功能。

![](https://cdn.isharkfly.com/com-isharkfly-www/discourse-uploads/optimized/2X/9/91d312f7dcb94ff748f848881baac4cbd4ea8f2c_2_690x390.png)

这也就是为什么 Docker 官方切换到 Alpine 的原因。

## 运行 busybox

启动一个 `busybox` 容器，并在容器中执行 `grep` 命令。

从启动的速度来看，那就是几乎是光速了。

```bash
PS C:\Users\yhu> docker run -it busybox
/ # grep
BusyBox v1.36.1 (2023-05-18 22:34:17 UTC) multi-call binary.

Usage: grep [-HhnlLoqvsrRiwFE] [-m N] [-A|B|C N] { PATTERN | -e PATTERN... | -f FILE... } [FILE]...

Search for PATTERN in FILEs (or stdin)

        -H      Add 'filename:' prefix
        -h      Do not add 'filename:' prefix
        -n      Add 'line_no:' prefix
        -l      Show only names of files that match
        -L      Show only names of files that don't match
        -c      Show only count of matching lines
        -o      Show only the matching part of line
        -q      Quiet. Return 0 if PATTERN is found, 1 otherwise
        -v      Select non-matching lines
        -s      Suppress open and read errors
        -r      Recurse
        -R      Recurse and dereference symlinks
        -i      Ignore case
        -w      Match whole words only
        -x      Match whole lines only
        -F      PATTERN is a literal (not regexp)
        -E      PATTERN is an extended regexp
        -m N    Match up to N times per file
        -A N    Print N lines of trailing context
        -B N    Print N lines of leading context
        -C N    Same as '-A N -B N'
        -e PTRN Pattern to match
        -f FILE Read pattern from file
/ #
```

查看容器内的挂载信息。

```bash
/ # mount
overlay on / type overlay (rw,relatime,lowerdir=/var/lib/docker/overlay2/l/K7LGRMOMB4YBJOAIY37TDH27OH:/var/lib/docker/overlay2/l/WV2IR37DT2RO7IBXLLNKC5WMBI,upperdir=/var/lib/docker/overlay2/deeb782171b9c2a33054df6b46a3125dc7d283d3af2136a4cc2aa84ec9c9a388/diff,workdir=/var/lib/docker/overlay2/deeb782171b9c2a33054df6b46a3125dc7d283d3af2136a4cc2aa84ec9c9a388/work)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev type tmpfs (rw,nosuid,size=65536k,mode=755)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=666)
sysfs on /sys type sysfs (ro,nosuid,nodev,noexec,relatime)
tmpfs on /sys/fs/cgroup type tmpfs (rw,nosuid,nodev,noexec,relatime,mode=755)
cpuset on /sys/fs/cgroup/cpuset type cgroup (ro,nosuid,nodev,noexec,relatime,cpuset)
cpu on /sys/fs/cgroup/cpu type cgroup (ro,nosuid,nodev,noexec,relatime,cpu)
cpuacct on /sys/fs/cgroup/cpuacct type cgroup (ro,nosuid,nodev,noexec,relatime,cpuacct)
blkio on /sys/fs/cgroup/blkio type cgroup (ro,nosuid,nodev,noexec,relatime,blkio)
memory on /sys/fs/cgroup/memory type cgroup (ro,nosuid,nodev,noexec,relatime,memory)
devices on /sys/fs/cgroup/devices type cgroup (ro,nosuid,nodev,noexec,relatime,devices)
freezer on /sys/fs/cgroup/freezer type cgroup (ro,nosuid,nodev,noexec,relatime,freezer)
net_cls on /sys/fs/cgroup/net_cls type cgroup (ro,nosuid,nodev,noexec,relatime,net_cls)
perf_event on /sys/fs/cgroup/perf_event type cgroup (ro,nosuid,nodev,noexec,relatime,perf_event)
net_prio on /sys/fs/cgroup/net_prio type cgroup (ro,nosuid,nodev,noexec,relatime,net_prio)
hugetlb on /sys/fs/cgroup/hugetlb type cgroup (ro,nosuid,nodev,noexec,relatime,hugetlb)
pids on /sys/fs/cgroup/pids type cgroup (ro,nosuid,nodev,noexec,relatime,pids)
rdma on /sys/fs/cgroup/rdma type cgroup (ro,nosuid,nodev,noexec,relatime,rdma)
misc on /sys/fs/cgroup/misc type cgroup (ro,nosuid,nodev,noexec,relatime,misc)
cgroup on /sys/fs/cgroup/systemd type cgroup (ro,nosuid,nodev,noexec,relatime,name=systemd)
mqueue on /dev/mqueue type mqueue (rw,nosuid,nodev,noexec,relatime)
shm on /dev/shm type tmpfs (rw,nosuid,nodev,noexec,relatime,size=65536k)
/dev/sdd on /etc/resolv.conf type ext4 (rw,relatime,discard,errors=remount-ro,data=ordered)
/dev/sdd on /etc/hostname type ext4 (rw,relatime,discard,errors=remount-ro,data=ordered)
/dev/sdd on /etc/hosts type ext4 (rw,relatime,discard,errors=remount-ro,data=ordered)
devpts on /dev/console type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=666)
proc on /proc/bus type proc (ro,nosuid,nodev,noexec,relatime)
proc on /proc/fs type proc (ro,nosuid,nodev,noexec,relatime)
proc on /proc/irq type proc (ro,nosuid,nodev,noexec,relatime)
proc on /proc/sys type proc (ro,nosuid,nodev,noexec,relatime)
tmpfs on /proc/acpi type tmpfs (ro,relatime)
tmpfs on /proc/kcore type tmpfs (rw,nosuid,size=65536k,mode=755)
tmpfs on /proc/keys type tmpfs (rw,nosuid,size=65536k,mode=755)
tmpfs on /proc/timer_list type tmpfs (rw,nosuid,size=65536k,mode=755)
tmpfs on /sys/firmware type tmpfs (ro,relatime)
/ #
```

`busybox` 镜像虽然小巧，但包括了大量常见的 `Linux` 命令，读者可以用它快速熟悉 `Linux` 命令。

![](https://cdn.isharkfly.com/com-isharkfly-www/discourse-uploads/original/2X/8/860aea77b579cc4581ba7cbfea17889048954556.png)

随着官方对 Docker 容器切换的情况来看，Busybox 对大部分使用 Docker 的人来说可能用不上。

基本上了解下即可。

## 相关资源

* `Busybox` 官网：https://busybox.net/
* `Busybox` 官方仓库：https://git.busybox.net/busybox/
* `Busybox` 官方镜像：https://hub.docker.com/_/busybox/
* `Busybox` 官方仓库：https://github.com/docker-library/busybox

---
https://www.isharkfly.com/t/docker-busybox/15734