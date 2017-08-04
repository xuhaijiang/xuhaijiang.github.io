#### 介绍

- [Executor](java/thread/Executor.md) 具体Runnable任务的执行者

- [ExecutorService](java/thread/ExecutorService.md) 一个线程池管理者，其实现类有多种，我会介绍一部分。我们能把Runnable,Callable提交到池中让其调度
- [Semaphore](java/thread/Semaphore.md) 一个计数信号量
- [ReentrantLock](java/thread/ReentrantLock.md) 一个可重入的互斥锁定 Lock，功能类似synchronized，但要强大的多。
- [Future](java/thread/Future.md) 是与Runnable,Callable进行交互的接口，比如一个线程执行结束后取返回的结果等等，还提供了cancel终止线程,可异步计算的结果
- [BlockingQueue](java/thread/BlockingQueue.md) 阻塞队列。
- [CompletionService](java/thread/CompletionService.md) ExecutorService的扩展，可以获得线程执行结果的
- [CountDownLatch](java/thread/CountDownLatch.md) 一个同步辅助类，在完成一组正在其他线程中执行的操作之前，它允许一个或多个线程一直等待。 
- [CyclicBarrier](java/thread/CyclicBarrier.md) 一个同步辅助类，它允许一组线程互相等待，直到到达某个公共屏障点 
- [ScheduledExecutorService](java/thread/ScheduledExecutorService.md) 一个 ExecutorService，可安排在给定的延迟后运行或定期执行的命令。