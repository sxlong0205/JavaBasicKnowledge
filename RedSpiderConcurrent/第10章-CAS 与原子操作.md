## 乐观锁与悲观锁的概念

悲观锁：总是认为每次访问共享变量资源时会发生冲突。

乐观锁：又称为"无锁"，当线程发生冲突时，乐观锁通常是使用一种称为 CAS 的技术来保证线程执行的安全性。 **由于无锁操作中没有锁的存在，因此乐观锁天生免疫死锁。**

## CAS 的概念

CAS 的全称是：比较并交换（Compare And Swap），在 CAS 中，有这样三个值：

- V：要更新的变量（var）
- E：预期值（expected）
- N：新值（new）

比较并交换的过程：判断 V 是否等于 E，如果等于，将 V 的值设置为 N；如果不等，则当前线程放弃更新，什么都不做， **所以这里的预期值 E 本质上指的是"旧值"。**

> CAS 是一种原子操作，是一种系统原语，是一条 CPU 的原子指令，从 CPU 层面保证它的原子性。

**当多个线程同时使用 CAS 操作一个变量时，只有一个会胜出，并成功更新，其余均会失败，但失败的线程并不会被挂起，仅是被告知失败，并且允许再次尝试，当然也允许失败的线程放弃操作。**

### Java 实现 CAS 的原理-Unsafe 类

```java
public native boolean compareAndSwapObject(Object o, long offset,Object expected, Object x);
public native boolean compareAndSwapInt(Object o, long offset,int expected,int x);
public native boolean compareAndSwapLong(Object o, long offset,long expected,long x);
```

Linux 的 X86 下主要是通过 cmpxchgl 这个指令在 CPU 级完成 CAS 操作的，但在多处理器情况下必须使用 lock 指令加锁来完成。 

### 原子操作-AtomicInteger 类源码解析

```java
@HotSpotIntrinsicCandidate
public final int getAndAddInt(Object o, long offset, int delta) {
    int v;
    do {
        v = getIntVolatile(o, offset);
    } while (!weakCompareAndSetInt(o, offset, v, v + delta));
    return v;
}
```
这里使用的是 do-while 循环，它的目的是保证循环体内的语句至少会被执行一遍。这样才能保证 return 的值 v 是我们期望的值。

```java
public final boolean weakCompareAndSetInt(Object o, long offset,
                                          int expected,
                                          int x) {
    return compareAndSetInt(o, offset, expected, x);
}

public final native boolean compareAndSetInt(Object o, long offset,
                                             int expected,
                                             int x);
```
这里可以看到，其实最终调用的就是 Unsafe 类中的 native 方法。

> 为什么不直接调用 compareAndSetInt 而是要通过 weakCompareAndSetInt 方法？
>
> 这两个方法上面增加了 @HotSpotIntrinsicCandidate 注解，这个注解允许虚拟机自己来写汇编或 IR 编译器来实现该方法以提高性能，所以虽然底层调用的方法一样，但是不排除 HotSpot VM 会手动实现 weakCompareAndSet 真正含义功能的可能性。也就是说 weakCompareAndSet 无法保证处理操作目标的 volatile 变量外的其他变量的执行顺序（编译器和处理器为了优化程序性能而对指令序列进行重新排序），同时也无法保证这些变量的可见性。这在一定程度上可以提高性能。

### CAS 实现原子操作的三大问题
#### ABA 问题

所谓 ABA 问题，就是一个值原来是 A，变成了 B，又变回了 A。这个时候使用 CAS 是检查不出变化的，但实际上却被更新了两次。

ABA 问题的解决思路是在变量前面追加上版本号或者时间戳。从 JDK 1.5 开始，JDK 的 atomic 包里提供了一个类 AtomicStampedReference 类来解决 ABA 问题。

这个类的 compareAndSet 方法的作用是首先检查当前引用是否等于预期引用，并且检查当前标志是否等于预期标志，如果二者都相等，才使用 CAS 设置为新的值和标志。
```java
public boolean compareAndSet(V   expectedReference,
                             V   newReference,
                             int expectedStamp,
                             int newStamp) {
    Pair<V> current = pair;
    return
        expectedReference == current.reference &&
        expectedStamp == current.stamp &&
        ((newReference == current.reference &&
          newStamp == current.stamp) ||
         casPair(current, Pair.of(newReference, newStamp)));
}
```

#### 循环时间长开销大

解决思路是让 JVM 支持处理器提供的 pause 指令。pause 指令能让自旋失败时 CPU 睡眠一小段时间再继续自旋。

#### 只能保证一个共享变量的原子操作
这个问题有两种解决方案：
1. 使用 JDK 1.5 提供的 AtomicReference 类保证对象之间的原子性，把多个变量放到一个对象里面进行 CAS 操作；
2. 使用锁。