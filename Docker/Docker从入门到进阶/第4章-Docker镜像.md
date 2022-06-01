# Docker 镜像

## 是什么

### 是什么

镜像是一种轻量级、可执行的独立软件包，它包含运行某个软件所需的所有内容，我们把应用程序和配置依赖打包好形成一个可交付的运行环境（包括代码、运行时需要的库、环境变量和配置文件等），这个打包好的运行环境就是 image 镜像文件。只有通过这个镜像文件才能生成 Docker 容器实例（类似 Java 中 new 出来一个对象）。

### 分层的镜像

以我们的 pull 为例，在下载的过程中我们可以看到 Docker 的镜像好像是在一层一层的下载。

### UnionFS（联合文件系统）

UnionFS（联合文件系统）：Union 文件系统（UnionFS）是一种分层、轻量级并且高性能的文件系统，它支持对文件系统的修改作为一次提交来一层层的叠加，同时可以将不同目录挂载到同一个虚拟文件系统下（unite several directories into a single virtual filesystem）。Union 文件系统是 Docker 镜像的基础。镜像可以通过分层来进行继承，基于基础镜像（没有父镜像），可以制作各种具体的应用镜像。

特性：一次同时加载多个文件系统，但从外面看起来，只能看到一个文件系统，联合加载会把各层文件系统叠加起来，这样最终的文件系统包含所有底层的文件和目录。

### Docker 镜像加载原理

Docker 的镜像实际上由一层一层的文件系统组成，这种层级的文件系统 UnionFS。

BootFS（Boot File System）主要包含 BootLoader 和 Kernel，BootLoader 主要是引导加载 Kernel，Linux 刚启动时会加载 BootFS 文件系统，在 Docker 镜像的最底层是引导文件系统 BootFS。这一层与我们典型的 Linux/Unix 系统是一样的，包含 Boot 加载器和内核。当 Boot 加载完成之后整个内核就都在内存中了，此时内存的使用权已由 BootFS 转交给内核，此时系统也会卸载 BootFS。

## 重点理解



## Docker 镜像 commit 操作案例



