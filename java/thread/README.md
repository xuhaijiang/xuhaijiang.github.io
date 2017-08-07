#### 介绍

- [Executor](executor.md) 具体Runnable任务的执行者
- [ExecutorService](executorService.md) 一个线程池管理者，其实现类有多种，我会介绍一部分。我们能把Runnable,Callable提交到池中让其调度
- [Semaphore](semaphore.md) 一个计数信号量
- [ReentrantLock](reentrantLock.md) 一个可重入的互斥锁定 Lock，功能类似synchronized，但要强大的多。
- [Future](future.md) 是与Runnable,Callable进行交互的接口，比如一个线程执行结束后取返回的结果等等，还提供了cancel终止线程,可异步计算的结果
- [BlockingQueue](blockingQueue.md) 阻塞队列。
- [CompletionService](completionService.md) ExecutorService的扩展，可以获得线程执行结果的
- [CountDownLatch](countDownLatch.md) 一个同步辅助类，在完成一组正在其他线程中执行的操作之前，它允许一个或多个线程一直等待。 
- [CyclicBarrier](cyclicBarrier.md) 一个同步辅助类，它允许一组线程互相等待，直到到达某个公共屏障点 
- [ScheduledExecutorService](scheduledExecutorService.md) 一个 ExecutorService，可安排在给定的延迟后运行或定期执行的命令。


#### AQS
**AbstractQueuedSynchronizer.java**
AQS是JDK1.5提供的一个基于FIFO等待队列实现的一个用于实现同步器的基础框架，这个基础框架的重要性可以这么说，JCU包里面几乎所有的有关锁、多线程并发以及线程同步器等重要组件的实现都是基于AQS这个框架。AQS的核心思想是基于volatile int state这样的一个属性同时配合Unsafe工具对其原子性的操作来实现对当前锁的状态进行修改。当state的值为0的时候，标识改Lock不被任何线程所占有。

#### Unsafe
JAVA对硬件级别的原子操作,为CAS技术提供支持。
Unsafe类的使用都是受限制的，只有授信的代码才能获得该类的实例，当然JDK库里面的类是可以随意使用的。

**原子方法**
![](/image/unsafe.png)


#### CAS
Compare and Swap (比较并交换),设计并发算法时的一种技术。

##### CAS有三个操作数
- 内存值V
- 旧的预期值A
- 要修改的值B

**关系：** 当且仅当预期值A和内存值V相同时，将内存值修改为B并返回true，否则什么都不做并返回false。

**AtomicLong.java **代码分析

    // volatile修饰的,对所有线程可见
    private volatile long value;
    
    public final int addAndGet(long delta) {
        // 此循环作用: 保证获取的value和内存中的value一致为止
        for (;;) {
            int current = get();
            int next = current + delta;
            // unsafe 原子操作支持
            if (compareAndSet(current, next))
                return next;
        }
    }

