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
| void | lock() | 获取锁 |
| void | unlock() | 视图释放锁。如果当前线程是此锁的所有者，则将保持计数减 1。如果保持计数现在为0，则释放锁。如果当前线程不是此锁的所有者，则抛出异常 IllegalMonitorStateException |


#### 示例
