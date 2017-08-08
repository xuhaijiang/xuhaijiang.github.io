#### CyclicBarrier 同步工具
一个同步辅助类，它允许一组线程互相等待，直到到达某个公共屏障点 (common barrier point)。在涉及一组固定大小的线程的程序中，这些线程必须不时地互相等待，此时 CyclicBarrier 很有用。因为该 barrier 在释放等待线程后可以重用，所以称它为循环 的 barrier。



#### API

| 返回 | 方法 | 说明 |
|:---:|:---|:---|
| int | await() | 所有线程都在此 barrier 上调用 await 方法之前将一直等待。 |
| int | getNumberWaiting() | 返回当前屏障点等待的线程数目。 |
| int | getparties() | 返回要求启动此屏障点的线程数目。 |
| boolean | isBroken() | 查询此屏障点是否处于损坏状态。 |
| void | reset() | 将屏障点重置为初始状态。 |



#### 示例