# JVM运行时参数

## JVM 参数选项类型

### 类型一：标准参数选项

**特点**

比较稳定，后续版本基本不会变化，以`-`开头。

**各种选项**

运行 Java 或者 `java -help` 可以看到所有的标准选项。

**补充内容：-server 与 -client**

HotSpot JVM 有两种模式，分别是 server 和 client，分别通过 -server 和 -client 模式设置：

1. 在 32 位 Windows 系统上，默认使用 Client 类型的 JVM。要想使用 Server 模式，则机器配置至少有 2 个以上的 CPU 和 2G 以上的物理内存。Client 模式适用于对内存要求较小的桌面应用程序，默认使用 Serial 串行垃圾收集器。
2. 64 位机器上只支持 Server 模式的 JVM，适用于需要大内存的应用程序，默认使用并行垃圾收集器。

关于 Server 和 Client 的官网介绍为：https://docs.oracle.com/javase/8/docs/techontes/guides/vm/server-class.html

### 类型二：-X 参数选项

**特点**

非标准化参数，功能比较稳定，以 `-X` 开头。

**各种选项**

运行 `java -X` 命令可以看到所有的 X 选项。

```
-Xmixed								混合模式执行（默认）
-Xint								仅解释模式执行
-Xcomp								仅采用即时编译器模式
-Xbootclasspath:<用;分隔的目录和 zip/jar 文件>	设置搜索路径以引导类和资源
-Xbootclasspath/a:<用;分隔的目录和 zip/jar 文件>	附加在引导类路径末尾
-Xbootclasspath/p:<用;分隔的目录和 zip/jar 文件>	置于引导类路径之前
-Xdiag								显示附加诊断消息
-Xnoclassgc							禁用类垃圾收集
-Xincgc								启用增量垃圾收集
-Xloggc:<file>						将 GC 状态记录在文件中（带时间戳）
-Xbatch								禁用后台编译
-Xms<size>							设置初始 Java 堆大小
-Xmx<size>							设置最大 Java 堆大小
-Xss<size>							设置 Java 线程堆栈大小
-Xprof								输出 CPU 配置文件数据
-Xfuture							启用最严格的检查，预期将来的默认值
-Xrs								减少 Java/VM 对操作系统信号的使用
-Xcheck:jni							对 JNI 函数执行其他检查
-Xshare:off							不尝试使用共享类数据
-Xshare:auto						在可能的情况下使用共享类数据（默认）
-Xshare:on							要求使用共享类数据，否则将失败
-XshowSettings						显示所有设置并继续
-XshowSettings:all					显示所有设置并继续
-XshowSettings:vm					显示所有与 VM 相关的设置并继续
-XshowSettings:properties			显示所有属性设置并继续
-XshowSettings:locale				显示所有与区域设置相关的设置并继续
```

**JVM 的 JIT 编译模式相关的选项**

- `-Xint`：禁用 JIT，所有字节码都被解释执行，这个模式的速度是最慢的。
- `-Xcomp`：所有字节码第一次使用就都被编译成本地代码，然后再执行。
- `-Xmixed`：混合模式，默认模式，让 JIT 根据程序运行的情况，有选择地将某些代码编译成本地代码

**特别地**

-Xmx -Xms -Xss 属于 XX 参数？

- `-Xms<size>`：设置初始 Java 堆大小，等价于 `-XX:InitialHeapSize`。
- `-Xmx<size>`：设置最大 Java 堆大小，等价于 `-XX:MaxHeapSize`。
- `-Xss<size>`：设置 Java 线程堆栈大小，`-XX:ThreadStackSize`。

### 类型三：-XX 参数选项

**特点**

- 非标准化参数
- 使用的最多的参数类型
- 实验性选项
- 以 `-XX` 开头

**作用**

用于开发和调试 JVM。

**分类**

- Boolean 类型格式
  - `-XX:+<option>` 表示启用 option 属性。
  - `-XX:- <option>` 表示禁用 option 属性。
  - 说明：因为有的指令默认是开启的，所以可以使用 `-` 关闭。
- 非 Boolean 类型模式（key-value 类型）
  - 子类型 1：数值型格式 `-XX:<option>=<number>`。
  - 子类型 2：非数值型格式 `-XX:<name>=<string>`。

**特别地**

- `-XX:+PrintFlagsFinal`
  - 输出所有参数的名称和默认值。
  - 默认不包括 Diagnostic 和 Experimental 的参数。
  - 可以配合 `-XX:+UnlockDiagnosticVMOptions` 和 `-XX:UnlockExperimentalVMOptions` 使用。

## 添加 JVM 参数选项

### Eclipse

### IDEA

### 运行 jar 包

`java -Xms50m -Xmx50m -XX:+PrintGCDetails -XX:+PrintGCTimeStamps -jar demo.jar`

### 通过 Tomcat 运行 war 包

- Linux 系统下可以在 tomcat/bin/catalina.sh 中添加类似如下配置： JAVA_OPTS="-Xms512M -Xmx1024M"。
- Windows 系统下在 catalina.bat 中添加类似如下配置： set "JAVA_OPTS=Xms512M -Xmx1024M"。

### 程序运行过程中

- 使用 jinfo -flag <name>=<value> <pid> 设置非 Boolean 类型参数。
- 使用 jinfo -flag [+ | -] <name> <pid> 设置 Boolean 类型参数。

## 常用的 JVM 参数选项

### 打印设置的 XX 选项及值

- `-XX:+PrintCommandLineFlags`：可以让在程序运行前打印出用户手动设置或者 JVM 自动设置的 XX 选项。
- `-XX:+PrintFlagsInitial`：表示打印所有 XX 选项的默认值。
- `-XX:+PrintFlagsFinal`：表示打印出 XX 选项在运行程序时生效的值。
- `-XX:+PrintVMOptions`：打印 JVM 的参数。

### 堆、栈、方法区等内存大小设置

栈：

- `-Xss128k`
  - 设置每个线程的栈大小为 128k。
  - 等价于 `-XX:ThreadStackSize=128k`。

堆内存：

- `-Xms3550m`：等价于 `-XX:InitialHeapSize`，设置 JVM 初始堆内存为 3550M。
- `-Xmx3550m`：等价于 `-XX:MaxHeapSize`，设置 JVM 最大堆内存为 3550M。
- `-Xmn2g`
  - 设置年轻代大小为 2G。
  - 官方推荐配置为整个堆大小的 3/8。
- `-XX:NewSize=1024m`：设置年轻代初始值为 1024M。
- `-XX:MaxNewSize=1024m`：设置年轻代最大值为 1024M。
- `-XX:SurvivorRatio=8`：设置年轻代中 Eden 区与一个 Survivor 区的比值，默认为 8。
- `-XX:+UseAdaptiveSizePolicy`：自动选择各区大小比例。
- `-XX:NewRatio=4`：设置老年代与年轻代（包括 1 个 Eden 和 2 个 Survivor 区）的比值。
- `-XX:PretenureSizeThreadshold=1024`
  - 设置让大于此阈值的对象直接分配在老年代，单位为字节。
  - 只对 Serial、ParNew 收集器有效。
- `-XX:MaxTenuringThreshold=15`
  - 默认值为 15。
  - 新生代每次 MinorGC 后，还存活的对象年龄 +1，当对象的年龄大于设置的这个值时就进入老年代。
- `-XX:+PrintTenuringDistribution`：让 JVM 在每次 MinorGC 后打印出当前使用的 Survivor 中对象的年龄分布。
- `-XX:TargetSurvivoRatio`：表示 MinorGC 结束后 Survivor 区域中占用空间的期望比例。

方法区：

- 永久代：
  - `-XX:PermSize=256m`：设置永久代初始值为 256M。
  - `-XX:MaxPermSize=256m`：设置永久代最大值为 256M。
- 元空间：
  - `-XX:MetaspaceSize`：初始空间大小。
  - `-XX:MaxMetaspaceSize`：最大空间，默认没有限制。
  - `-XX:+UseCompressedOops`：压缩对象指针。
  - `-XX:CompressedClassSpaceSize`：设置 Class Metaspace 的大小，默认 1G。

直接内存：

- `-XX:MaxDirectMemorySize`：指定 DirectMemory 容量，若未指定，则默认与 Java 堆最大值一样。

### OutOfMemory 相关的选项

- `-XX:+HeapDumpOnOutOfMemoryError`：表示在内存出现 OOM 的时候，把 Heap 转存（Dump）到文件以便后续分析。
- `-XX:+HeapDumpBeforeFullGC`：表示在出现 FullGC 之前，生成 Heap 转储文件。
- `-XX:HeapDumpPath=<path>`：指定 Heap 转存文件的存储路径。
- `-XX:OnOutOfMemoryError`：指定一个可行性程序或者脚本的路径，当发生 OOM 的时候，去执行这个脚本。

    > 对 OnOutOfMemoryError 的运维处理
    >
    > 以部署在 Linux 系统 /opt/Server 目录下的 Server.jar 为例
    >
    > 1. 在 run.sh 启动脚本添加 JVM 参数：`-XX:OnOutOfMemoryError=/opt/Server/restart.sh`
    > 2. restart.sh 脚本
    >
    > Linux 环境：
    >
    > ```shell
    > #!/bin/bash
    > pid=${ps -ef | grep Server.jar | awk '{if($8=="java") {print $2}}'}
    > kill -9 pid
    > cd /opt/Server/;sh run.sh
    > ```
    >
    > Windows 环境：
    >
    > ```shell
    > echo off
    > wmic process where Name='java.exe' delete
    > cd D:\Server
    > start run.bat
    > ```

### 垃圾收集器相关选项



### GC 日志相关选项

### 其他参数

## 通过 Java 代码获 JVM 参数