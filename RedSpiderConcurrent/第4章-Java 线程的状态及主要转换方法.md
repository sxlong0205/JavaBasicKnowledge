### 操作系统中的线程状态转换

在现在的操作系统中，线程是被视为轻量级进程的，所以 **操作系统线程的状态其实和操作系统进程的状态是一致的**。

![](img/系统进程状态转换图.png)

-   就绪状态（ready）：线程正在等待使用 CPU，经调度程序调用之后可进入 running 状态。
-   执行状态（running）：线程正在使用 CPU。
-   等待状态（waiting）：线程经过等待事件的调用或者正在等待其他资源（如 I/O）。

### Java 线程的六个状态

```java
// Thread.State 源码
public enum State {
    NEW,
    RUNNABLE,
    BLOCKED,
    WAITING,
    TIMED_WAITING,
    TERMINATED;
}
```

#### NEW

处于 NEW 状态的线程此时尚未启动。

**关于 `start()` 的两个引申问题**

1.  反复调用同一个线程的 `start()` 方法是否可行？
2.  假如一个线程执行完毕（此时处于 TERMINATED 状态），再次调用这个线程的 `start()` 方法是否可行？

两个问题的答案都是不可行，在调用一次 `start()` 之后，threadStatus 的值会改变（threadStatus !=0），此时再次调用 `start()` 方法会抛出 IllegalThreadStateException 异常。比如，threadStatus 为 2 代表当前线程状态为 TERMINATED。

#### RUNNABLE

表示当前线程正在运行中。处于 RUNNABLE 状态的线程在 Java 虚拟机中运行，也有可能在等待 CPU 分配资源。Java 线程的 **RUNNABLE** 状态其实是包括了传统操作系统线程的 **ready** 和 **running** 两个状态的。

#### BLOCKED

阻塞状态。处于 BLOCKED 状态的线程正等待锁的释放以进入同步区。

#### WAITING

等待状态。处于等待状态的线程变成 RUNNABLE 状态需要其他线程唤醒。

调用如下 3 个方法会使线程进入等待状态：

-   `Object.wait()`：使当前线程处于等待状态直到另一个线程唤醒它；
-   `Thread.join()`：等待线程执行完毕，底层调用的是 Object 实例的 wait 方法；
-   `LockSupport.park()`：除非获得调用许可，否则禁用当前线程进行线程调度。

#### TIMED_WAITING

超时等待状态。线程等待一个具体的时间，时间到后会被自动唤醒。

调用如下方法会使线程进入超时等待状态：

-   `Thread.sleep(long millis)`：使当前线程睡眠指定时间；
-   `Object.wait(long timeout)`：线程休眠指定时间，等待期间可以通过 `notify()/notifyAll()` 唤醒；
-   `Thread.join(long millis)`：等待当前线程最多执行 millis 毫秒，如果 millis 为 0，则会一直执行；
-   `LockSupport.parkNanos(long nanos)`： 除非获得调用许可，否则禁用当前线程进行线程调度指定时间；
-   `LockSupport.parkUntil(long deadline)`：同上，也是禁止线程进行调度指定时间。

#### TERMINATED

终止状态。此时线程已执行完毕。

### 线程状态的转换

![](img/线程状态转换图.png)

#### BLOCKED 与 RUNNABLE 状态的转换

#### WAITING 状态与 RUNNABLE 状态的转换

##### `Object.wait()`

调用 `wait()` 方法前线程必须持有对象的锁。

线程调用 `wait()` 方法时，会释放当前的锁，直到有其他线程调用 `notify()/notifyAll()` 方法唤醒等待锁的线程。

需要注意的是，其他线程调用 `notify()` 方法只会唤醒单个等待锁的线程，如有有多个线程都在等待这个锁的话不一定会唤醒到之前调用 `wait()` 方法的线程。

同样，调用 `notifyAll()` 方法唤醒所有等待锁的线程之后，也不一定会马上把时间片分给刚才放弃锁的那个线程，具体要看系统的调度。

##### `Thread.join()`

调用 `join()` 方法不会释放锁，会一直等待当前线程执行完毕（转换为 TERMINATED 状态）。

#### TIMED_WAITING 与 RUNNABLE 状态转换

##### `Thread.sleep(long)`

使当前线程睡眠指定时间。需要注意这里的“睡眠”只是暂时使线程停止执行，**并不会释放锁**。时间到后，线程会重新进入 RUNNABLE 状态。

##### `Object.wait(long)`

`wait(long)` 方法使线程进入 TIMED_WAITING 状态。这里的 `wait(long)` 方法与无参方法 `wait()` 相同的地方是，都可以通过其他线程调用 `notify()` 或 `notifyAll()` 方法来唤醒。

不同的地方是，有参方法 `wait(long)` 就算其他线程不来唤醒它，经过指定时间 long 之后它会自动唤醒，拥有去争夺锁的资格。

##### `Thread.join(long)`

`join(long)` 使当前线程执行指定时间，并且使线程进入 TIMED_WAITING 状态。

#### 线程中断

简单介绍下 Thread 类里提供的关于线程中断的几个方法：

-   `Thread.interrupt()`：中断线程。这里的中断线程并不会立即停止线程，而是设置线程的中断状态为 true（默认是 flase）；
-   `Thread.interrupted()`：测试当前线程是否被中断。线程的中断状态受这个方法的影响，意思是调用一次使线程中断状态设置为 true，连续调用两次会使得这个线程的中断状态重新转为 false；
-   `Thread.isInterrupted()`：测试当前线程是否被中断。与上面方法不同的是调用这个方法并不会影响线程的中断状态。

>   在线程中断机制里，当其他线程通知需要被中断的线程后，线程中断的状态被设置为 true，但是具体被要求中断的线程要怎么处理，完全由被中断线程自己而定，可以在合适的实际处理中断请求，也可以完全不处理继续执行下去。