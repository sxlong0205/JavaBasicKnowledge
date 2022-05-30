# Docker 安装

## 前提说明

### CentOS Docker 安装

Docker 并非是一个通用的容器工具，它依赖于已存在并运行的 Linux 内核环境。

Docker 实质上是在已经运行的 Linux 下制造了一个隔离的文件环境，因此它执行的效率几乎等同于所部属的 Linux 主机。

因此，Docker 必须部署在 Linux 内核的系统上，如果其他系统想要部署 Docker 就必须安装一个虚拟 Linux 环境。

<img src="img/Image-20220530162106232.png" alt="Image-20220530162106232" style="zoom:67%;" />

在 Windows 上部署 Docker 的方法都是先安装一个虚拟机，并在安装 Linux 系统的虚拟机中运行 Docker。

### 前提条件

目前，CentOS 仅发行版本中的内核支持 Docker。Docker 运行在CentOS 7（64-bit）上， 要求系统为64位、Linux系统内核版本为 3.8以上，这里选用Centos7.x。

### 查看自己的内核

uname 命令用于打印当前系统相关信息（内核版本号、硬件架构、主机名称和操作系统类型等）。 

![Image-20220530163018106](img/Image-20220530163018106.png)

## Docker 的基本组成

### 镜像（Image）

Docker 镜像（Image）就是一个 **只读** 的模板。镜像可以用来创建 Docker 容器，一个镜像可以创建很多容器。 它也相当于是一个 root 文件系统。比如官方镜像 Centos:7 就包含了完整的一套 Centos:7 最小系统的 root 文件系统。 相当于容器的"源代码"，Docker 镜像文件类似于 Java 的类模板，而 Docker 容器实例类似于 Java 中 new 出来的实例对象。 

### 容器（Container）

1.   从面向对象角度 

     Docker 利用容器（Container）独立运行的一个或一组应用，应用程序或服务运行在容器里面，容器就类似于一个虚拟化的运行环境，容器是用镜像创建的运行实例。就像是 Java 中的类和实例对象一样，镜像是静态的定义，容器是镜像运行时的实体。容器为镜像提供了一个标准的和隔离的运行环境，它可以被启动、开始、停止、删除。每个容器都是相互隔离的、保证安全的平台。 

2.   从镜像容器角度 

     **可以把容器看做是一个简易版的** Linux **环境** （包括 root 用户权限、进程空间、用户空间和网络空间等）和运行在其中的应用程序。 

### 仓库（Repository）

仓库（Repository）是集中存放镜像文件的场所。  

类似于 

-   Maven仓库，存放各种 jar包的地方； 
-   GitHub 仓库，存放各种 git 项目的地方； 
-   Docker 公司提供的官方 Registry 被称为 Docker Hub，存放各种镜像模板的地方。 

仓库分为公开仓库（Public）和私有仓库（Private）两种形式。 

最大的公开仓库是 Docker Hub（https://hub.docker.com/）， 存放了数量庞大的镜像供用户下载。国内的公开仓库包括阿里云、网易云等。

### 总结

需要正确的理解仓库/镜像/容器这几个概念: 

Docker 本身是一个容器运行载体或称之为管理引擎。我们把应用程序和配置依赖打包好形成一个可交付的运行环境，这个打包好的运行环境就是 Image 镜像文件。只有通过这个镜像文件才能生成Docker容器实例(类似 Java 中 new 出来一个对象)。  

Image文件可以看作是容器的模板。Docker 根据 Image 文件生成容器的实例。同一个 Image 文件，可以生成多个同时运行的容器实例。 

镜像文件 

-   Image 文件生成的容器实例，本身也是一个文件，称为镜像文件。 

容器实例 

-   一个容器运行一种服务，当我们需要的时候，就可以通过 Docker 客户端创建一个对应的运行实例，也就是我们的容器 

仓库。

-   就是放一堆镜像的地方，我们可以把镜像发布到仓库中，需要的时候再从仓库中拉下来就可以了。 

 <img src="img/image-20220530165141014.png" alt="image-20220530165141014" style="zoom:67%;" />

Docker 是一个 Client-Server 结构的系统，Docker 守护进程运行在主机上，然后通过 Socket 连接从客户端访问，守护进程从客户端接受命令并管理运行在主机上的容器。容器，是一个运行时环境，就是我们前面说到的集装箱。

<img src="img/image-20220530165310908.png" alt="image-20220530165310908" style="zoom:67%;" />

## Docker 平台架构图解

Docker 是一个 C/S 模式的架构，后端是一个松耦合架构，众多模块各司其职。

1.   用户是使用 Docker Client 与 Docker Daemon 建立通信，并发送请求给后者。
2.   Docker Daemon 作为 Docker 架构中的主体部分，首先提供 Docker 架构中的主体部分，首先提供 Docker Server 的功能使其可以接受 Docker Client 的请求。
3.   Docker Engine 执行 Docker 内部的一系列工作，每一项工作都是以一个 Job 的形式的存在。
4.   Job 的运行过程中，当需要容器镜像时，则从 Docker Registry 中下载镜像，并通过镜像管理驱动 Graph Driver 将下载镜像以 Graph 的形式存储。
5.   当需要为 Docker 创建网络环境时，通过网络管理驱动 Network Driver 创建并配置 Docker 容器网络环境。
6.   当需要限制 Docker 容器运行资源或执行用户指令等操作时，则通过 Exec Driver 来完成。
7.   Libcontainer 是一项独立的容器管理包，Network Driver 以及 Exec Driver 都是通过 Libcontainer 来实现具体对容器进行的操作。

![image-20220530171234139](img/image-20220530171234139.png)

## 安装步骤

官网文档：https://docs.docker.com/engine/install/

## 阿里云镜像加速

### 是什么

https://promotion.aliyun.com/ntms/act/kubernetes.html

### 注册一个属于自己的阿里云账户（可复用淘宝账号）

![image-20220530172846326](img/image-20220530172846326.png)

![image-20220530173107104](img/image-20220530173107104.png)

![image-20220530173314487](img/image-20220530173314487.png)

### 获得加速器地址连接

![image-20220530173314487](img/image-20220530173314487.png)

### 粘贴脚本直接执行

![image-20220530173239414](img/image-20220530173239414.png)

### 重启服务器

```shell
systemctl daemon-reload
systemctl restart docker
```

## 永远的 Hello World

![image-20220530173539941](img/image-20220530173539941.png)

￼￼![image-20220530173610014](img/image-20220530173610014.png)

## 底层原理

为什么 Docker 会比 VM 虚拟机快？

1.   Docker 有着比虚拟机更少的抽象层。

     由于 Docker 不需要 Hypervisor（虚拟机）实现硬件资源虚拟化,运行在 Docker 容器上的程序直接使用的都是实际物理机的硬件资源。因此在 CPU、内存利用率上 Docker 将会在效率上有明显优势。 

2.   Docker 利用的是宿主机的内核,而不需要加载操作系统 OS 内核 

     当新建一个容器时，Docker 不需要和虚拟机一样重新加载一个操作系统内核。进而避免引寻、加载操作系统内核返回等比较费时费资源的过程，当新建一个虚拟机时，虚拟机软件需要加载 OS，返回新建过程是分钟级别的。而 Docker 由于直接利用宿主机的操作系统，则省略了返回过程，因此新建一个 Docker 容器只需要几秒钟。 