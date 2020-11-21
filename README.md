# CWIKIUS  Docker 文档和手册

欢迎来到 CWIKIUS Docker 文档和手册的空间

本文档的编译发布版本访问地址：[docker-docs.ossez.com](https://docker-docs.ossez.com)

CWIKIUS 的有关 Docker 相关文档：[https://www.cwiki.us/display/DockerZH/Docker](https://www.cwiki.us/display/DockerZH/Docker)

GitHub 上有关 CWIKIUS Docker 的项目的源代码文件：[https://github.com/cwiki-us-docs/docker-docs](https://github.com/cwiki-us-docs/docker-docs)

如果您有兴趣参与我们的小组和项目，请使用下面的联系方式和我们联系：

| 联系方式名称  | 联系方式  |
|---|---|
| 电子邮件  | [service@ossez.com](mailto:service@ossez.com)  |
| QQ 或微信  | 103899765  |
| QQ 交流群 Spring | 15186112 |
| 社区论坛 | [https://www.ossez.com/c/Toolkit-Algorithm-Computer-Science/system-and-container/25](https://www.ossez.com/c/Toolkit-Algorithm-Computer-Science/system-and-container/25) |

## 微信及公众平台
我们建议您通过社区论坛来和我们进行沟通，请关注我们的微信公众号。

![](https://cdn.ossez.com/img/cwikius/cwikius-qr-wechat-search-w400.png)

## CWIKIUS 文档和手册快速导航
有关相关文档和我们参考过的一些内容的快速导航。

| 网站地址  | 网站链接  |
|---|---|
| CWIKIUS Docker Docs 在线文档  | https://docker-docs.ossez.com |
| CWIKI.US 空间  | https://www.cwiki.us/display/DockerZH/Docker  |
| Docker 官方文档 | https://docs.docker.com/ |
| chinese_docker | https://github.com/widuu/chinese_docker |
| daocloud.io | https://guide.daocloud.io/#all-updates |

欢迎来到 Docker 文档的代码仓库。本代码仓库是文档 https://docs.docker.com 的源代码。

如果你发现这个文档有任何问题，Docker 官方欢迎你来创建 合并请求（Pull Requests）。Docker 的文档是完全开源的，Docker 官方也非常感谢社区对 Docker 的贡献。

## 提供反馈

Docker 的官方和 CWIKIUS 都非常欢迎您对我们的内容进行反馈，并且我们将这个提供反馈的方法进行了调整，以便于更好的进行访问和提交。你可以对页面进行编辑或者针对 https://docs.docker.com 上每一个页面的右上角提供的链接来对内容进行编辑和提交合并请求。

你也可以对每一个页面来进行评分，评分的链接在页面的页脚。

**本仓库只针对文档的内容进行修改。** 如果你考虑对文档进行修改的话，在提交 PR 之前你应该先考虑下这个问题应该是和文档相关的，比如说文档描述的不清楚，文档出现了错误，或者在文档让用户非常困惑等。

* 如果你在使用 Docker 的时候遇到了问题，请访问 https://forums.docker.com 论坛中的内容。
* 如果针对 Docker 的新功能和特性有什么更好的建议或者你找到了 Docker 的一个 bug，请使用 Docker 的代码仓库来提交你的问题。

## 贡献

我们非常重视你对文档的贡献，我们也希望能够尽可能的在文档仓库中间的的工作。

在你决定对文档进行贡献的时候，你需要首先确定你希望工作的分支。如果你在这个上面有什么困惑的话，你只需要向我们提问即可，官方和我们都会尽可能的帮助你。

如果官方的开放人员或者其他人发现了你可能提交了错误的分支，将会有人提醒你的，这个时候你只需要 rebase 你的工作就可以了。

> **Note**: 希望对 Docker 的开发贡献你自己的力量？请参考下面文档的内容：[Contribution guidelines](CONTRIBUTING.md)。

### 不需要在这里编辑的文件

文件或者目录列在为 

[`.NOT_EDITED_HERE.yaml`](.NOT_EDITED_HERE.yaml) 

关键字的路径被其他仓库使用的是不应该进行编辑的。

对上面字符串进行编辑后提交的 PR 请求会被驳回（rejected），请确定你编辑的仓库中的文件和路径是正确的。

### 文档改善计划概述

合并请求（PR）应该是针对 `master` 分支提出的，这个内容包括有：

* 不针对新特性的概念性的内容和基于任务的信息
* 重新格式化或者重写部分内容
* 文档错误的修改
* 拼写或者语法错误

> 你是否享受创建一些图形呢？好看漂亮的图形和设计是一个好文档的关键，我们尤其欢迎您在这个方面的贡献和帮助。

## GitHub 提交 合并请求（PR） 之前的预存（staging ）

针对提交到 `master` 分支的每一次合并请求，一个针对站点使用 Netlify 的预存 staging 将会被创建。

如果站点被重构创建，将会看到 **deploy/netlify — Deploy preview ready**** 文字。

否则的话，你将会看到一个错误信息，单击 **Details** 来查看暂存的站点或者阻止站点重构的错误。重新查看暂存的站点来确定是不是你提交的内容导致的错误。

在 PR 合并到 master 分支之前，其他的项目相关人员同时也会查看暂存的站点。通过这个选项，我们来保护 https://docs.docker.com 站点不会有错误。

## 在本地构建和查看文档

在你的本地计算机上，克隆这个仓库：

```bash
git clone --recursive https://github.com/cwiki-us-docs/docker-docs.git
cd docker-docs
```

然后使用 Docker Compose 来运行和构建这个文档，Docker Compose 的访问链接为：https://docs.docker.com/compose

```bash
docker-compose up -d --build
```

> Docker Compose 包含有 [Docker Desktop](https://docs.docker.com/desktop)。
> 如果你的计算机上没有安装 Docker Compose，请访问下面的链接上的参考来进行安装：https://docs.docker.com/compose/install/。

一旦容器被构建和运行了，请通过浏览器来访问 [http://localhost:4000](http://localhost:4000]地址来查看构建成功的文档页面。

当你对文档进行了新的修改后，你可以再次运行 *docker-compose up* 命令。这个命令将会重新构建文档，并且将你的容器进行更新。

```bash
docker-compose up -d --build
```

一旦容器被构建和运行了，请通过浏览器来访问 [http://localhost:4000](http://localhost:4000]地址来查看构建成功的文档页面。


如果你想停止预存（staging）的容器，请使用  *docker-compose down* 命令

```bash
docker-compose down
```

### 启用文档的部署特性

在默认的本地构建文档中，我们禁用了一些特性来缩短文档的构建时间。在针对 [docs.docker.com](https://docs.docker.com) 网站中部署的文档和本地构建的文档有下面的一些配置不同：

- 使用 `js/metadata.json` 的自动搜索完成
- google analytics 配置
- 页面评分配置（page ratings）
-  创建站点地图 `sitemap.xml`
- 样式表的压缩和小型化（css/style.css）
- 针对内容在其他仓库中的 "编辑页面（edit this page）" 页面的链接

如果你对上面的内容进行了修改的话，你可以在你的本地使用 "服务器（Production）" 构建。

为了能够预览针对服务器的部署环境的特性是否被启用了，你需要在对你的文档进行构建的时候设置 `JEKYLL_ENV` 环境变量。

```bash
JEKYLL_ENV=production docker-compose up --build
```

当构建完成后，请访 [http://localhost:4000](http://localhost:4000) 地址中的内容来确定构建的正确。

如果你对文档进行了修改，并且需要重新构建的话，你需要重复上面的步骤。

<!--
TODO re-enable auto-builds, or push master builds to Docker hub
## Read these docs offline

To read the docs offline, you can use either a standalone container or a swarm service.
To see all available tags, go to [Docker Hub](https://docs.docker.com/docker-hub/).

The following examples use the `latest` tag:

- Run a single container:

  ```bash
  docker run  -it -p 4000:4000 docs/docker.github.io:latest
  ```

- Run a swarm service:

  ```bash
  docker service create -p 4000:4000 --name localdocs --replicas 1 docs/docker.github.io:latest
  ```

  This example uses only a single replica, but you could run as many replicas as you'd like.

Either way, you can now access the docs at port 4000 on your Docker host.
-->

## 重要的文件

- `/_data/toc.yaml` 定义了文档的左侧导航
- `/js/docs.js` 定义了文档使用的主要 JS 文本，例如 TOC 创建，菜单同步等
- `/css/style.scss` 定义了文档使用的主要样式表规则
- `/_layouts/docs.html` 为 HTML 的模板文件，包括定义了 header 和 footer，同时也包括了所有文档内容需要使用的 JS/CSS

## GitHub 查看的相关链接

你可以自由的链接到 `../foo.md` 文件，这样的话这个文本就可以在 GitHub 上进行阅读了，但是需要注意的是 Jekyll 模板将会通知templating notation
`{% such as this %}` 将会被读成原始文档，而不会被处理。因此最好的办法就是访问官方 [https://docs.docker.com/](https://docs.docker.com/) 文档链接来进行阅读文档。

### 测试修改和实践指南

如果你希望对修改的样式表进行测试，或者你希望对 Markdown， Bootstrap， JQuery 或者其他的一些内容进行测试的话，请参考 `test.md` 中的内容（访问路径为 `/test/`）。

### 预页面字体格式

字体格式将会告诉页面在 Markdown 文件的最上端，使用 3 个横线作为开始和结束。其中包括有 YAML 内容，下面为可以支持的关键字，包括有表头，描述和关键字是否是必须的。

| 关键字                    | 是否必须  | 描述                             |
|------------------------|-----------|-----------------------------------------|
| title                  | 是       | 这个字段定义的是页面的标题，将会添加到 HTML 输出中的 `<h1>` 级别的头部。 |
| description            | 是       | 一个描述页面内容的例子，将会添加到 HTML 的 metadata 上面。 |
| keywords               | 是       | 一个使用逗号分隔符的关键字列表，将会添加到 HTML 的 metadata 上面。 |
| redirect_from          | 否       | 一个 YAML 的列表，这个将会显示链接到当前页面的的所有页面列表。在页面处理的过程中，这个地方配置的页面内容，将会为那些页面创建一个 302 重定向链接到这个页面上。 |
| notoc                  | 否       | 可以使用 `true` 或者 `false`。如果选择 `true` 的话， TOC 将不会在 HTML 输出的时候创建。默认的配置选项是 `false`。针对没有页面头部内容，将会创建相同的显示页面。|
| toc_min                | 否       | 如果 `notoc` 设置为 `true` 的话，这个选项将会被忽略。包括在页面 TOC 中头部，最小的页面级别为。默认配置为 `2`， 意思是显示页面头部最小的开始为 `<h2>`。 |
| toc_max                | 否       | 如果 `notoc` 设置为 `false` 的话，这个选项将会被忽略。包括在页面 TOC 中头部，最大的页面级别为。默认配置为 `3`， 意思是显示页面头部最小的开始为 `<h3>`。如果这个设置和 `toc_min` 相同的话，那么只有 `toc_min` 的级别标题被显示。 |
| no_ratings             | 否       | 可以使用 `true` 或者 `false`。设置是否为页面设置投票，如果设置为 `true` 的话，页面将不会显示投票。默认为 `false`。 |
| skip_read_time         | 否       | 设置 `true` 的话，将不会在页面中设置页面的估计阅读时间。 |
| sitemap                | 否       | 通知这个页面将不会被搜索引擎进行索引，当设置为 `false` 的时候，这个页面将会从 `sitemap.xml` 中进行剔除，并且在页面的头部（header）将会添加 `<meta name="robots" content="noindex"/>` 这个内容。 |

下面显示的内容是一个有效的页面 Metadata 配置（没有转换为 HTML）页面。在预页面格式中内容的顺序是没有关系的，你可以随意调整上面参数的顺序。

```liquid
---
description: Instructions for installing Docker on Ubuntu
keywords: requirements, apt, installation, ubuntu, install, uninstall, upgrade, update
redirect_from:
- /engine/installation/ubuntulinux/
- /installation/ubuntulinux/
- /engine/installation/linux/ubuntulinux/
title: Get Docker for Ubuntu
toc_min: 1
toc_max: 6
skip_read_time: true
no_ratings: true
---
```

### 创建标签（Tab）页

为了在页面中使用标签页，例如测试页面中的标签页：https://docker.ossez.com/test/，这个需要使用 HTML 文件。The use of tabs, as on pages like [https://docs.docker.com/engine/api/](/engine/api/), requires

标签页使用的是 Bootstrap CSS/JS，因此请参考相关的文档来获得有关标签页使用的更多有关内容和信息。针对标准的水平标签页，你可以拷贝和粘贴下面的表单内容，在上面的表单内容中关键的地方在 `href="#id"` 和 `id="id"`。

这个需要和你的标签页配置进行对应。以便于添加和删除标签页。

```html
<ul class="nav nav-tabs">
  <li class="active"><a data-toggle="tab" data-target="#tab1">TAB 1 HEADER</a></li>
  <li><a data-toggle="tab" data-target="#tab2">TAB 2 HEADER</a></li>
</ul>
<div class="tab-content">
  <div id="tab1" class="tab-pane fade in active">TAB 1 CONTENT</div>
  <div id="tab2" class="tab-pane fade">TAB 2 CONTENT</div>
</div>
```

有关更多标签页的内容，请参考 `test.md` 页面中的内容。

### 运行页面中的 Javascript

如果你需要在页面中运行自定义的 Javascript 脚本，这个是需要基于 JQuery 和 Bootstrap 来进行运行的。

请确定 `<script>` 标记存储在页面的最后（在所有页面都被载入完成以后）。这是因为，如果你的脚本在页面之前的话，很有肯能导致你的页面在 JQuery 和 Bootstrap JS 载入完成之前运行，这会导致脚本错误。

> **Note**: 通常来说这个是一个糟糕的决定。

### 图片

不要忘记删除所有不需要的图片，将图片保存在 images/ 目录中，这个目录为通常我们保存图片的路径。

通常的，这个文件夹中的图片文件是按照图片文件名的字母进行排和分组的。例如，相对命名方式来说 `settings-file-share.png` 和 `settings-proxies.png` 针对  `file-share-settings.png` 和 `proxies-settings.png` 来说就更好了。

你还可以添加数字，尤其你是针对图片有使用和显示顺序的情况下。例如，`run-only-the-images-you-trust-1.svg`，`run-only-the-images-you-trust-2.png`， `run-only-the-images-you-trust-3.png` 等。

在可能的情况下，对需要的内容进行截图，并且避免对整个桌面进行截图，这样避免一些重要的配置信息被泄漏也能够为编辑节约不少的编辑时间。

在 Mac 的计算机中，请对创建进行截图而且不要保存为阴影。你可以使用下面的方法进行操作：当你按下 `Command-Shift-4` 后，单击选项，来进行禁用 。

如果你想全局进行禁用，请运行下面的脚本：

```bash
$ defaults write com.apple.screencapture disable-shadow -bool TRUE
$ killall SystemUIServer  # restart it.
```

在后面，你可以通过设置 `-bool FALSE` 来重新启用阴影。

为了保持我们的 Git 仓库不至于过大，请尽量对图片进压缩。在 Mac 的计算中，你也许可以使用 https://imageoptim.com 来对图片进行压缩。

请对图片进行压缩之后，才上传图片到 Git 的仓库中。如果你在这个之前操作的话，你可能还是增加了 Git 仓库的内容，但是针对网络传输方面的内容进行了优化。

## 版权和许可证

Copyright 2013-2020 Docker, inc, 文件的发布是基于 Apache 2.0 license 下进行发布。

中文版本的翻译和维护由 CWIKIUS 进行。我们允许在非商业的情况下自由扩散分发，并保留适当的权利。您可以对我们的作品进行演绎，但需要保留版权信息和来源。

本中文版本请参考：https://docker.ossez.com/ 页面中的编译部署内容和 https://docker-docs.ossez.com/ 基于 MD 的编译版本。