---
title: Docker使用总结
date: 2015/10/26
tags: 
- Docker
categories: 
- Docker
---

[toc]

---

## 1.[安装(基于ubuntu)](http://docs.docker.com/linux/step_one/)


**1.安装wget**

```
sudo apt-get update
sudo apt-get install wget
```

**2.安装Docker软件包**

+ 从Docker官网下载

```
wget -qO- https://get.docker.com/ | sh
```

+ 从DaoCloud下载

```
curl -sSL https://get.daocloud.io/docker | sh
```

---
 
## 2.使用Docker Hub Mirror

**简介**

> Mirror 是 Docker Registry 的一种特殊类型，它起到了类似代理服务器的缓存角色，在用户和 Docker Hub 之间做镜像的缓存。这个功能的设计目的是为了企业客户访问 Docker Hub 时降低网络开销。

**使用DaoCloud加速器2.0**

+ [免费注册](https://account.daocloud.io/signup?invite_code=pfkx67jvijuf16g9akki)

+ 安装加速器

运行安装命令（Docker ToolBox下可以使用 docker-machine ssh default 进入终端，boot2docker 可以使用 boot2docker ssh）

```
curl -sSL https://get.daocloud.io/daomonit/install.sh | sh -s 89740b95f9100e3fd8d7ca5c9634166d87dfdf20
```

+ 卸载加速器

可以通过运行 `dpkg -r daomonit` 卸载主机监控程序。( Centos 通过  `rpm -e daomonit` 卸载，Docker ToobBox 通过 `docker rm -f daomonit` 卸载)

---

## 3.[常用命令](https://docs.docker.com/reference/commandline/cli/)

|命令|使用场景|
|-|-|
|**A**|*|
|docker **attach** < container >|与运行中的容器**交互**|
|**B**|*|
|docker **build** [ options ] < new image name > < Dockerfile position >|**构建**镜像|
|**C**|*|
|docker **commit** < current job > < new image name >|将**容器状态保存**为镜像|
|docker **cp** < container:path > < hostpath >|从容器内**复制文件**到指定的路径|
|docker create <br/> [ options ] < image >|在指定镜像上创建一个**读写层**|
|**D**|*|
|docker **diff** < container >|查看容器内发生**变化**的文件和目录|
|**E**|*|
|docker **export** < image >|用于将容器的系统文件**打包**成tar文件|
|docker **events**|打印指定时间内的容器的**实时系统事件**|
|**H**|*|
|docker **help** < cmd >|查看和指定命令相关的**帮助**|
|docker **history** < image name >|查看镜像的**历史**|
|**I**|*|
|docker **images**|**显示**当前本地所有镜像|
|docker **import** < path >|**导入**远程文件、本地文件和目录|
|docker **info**|*|
|docker **inspect** < container/image >|收集有关容器和镜像的**底层信息**，包括容器实例的IP地址，端口绑定列表，特定端口映射的搜索，收集配置的详细信息|
|**K**|*|
|docker **kill** [ options ] < container >|发送SIGKILL信号来**停止容器的主进程**|
|**L**|*|
|docker **load** < *.tar >|从tar文件中**载入镜像**或仓库到STDIN|
|docker **login** [ options ] < server >|**登录**到Docker registry服务器|
|docker **logs** < imgae name >|查看指定镜像的**日志**|
|**P**|*|
|docker **pull** < docker hub namespace/image name >|**拉取**指定镜像|
|docker **ps**|查看当前**正在运行**的容器|
|docker **push** < image name >|**推送**指定镜像|
|**R**|*|
|docker **restart** < container name \| container id >|**重启**指定容器|
|docker **rm** < container name \| container id >|**删除**指定容器|
|docker **rmi** [ -f ] < image name \| image id >|**删除**指定镜像|
|docker **run** < image name >|**运行**指定镜像|
|**S**|*|
|docker **save** < image >|**保存镜像**到tar文件中,并发送到STDOUT|
|docker **search** < image name \| repository name >|**搜索**镜像|
|docker **start** < container name \| container id >|**启动**指定容器|
|docker **stop** < container name \| container id >|**停止**指定容器|
|**T**|*|
|docker **tag** < image id > < docker hub namespace/image name:version label or tag >|设置镜像**标签**|
|**W**|*|
|docker **wait** < image >|**阻塞**对指定容器的其它调用方法，直到容器停止后退出阻塞|

---

## 4.Docker镜像构建

### 4.1 [Dockerfile语法](https://docs.docker.com/reference/builder/)

|关键字|使用场景|注意点|
|-|-|-|
|**ADD** <br/> < src > < des >|**复制文件**指令。它有两个参数<source>和<destination>。destination是容器内的路径。source可以是URL或者是启动配置上下文中的一个文件|官方推荐用 COPY ，源文件可以是 url 或 tar 包，当源文件为 tar 包时会自动 untar |
|**COPY** <br/> < src > < des >|**复制文件**到容器中|官方推荐|
|**CMD** <br/> [ "exec","p1","p2" ]  **CMD** [ "p1","p2" ]  **CMD** cmd p1 p2|容器运行时默认调用的**启动命令**，提供了容器默认的执行命令|Dockerfile只允许使用一次CMD指令，使用多个CMD会抵消之前所有的指令，只有最后一个指令生效|
|**EXPOSE** <br/> < hostport:contport >|指定容器在运行时监听的**端口**|*|
|**ENTRYPOINT**  ["exec","p1","p2"]  **ENTRYPOINT** <br/> cmd p1 p2|配置给容器一个可执行的命令，这意味着在每次使用镜像创建容器时一个特定的应用程序可以被设置为**默认程序**。同时也意味着该镜像每次被调用时仅能运行指定的应用。|类似于CMD，Docker只允许一个ENTRYPOINT，多个ENTRYPOINT会抵消之前所有的指令，只执行最后的ENTRYPOINT指令|
|**ENV** <br/> < key > < value >|设置**环境变量**。它们使用键值对，增加运行程序的灵活性|*|
|**FROM** < image >|指定最底层**镜像**|*|
|**MAINTAINER** <br/> < author name >|说明镜像**作者**|*|
|**RUN** < cmd > |在shell或者exec的环境下执行的**命令**|RUN指令会在新创建的镜像上添加新的层面，接下来提交的结果用在Dockerfile的下一条指令中|
|**USER** < uid >| 指定容器运行时**身份**，镜像正在运行时设置一个 UID |*|
|**VOLUME** < path >| 授权访问从容器内到主机上的目录，即为容器指定**挂载数据卷**|*|
|**WORKDIR** <br/> < dirpath > |指定 RUN、CMD 与 ENTRYPOINT 命令的**工作目录**|*|

### 4.2 示例

+ wdcxc/hexo:base

```
#Hexo Docker Image 
#image:wdcxc/hexo
FROM debian:stable
MAINTAINER wdcxc<904342189@qq.com>
#install
RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup | bash 
RUN apt-get update && apt-get install -y nodejs && npm install -g hexo
#configure
RUN mkdir -p /usr/local/hexo && cd /usr/local/hexo && hexo init && npm install
#run
EXPOSE 4000:4000
WORKDIR /usr/local/hexo/

```

---

## 5.注意点

+ Docker只支持64位平台 

+ 程序运行完成之后，容器不会被销毁，但是状态为 Exited。此外对于以交互模式启动的容器可以先按下 Ctrl+P 然后按下 Ctrl+Q 这样的按键顺序脱离（detach）一个容器，脱离后的容器状态仍为 Up 并且程序会继续在后台运行，这时可以使用 attach 命令重新附到一个已经脱离的程序

+ 如果要删除所有容器 docker rm $(docker ps -q -a)

+ 要注意的一点：容器被删除后里面的数据会被删除，因此要注意挂载数据卷使数据持久化

+ 不要在构建中升级版本
更新将发生在基础镜像里，你不需要在你的容器内来apt-get upgrade更新。因为在隔离情况下，如果更新时试图修改 init 或改变容器内的设备，更新可能会经常失败。它还可能会产生不一致的镜像，因为你不再有你的应用程序该如何运行以及包含在镜像中依赖的哪种版本的正确源文件。

+ 构建镜像时文件名必须为Dockerfile，构建相关文件最好都放在同一目录下

---

## 6.参考资料

+ [Docker Get Started](https://docs.docker.com/mac/started/)

+ [关于DaoCloud](http://help.daocloud.io/index.html)

+ [Docker 新手入门 30 min](http://help.daocloud.io/tutorials/index.html)

+ [Docker官网](http://www.docker.com/)

+ [Docker Docs](https://docs.docker.com/)

+ [Write a volume plugin](https://docs.docker.com/extend/plugins_volume/)

+ [Dockerfile reference](https://docs.docker.com/reference/builder/)

