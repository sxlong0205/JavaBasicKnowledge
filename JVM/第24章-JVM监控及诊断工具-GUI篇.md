# JVM监控及诊断工具-GUI篇

## 工具概述

使用上一章命令行工具或组合能帮您获取目标 Java 应用性能相关的基础信息，但它们存在下列局限：

1. 无法获取方法级别的分析数据，如方法间的调用关系，各方法的调用次数和调用时间等（这对定位应用性能瓶颈至关重要）。
2. 要求用户登录到目标 Java 应用所在的宿主机上，使用起来不是很方便。
3. 分析数据通过终端输出，结果展示不够直观。

为此，JDK 提供了一些内存泄漏的分析工具，如 JConsole、jVisual VM 等，用于辅助开发人员定位问题，但这些工具很多时候并不足以满足快速定位的需求，所以这里我们介绍的工具相对多一些、丰富一些。

图形化综合诊断工具：

- JDK 自带的工具

    - JConsole：JDK 自带的可视化监控工具、查看 Java 应用程序的运行概况、监控堆信息、永久区（或元空间）使用情况、类加载情况等。

        位置：jdk\bin\JConsole.exe

    - Visual VM：Visual VM 是一个工具，它提供了一个可视界面，用于查看 Java 虚拟机上运行的基于 Java 技术的应用程序的详细信息。

        位置：jdk\bin\jvisualvm.exe

    - JVM：Java Mission Control，内置 Java Flight Recorder，能够以极低的性能开销收集 Java 虚拟机的性能数据。

- 第三方工具

    - MAT：MAT（Memory Analyzer Tool）是基于 Eclipse 的内存分析工具，是一个快速、功能丰富的 Java Heap 分析工具，它可以帮助我们查看内存泄漏和减少内存消耗。
    - JProfiler：商业软件，需要付费，功能强大。
    - Arthas：Alibaba 开源的 Java 诊断工具。
    - Btrace：Java 运行时追踪工具，可以在不停机的情况下，跟踪指定的方法调用、构造函数调用和系统内存等信息。

## JConsole

### 基本概述

- 从 Java 5 开始，在 JDK 中自带的 Java 监控和管理控制台。
- 用于对 JVM 中内存、线程和类等的监控，是一个基于 JMX（Java Management Extensions）的 GUI 性能监控工具。

官方教程：https://docs.oracle.com/javase/7/docs/technotes/guides/management/JConsole.html

### 启动

jdk/bin 目录下，启动 JConsole.exe 即可，不需要使用 jps 命令来查询。

### 三种连接方式

- Local：使用 JConsole 连接一个正在本地系统运行的 JVM，并且执行程序的和运行 JConsole 的需要是同一个用户，JConsole 使用文件系统的授权通过 RMI 连接器连接到平台的 MBean 服务器上。这种从本地连接的监控能力只有 Sun 的 JDK 具有。
- Remote：使用下面的 URL 通过 RMI 连接器连接到一个 JMX 代理，service:jmx:rmi:///jndi/rmi://hostName:portNum/jmxrmi。JConsole 为建立连接，需要在环境变量中设置 mx.remote.credentials 来指定用户名和密码，从而进行授权。
- Advanced：使用一个特殊的 URL 连接 JMX 代理。一般情况使用自己定制的连接器而不是 RMI 提供的连接器来连接 JMX 代理，或者是一个使用 JDK 1.4 的实现了 JMX 和 JMX Remote 的应用。

### 主要作用

- 监控内存
- 监控线程
- 监控死锁
- 类加载与虚拟机信息

## Visual VM

### 基本概述

Visual VM 是一个功能强大的多合一故障诊断和性能监控的可视化工具。

它继承了多个 JDK 命令行工具，使用 Visual VM 可用于显示虚拟机进程及进程的配置和环境信息（jps、jinfo），监视应用程序的 CPU、GC、堆、方法区及线程的信息（jstat、jstack）等，甚至代替 JConsole。

在 JDK 6 update 7 以后，Visual VM 便作为 JDK 的一部分发布（Visual VM 在 JDK/bin 目录下）。

此外，Visual VM 也可以作为独立的软件安装。首页：https://visualvm.github.io/index.html

### 插件的安装

Visual VM 的一大特点是支持插件扩展，并且插件安装非常方便。我们既可以通过离线下载插件文件 *.nbm，然后在 Plugin 对话框的已下载页面下，添加已下载的插件。也可以在可用插件页面下，在线安装插件。插件地址：https://visualvm.github.io/pluginscenters.html

IDEA 安装 Visual VM Launcher 插件：

```
Preferences --> Plugins --> 搜索 Visual VM Launcher，安装重启即可。
```

### 连接方式

本地连接：监控本地 Java 进程的 CPU、类、线程等。

远程连接：

1. 确定远程服务器的 IP 地址
2. 添加 JMX（通过 JMX 技术具体监控远端服务器哪个 Java 进程）
3. 修改 bin/catalina.sh 文件，连接远程的 Tomcat
4. 在 ../conf 中添加 jmxremote.access 和 jmxremote.password 文件
5. 将服务器地址改为公网 IP 地址
6. 设置阿里云安全策略和防火墙策略
7. 启动 Tomcat，查看 Tomcat 启动日志和端口监听
8. JMX 中输入端口号、用户名、密码登录

### 主要功能

1. 生成/读取堆内存快照
2. 查看 JVM 参数和系统属性
3. 查看运行中的虚拟机进程
4. 生成/读取线程快照
5. 程序资源的实时监控
6. 其他功能：
    1. JMX 代理连接
    2. 远程环境监控
    3. CPU 分析和内存分析

## Eclipse MAT

### 基本概述

MAT（Memory Analyzer Tool）工具是一款功能强大的 Java 堆内存分析器。可以用于查找内存泄漏以及查看内存消耗情况。

MAT 是基于 Eclipse 开发的，不仅可以单独使用，还可以作为插件的形式嵌入在 Eclipse 中使用，是一款免费的性能分析工具，使用起来非常方便。可以在 https://www.eclipse.org/mat/downloads.php 下载并使用 MAT。

### 获取堆 dump 文件

**dump 文件内容**

MAT 可以分析 Heap dump 文件。在进行内存分析时，只要获得了反映当前设备内存映像的 hprof 文件，通过 MAT 打开就可以直观地看到当前的内存信息。

一般来说：这些内存信息包含：

- 所有的对象信息，包括对象实例、成员变量、存储于栈中的基本类型值和存储于堆中的其他对象的引用值。
- 所有的类信息，包括 ClassLoader、类名称、父类、静态变量等。
- GCRoot 到所有的这些对象的引用路径。
- 线程信息，包括线程的调用栈及此线程的线程局部变量（TLS）。

**两点说明**

说明 1：

MAT 不是一个万能的工具，它并不能处理所有类型的堆存储文件。但是比较主流的厂家和格式，例如 Sun、HP、SAP 所采用的 HPROF 二进制堆存储文件。以及 IBM 的 PHD 堆存储文件等都能被很好地解析。

说明 2：

最吸引人的还是能够快速为开发人员生成内存泄漏报表，方便定位问题和分析问题。虽然 MAT 有如此强大的功能，但是内存分析也没有简单到一键完成的程度，很多内存问题还是需要我们从 MAT 展现给我们的信息当中通过经验和直觉来判断才能发现。

**获取 dump 文件**

方法一：通过前一章介绍的 jmap 工具生成，可以生成任意一个 Java 进程的 dump 文件；

方法二：通过配置 JVM 参数生成

- 选项"`-XX:+HeapDumpOnOutOfMemoryError`"或"`-XX:+HeapDumpBeforeFullGC`"
- 选项"`-XX:HeapDumpPath`"所代表的含义就是当程序出现 OutOfMemory 时，将会在相应的目录下生成一份 dump 文件。如果不指定选项"`XX:HeapDumpPath`"则在当前目录下生成 dump 文件。

对比：考虑到生产环境中几乎不可能在线对其进行分析，大家都是采用离线分析，因此使用 jmap+MAT 工具是最常见的组合。

方法三：使用 Visual VM 可以导出堆 dump 文件。

方法四：使用 MAT 既可以打开一个已有的堆快照，也可以通过 MAT 直接从活动 Java 程序中导出堆快照。该功能将借助 jps 列出当前正在运行的 Java 进程，以供选择并获取快照。

![image-20220513113547589](img/image-20220513113547589.png)

### 分析堆 dump 文件

**histogram**

展示了各个类的实例数目以及这些实例的 Shallow Heap 或 Retained Heap 的总和。

MAT 的直方图和 jmap 的 -histo 子命令一样，都能够展示各个类的实例数目以及这些实例的 Shallow Heap 总和。但是，MAT 的直方图还能够计算 Retained Heap，并支持基于实例数目或 Retained Heap 的排序方式（默认为 Shallow Heap）。

此外，MAT 还可以将直方图中的类按照超类、类加载器或者包名分组。

当选中某个类时，MAT 界面左上角的 Inspector 窗口将展示该类的 Class 实例的相关信息，如类加载器等。

**Thread Overview**

- 查看系统中的 Java 线程
- 查看局部变量的信息

**获得对象相互引用的关系**

- with outgoing references
- with incoming references

**浅堆与深堆**

- Shallow Heap

    浅堆（Shallow Heap）是指一个对象所消耗的内存。在 32 位系统中，一个对象引用会占据 4 个字节，一个 int 类型会占据 4 个字节，long 型变量会占据 8 个字节，每个对象头需要占用 8 个字节。根据堆快照格式不同，对象的大小可能会向 8 字节进行对齐。 

    以 String 为例：2 个 int 值共占 8 字节，对象引用占用 4 字节，对象头 8 字节，合计 20 字节，向 8 字节对齐，故占 24 字节。（JDK 7 中）

    这 24 字节为 String 对象的浅堆大小。它与 String 的 value 实际取值无关，无论字符串长度如何，浅堆大小始终是 24 字节。

- Retained Heap

    保留集（Retained Set）：

    对象 A 的保留集指当对象 A 被垃圾回收后，可以被释放的所有对象集合（包括对象 A 本身），即对象 A 的保留集可以被认为是只能通过对象 A 被直接或间接访问到的所有对象的集合。通俗地说，就是指仅被对象 A 所持有的对象的集合。

    深堆（Retained Heap）：

    深堆是指对象的保留集中所有的对象的浅堆大小之和。

    注意：浅堆指对象本身占用的内存，不包括其内部引用对象的大小。一个对象的深堆指只能通过该对象访问到的（直接或间接）所有对象的浅堆之和，即对象被回收后，可以释放的真实空间。

- 对象实际大小

    另外一个常用的概念是对象的实际大小。这里，对象的实际大小定义为一个对象所能触及的所有对象的浅堆大小之和，也就是通常意义上我们说的对象大小。与深堆相比，似乎这个在日常开发中更为直观和被人接受。但实际上，这个概念和垃圾回收无关。

    下图显示了一个简单的对象引用关系图，对象 A 引用了 C 和 D，对象 B 引用了 C 和 E。那么对象 A 的浅堆大小只是 A 本身，不含 C 和 D，而 A 的实际大小为A、C、D 三者之和。而 A 的深堆大小为 A 与 D 之和，由于对象 C 还可以通过对象 B 访问到，因此不在对象 A 的深堆范围内。

    ![image-20220513115746866](img/image-20220513115746866.png)

- 练习

    看图理解 Retained Size

    ![image-20220513115845005](img/image-20220513115845005.png)

    上图中，GC Roots 直接引用了 A 和 B 两个对象。

    A 对象的 Retained Size=A 对象的 Shallow Size

    B 对象的 Retained Size=B 对象的 Shallow Size + C 对象的 Shallow Size

    这里不包括 D 对象，因为 D 对象被 GC Roots 直接引用。

- 支配树（Dominator Tree）

    支配树的概念源自图论。

    MAT 提供了一个称为支配树（Dominator Tree）的对象图。支配树体现了对象实例间的支配关系。在对象引用图中，所有指向对象 B 的路径都经过对象 A，则认为对象 A 支配对象 B。如果对象 A 是离对象 B 最近的一个支配对象，则认为对象 A 为对象 B 的直接支配者。支配树是基于对象间的引用图所建立的，它有以下基本性质：

    - 对象 A 的子树（所有被对象 A 支配的对象集合）表示对象 A 的保留集（Retained Set），即深堆。
    - 如果对象 A 支配对象 B，那么对象 A 的直接支配者也支配对象 B。
    - 支配树的边与对象引用图的边不直接对应。

    如下图所示：左图表示对象引用图，右图表示左图所对应的支配树。对象 A 和 B 由根对象直接支配，由于在到对象 C 的路径中，可以经过 A，也可以经过 B，因此对象 C 的直接支配者也是根对象。对象 F 与对象 D 相互引用，因为到对象 F 的所有路径必然经过对象 D，因此，对象 D 是对象 F 的直接支配者。而到对象 D 的所有路径中，必然经过对象 C，即使是从对象 F 到对象 D 的引用，从根节点出发，也是经过对象 C 的，所以，对象 D 的直接支配者为对象 C。

    ![image-20220513121457201](img/image-20220513121457201.png)

    同理，对象 E 支配对象 G。到达对象 H 的可以通过对象 D，也可以通过对象 E，因此对象 D 和 E 都不能支配对象 H，而经过对象 C 既可以到达 D 也可以到达 E，因此对象 C 为对象 H 的直接支配者。

    在 MAT 中，单击工具栏上的对象支配树按钮，可以打开对象支配树视图。

    ![image-20220513121643751](img/image-20220513121643751.png)

    下图显示了对象支配树视图的一部分。该截图显示部分 Lily 学生的 history 队列的直接支配对象。即当 Lily 对象被回收，也会一并回收的所有对象。显然能被 3 或者 5 整除的网页不会出现在该列表中，因为它们同时被另外两名学生对象引用。

    ![image-20220513121813229](img/image-20220513121813229.png)

## 再谈内存泄漏

### 内存泄露的理解与分类

**何为内存泄漏（Memory Leak）**

![image-20220513152746452](img/image-20220513152746452.png)

可达性分析算法来判断对象是否是不再使用的对象，本质都是判断一个对象是否还被引用。那么对于这种情况，由于代码的实现不同就会出现很多种内存泄漏问题（让 JVM 误以为此对象还在引用中，无法回收，造成内存泄漏）。

**内存泄漏（Memory Leak）的理解**

严格来说，只有对象不会再被程序用到了，但是 GC 又不能回收他们的情况，才叫内存泄漏。但实际情况很多时候一些不太好的实践（或疏忽）会导致对象的生命周期变得很长甚至导致 OOM，也可以叫做宽泛意义上的"内存泄漏"。

![image-20220513153747796](img/image-20220513153747796.png)

对象 X 引用对象 Y，X 的生命周期比 Y 的生命周期长，那么当 Y 生命周期结束的时候，X 依然引用着 Y，这时候，垃圾回收器是不会回收对象 Y 的；如果对象 X 还引用着生命周期比较短的 A、B、C，对象 A 又引用着对象 A、B、C，这样就可能造成大量无用的对象不能被回收，进而占据了内存资源，造成内存泄漏，直到内存溢出。

**内存泄漏和内存溢出的关系**

1. 内存泄漏（Memory Leak）

    申请了内存用完了不释放，比如一共有 1024M 的内存，分配了 521M 的内存一直不回收，那么可以用的内存只有 521M 了，仿佛泄漏掉了一部分。

2. 内存溢出（Out Of Memory）

    申请内存时，没有足够的内存可以使用。

可见，内存泄漏和内存溢出的关系：内存泄漏的增多，最终会导致内存溢出。

**泄漏的分类**

经常发生：发生内存泄露的代码会被多次执行，每次执行，泄漏一块内存；

偶尔发生：在某些特定情况下才会发生；

一次性：发生内存泄漏的方法只会执行一次；

隐式泄漏：一直占着内存不释放，直到执行结束；严格地说这个不算内存泄漏，因为最终释放掉了，但是如果执行时间特别长，也可能会导致内存耗尽。

### Java 中内存泄漏的 8 种情况

1. 静态集合类

    静态集合类，如 HashMap、LinkedList 等等。如果这些容器为静态的，那么它们的生命周期与 JVM 程序一致，则容器中的对象在程序结束之前将不能被释放，从而造成内存泄漏。简单而言，长生命周期的对象持有短生命周期对象的引用，尽管短生命周期的对象不再使用，但是因为长生命周期对象持有它的引用而导致不能被回收。

    ```java 
    public class MemoryLeak {
        static List list = new ArrayList();
        
        public void comTests() {
            Object obj = new Object();
            list.add(obj);
        }
    }
    ```

2. 单例模式

    单例模式，和静态集合导致内存泄漏的原因类似，因为单例的静态特性，它的生命周期和 JVM 的生命周期一样长，所以如果单例对象如果持有外部对象的引用，那么这个外部独享也不会被回收，那么就会造成内存泄漏。

3. 内部类持有外部类

    内部类持有外部类，如果一个外部类的实例对象的方法返回了一个内部类的实例对象。这个内部类对象被长期引用了，即使那个外部类实例对象不再被使用，但由于内部类持有外部类的实例对象，这个外部类对象将不会被垃圾回收，这也会造成内存泄漏。

4. 各种连接，如数据库连接、网络连接和 IO 连接等

    在对数据库进行操作的过程中，首先需要建立与数据库的连接，当不再使用时，需要调用 close 方法来释放与数据库的连接。只有连接被关闭后，垃圾回收器才会回收对应的对象。

    否则，如果在访问数据库的过程中，对 Connection、Statement 或 ResultSet 不显性地关闭，将会造成大量的对象无法被回收，从而引起内存泄漏。

    ```java
    public static void main(String[] args) {
        try {
            Connection conn = null;
            Class.forName("com.mysql.jdbc.Driver");
            conn = DriverManager.getConnection("url", "", "");
            Statement stmt = conn.createStatement();
            ResultSet rs = stmt.executeQuery("...");
        }catch (Exception e) {
            // 异常日志
        }finally {
            // 1.关闭结果集 Statement
            // 2.关闭声明的对象 ResultSet
            // 3.关闭连接 Connection
        }
    }
    ```

5. 变量不合理的作用域

    变量不合理的作用域。一般而言，一个变量的定义的作用范围大于其使用范围，很有可能会造成内存泄漏。另一方面，如果没有及时地把对象设置为 null，很有可能导致内存泄漏发生。

    ```java
    public class UsingRandom {
        private String msg;
        
        public void receiveMsg() {
            readFromNet(); // 从网络中接受数据保存到 msg 中
            saveDB(); // 把 msg 保存到数据库中
        }
    }
    ```

    如果上面这个伪代码，通过 readFromNet 方法把接受的消息保存在变量 msg 中，然后调用 saveDB 方法把 msg 的内容保存到数据库中，此时 msg 已经就没有用了，由于 msg 的生命周期与对象的生命周期相同，此时 msg 还不能回收，因此造成了内存泄漏。

    实际上这个 msg 变量可以放在 receiveMsg 方法内部，当方法使用完，那么 msg 的生命周期也就结束，此时就可以回收了。还有一种方法，在使用完 msg 后，把 msg 设置为 null，这样垃圾回收器也会回收 msg 的内存空间。

6. 改变哈希值

    改变哈希值，当一个对象被存储进 HashSet 集合中以后，就不能修改这个对象中的那些参与计算哈希值的字段了。

    否则，对象修改后的哈希值与最初存储进 HashSet 集合中时的哈希值就不同了，在这种情况下，即使在 contains 方法使用该对象的当前引用作为的参数去 HashSet 集合中检索对象，也将返回找不到对象的结果，这也会导致无法从 HashSet 集合中单独删除当前对象，造成内存泄漏。

    这也是 String 为什么被设置成了不可变类型，我们可以放心地把 String 存入 HashSet，或者把 String 当做 HashMap 的 key 值。

    当我们想把自己定义的类保存到散列表的时候，需要保证对象的 hashCode 不可改变。

7. 缓存泄露

    内存泄漏的另一个常见来源是缓存，一旦你把对象引用放入到缓存中，它就很容易遗忘。比如：之前项目在一次上线的时候，应用启动奇慢直到夯死，就是因为代码中会加载一个表中的数据到缓存（内存）中，测试环境只有几百条数据，但是生产环境有几百万的数据。

    对于这个问题，可以使用 WeakHashMap 代表缓存，此种 Map 的特点是，当除了自身有对 key 的引用外，此 key 没有其他引用那么此 map 会自动丢弃此值。

8. 监听器和回调

    内存泄漏第三个常见来源是监听器和其他回调，如果客户端在你实现的 API 中注册回调，却没有显示的取消，那么就会积聚。

    需要确保回调立即被当作垃圾回收的最佳方法是只保存它的弱引用，例如将他们保存成为 WeakHashMap 中的键。

### 支持使用 OQL 语言查询对象信息

MAT 支持一种类似于 SQL 的查询语言 OQL（Object Query Language），OQL 使用类 SQL 语法，可以在堆中进行对象的查找和筛选。

**SELECT 子句**

在 MAT 中，SELECT 子句的格式与 SQL 基本一致，用于指定要显示的列，SELECT 子句中可以使用"*"，查看结果对象的引用实例（相当于 outgoing reference）。

```sql
SELECT * FROM java.util.Vector v
```

使用"OBJECTS"关键字，可以将返回结果集中的项以对象的形式显示。

```sql
SELECT objects v.elementData FROM java.util.Vector v
SELECT objects s.value FROM java.lang.String s
```

在 SELECT 子句中，使用"AS RETAINED SET"关键字可以得到所得对象的保留集。

```sql
SELECT AS RETAINED SET * FROM com.atguigu.mat.Student
```

"DISTINCT" 关键字用于在结果集中去除重复对象。

```sql
SELECT DISTINCT OBJECTS classof(s) FROM java.lang.String s
```

**FROM 子句**

FROM 子句用于指定查询范围，它可以指定类名、正则表达式或者对象地址。

```sql
SELECT * FROM java.lang.String s
```

下列使用正则表达式，限定搜索范围，输出所有 com.atguigu 包下所有类的实例

```sql
SELECT * FROM "com\.atguigu\.."
```

也可以直接使用类的地址进行搜索。使用类的地址的好处是可以区分被不同 ClassLoader 加载的同一种类型。

```sql
SELECT * FROM 0x37a0b4d
```

**WHERE 子句**

WHERE 子句用于指定 OQL 的查询条件。OQL 查询将只返回满足 WHERE 子句指定条件的对象。WHERE 子句的格式与传统 SQL 极为相似。

下例返回长度大于 10 的 char 数组。

```sql
SELECT * FROM char[] s WHERE s.lenght > 10
```

下例返回所有 value 域不为 null 的字符串，使用"="操作符。

```sql
SELECT * FROM java.lang.String s WHERE s.value != null 
```

WHERE 子句支持多个条件的 AND、OR 运算。下例返回数组长度大于 15，并且深堆大于 1000 字节的所有 Vector 对象。

```sql
SELECT * FROM java.util.Vector v WHERE v.elementData.@length >15 AND v.@retainedHeapSize > 1000
```

**内置对象与方法**

OQL 中可以访问堆内对象的属性，也可以访问堆内代理对象的属性，访问堆内对象的属性时，格式如下：

`[<alias>.] <field>.<field>.<field>`，其中 alias 为对象名称。

访问 java.io.File 对象的 path 属性，并进一步访问 path 的 value 属性。

```sql
SELECT toString(f.path.value) FROM java.io.File f
```

下例显示了 String 对象的内容、objectId 和 objectAddress：

```sql
SELECT s.toString(), s.@objectId, s.@objectAddress FROM java.lang.String s
```

下例显示了 java.util.Vector 内部数组的长度：

```sql
SELECT v.elementData.@length FROM java.util.Vector v
```

下例显示了所有的 java.util.Vector 对象及其子类型：

```sql
SELECT * FROM INSTANCEOF java.util.Vector
```

## JProfiler



## Arthas



## Java Mission Control



## Btrace



## Flame Graphs（火焰图）