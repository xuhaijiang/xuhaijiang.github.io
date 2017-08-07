#### ReentrantLock
一个可重入的互斥锁,它具有与使用 Synchronized 方法和语句所访问的隐式监视器锁相同的一些行为和语义，但功能更强大。

_使用 lock块来调用 try , 在之前/之后的构造，经典代码如下:_
    class X {
        private final ReentrantLock lock = new ReentrantLock();
        // ...
        
        public void m() {
            lock.lock();
            try {
                // ... method body
            } finally {
                lock.unlock();
            }
        }
    }

#### API
| 返回 | 方法 | 说明 |
|---|:---|:---:|
| void | lock() | 获取锁。如果该锁没有被其他线程持有，则获得该锁并立即返回，将锁的保持计数设置为1。如果当前线程已经持有该锁，则将保持计数加1，并且该方法立即返回。如果该锁被其他线程持有，则禁用当前线程，并且在获得锁之前，该线程将一直处于休眠状态，此时锁保持计数被设置为1。 |
| void | unlock() | 视图释放锁。如果当前线程是此锁的所有者，则将保持计数减 1。如果保持计数现在为0，则释放锁。如果当前线程不是此锁的所有者，则抛出异常 IllegalMonitorStateException |
| boolean | isFair() | 如果此锁的公平设置为true，则返回 true。


#### 示例
