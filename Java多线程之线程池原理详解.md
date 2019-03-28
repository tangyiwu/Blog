# Java多线程之线程池原理详解

## 1. 线程池的使用

```java
ExecutorService executor = Executors.newCachedThreadPool();

public static ExecutorService newCachedThreadPool() {
        return new ThreadPoolExecutor(0, Integer.MAX_VALUE,
                                      60L, TimeUnit.SECONDS,
                                      new SynchronousQueue<Runnable>());
    }

public static ExecutorService newSingleThreadExecutor() {
        return new FinalizableDelegatedExecutorService
            (new ThreadPoolExecutor(1, 1,
                                    0L, TimeUnit.MILLISECONDS,
                                    new LinkedBlockingQueue<Runnable>()));
    }
```

Java JDK已经为我们提供了一个很好的工具类**Executors**，帮助我们创建各种情况下的线程池，其中都设计到一个类**ThreadPoolExecutor**

```
public ThreadPoolExecutor(int corePoolSize,
                              int maximumPoolSize,
                              long keepAliveTime,
                              TimeUnit unit,
                              BlockingQueue<Runnable> workQueue) {
        this(corePoolSize, maximumPoolSize, keepAliveTime, unit, workQueue,
             Executors.defaultThreadFactory(), defaultHandler);
    }
```

**ThreadPoolExecutor**构造方法中参数含义：

- corePoolSize: 线程池中核心线程数量，即使这些线程已经处于idle状态，正常情况下也不会被线程池销毁，除非调用了方法allowCoreThreadTimeOut
- maximumPoolSize:线程池中持有的线程最大数量。
- keepAliveTime:当线程数量超过corePoolSize时，线程处于idle状态能够等待下个任务到来的最长时间。
- workQueue: 等待执行的任务队列，当线程池中的线程数量超过corePoolSize，并且线程池处于运行状态时，任务是放入workQueue中，如果某个线程处于idle状态时，会尝试从workQueue中获取一个任务并执行任务。



