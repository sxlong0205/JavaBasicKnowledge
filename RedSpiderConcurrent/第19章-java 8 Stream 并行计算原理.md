### Java 8 Stream 简介

从 Java 8 开始，我们可以使用 Stream 接口以及 **lambda 表达式** 进行“流式计算”。它可以让我们对集合的操作更加简洁、更加可读、更加高效。

### Stream 单线程串行计算

Stream 接口默认是使用串行的方式

```java
public class StreamDemo {
    public static void main(String[] args) {
        Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9)
                .reduce((a, b) -> {
                    System.out.println(String.format("%s: %d + %d = %d",
                            Thread.currentThread().getName(), a, b, a + b));
                    return a + b;
                })
                .ifPresent(System.out::println);
    }
}
```

### Stream 多线程并行计算

```java
public class StreamParallelDemo {
    public static void main(String[] args) {
        Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9)
                .parallel()
                .reduce((a, b) -> {
                    System.out.println(String.format("%s: %d + %d = %d",
                            Thread.currentThread().getName(), a, b, a + b));
                    return a + b;
                })
                .ifPresent(System.out::println);
    }
}
```

可以很明显地看到，它使用的线程是 ForkJoinPool 里面的 commonPool 里面的 **worker** 线程。并且它们是并行计算的，并不是串行计算的。但由于 Fork/Join 框架的作用，它最终能很好的协调计算结果，使得计算结果完全正确。



