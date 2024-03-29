# Docker 简介

## 是什么

### 问题：为什么会有 Docker 出现

环境配置也各有不同。您正在开发的应用依赖于您当前的配置且还要依赖于某些配置文件。此外，您的企业还拥有标准化的测试和生产环境，且具有自身的配置和一系列支持文件。您希望尽可能多在本地模拟这些环境而不产生重新创建服务器环境的开销。请问：您要如何确保应用能够在这些环境中运行和通过质量检测？并且在部署过程中不出现令人头疼的版本、配置问题，也无需重新编写代码和进行故障修复？ 

答案就是使用容器。Docker 之所以发展如此迅速，也是因为它对此给出了一个标准化的解决方案————系统平滑移植，容器虚拟化技术。 

环境配置相当麻烦，换一台机器，就要重来一次，费力费时。很多人想到，能不能从根本上解决问题，软件可以带环境安装？也就是说，安装的时候，把原始环境一模一样地复制过来。开发人员利用 Docker 可以消除协作编码时"在我的机器上可正常工作"的问题。 

￼￼￼￼￼<img src="img/image-20220530155215440.png" alt="image-20220530155215440" style="zoom: 67%;" />

之前在服务器配置一个应用的运行环境，要安装各种软件，就拿尚硅谷电商项目的环境来说，Java/RabbitMQ/MySQL/JDBC 驱动包等。安装和配置这些东西有多麻烦就不说了，它还不能跨平台。假如我们是在 Windows 上安装的这些环境，到了 Linux 又得重新装。况且就算不跨操作系统，换另一台同样操作系统的服务器，要 **移植** 应用也是非常麻烦的。 

传统上认为，软件编码开发/测试结束后，所产出的成果即是程序或是能够编译执行的二进制字节码等(Java 为例)。而为了让这些程序可以顺利执行，开发团队也得准备完整的部署文件，让维运团队得以部署应用程式，开发需要清楚的告诉运维部署团队，用的全部配置文件+所有软件环境。不过，即便如此，仍然常常发生部署失败的状况 。Docker 的出现 使得 Docker 得以打破过去「程序即应用」的观念。透过镜像(images)将作业系统核心除外，运作应用程式所需要的系统环境，由下而上打包，达到应用程式跨平台间的无缝接轨运作。

### Docker 理念

Docker 是基于 Go 语言实现的云开源项目。 

Docker 的主要目标是"Build，Ship and Run Any App, Anywhere"，也就是通过对应用组件的封装、分发、部署、运行等生命周期的管理，使用户的 APP（可以是一个WEB应用或数据库应用等等）及其运行环境能够做到"一次镜像，处处运行"。 

￼￼￼￼￼￼￼<img src="img/image-20220530160024394.png" alt="image-20220530160024394" style="zoom:67%;" />

Linux 容器技术的出现就解决了这样一个问题，而 Docker 就是在它的基础上发展过来的。将应用打成镜像，通过镜像成为运行在 Docker 容器上面的实例，而 Docker 容器在任何操作系统上都是一致的，这就实现了跨平台、跨服务器。只需要一次配置好环境，换到别的机子上就可以一键部署好，大大简化了操作。 

### 一句话

解决了运行环境和配置问题的软件容器，方便做持续集成并有助于整体发布的容器虚拟化技术。

## 容器与虚拟机比较

### 容器发展简史

<img src="img/image-20220530160611462.png" alt="image-20220530160611462" style="zoom:67%;" />

<img src="img/image-20220530160653485.png" alt="image-20220530160653485" style="zoom:67%;" />

### 传统虚拟机技术

虚拟机（virtual machine）就是带环境安装的一种解决方案。 

它可以在一种操作系统里面运行另一种操作系统，比如在 Windows10 系统里面运行 Linux 系统 CentOS7。应用程序对此毫无感知，因为虚拟机看上去跟真实系统一模一样，而对于底层系统来说，虚拟机就是一个普通文件，不需要了就删掉，对其他部分毫无影响。这类虚拟机完美的运行了另一套系统，能够使应用程序，操作系统和硬件三者之间的逻辑不变。 

虚拟机的缺点： 

1.   资源占用多
2.   冗余步骤多
3.   启动慢  

### 容器虚拟化技术

Linux 容器(Linux Containers，缩写为 LXC) 

Linux 容器是与系统其他部分隔离开的一系列进程，从另一个镜像运行，并由该镜像提供支持进程所需的全部文件。容器提供的镜像包含了应用的所有依赖项，因而在从开发到测试再到生产的整个过程中，它都具有可移植性和一致性。 

Linux 容器不是模拟一个完整的操作系统 而是对进程进行隔离。有了容器，就可以将软件运行所需的所有资源打包到一个隔离的容器中。 容器与虚拟机不同，不需要捆绑一整套操作系统，只需要软件工作所需的库资源和设置。系统因此而变得高效轻量并保证部署在任何环境中的软件都能始终如一地运行。 

### 对比

<img src="img/image-20220530161028193.png" alt="image-20220530161028193" style="zoom:67%;" />

比较了 Docker 和传统虚拟化方式的不同之处： 

-   传统虚拟机技术是虚拟出一套硬件后，在其上运行一个完整操作系统，在该系统上再运行所需应用进程。
-   容器内的应用进程直接运行于宿主的内核，容器内没有自己的内核且也没有进行硬件虚拟，因此容器要比传统虚拟机更为轻便。 
-   每个容器之间互相隔离，每个容器有自己的文件系统 ，容器之间进程不会相互影响，能区分计算资源。 

## 去哪下

Docker 官网：http://www.docker.com

Docker Hub 官网: https://hub.docker.com/