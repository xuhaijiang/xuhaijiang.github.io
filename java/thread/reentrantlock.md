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
| void | acquire() |从此信号量获取一个许可,在提供一个许可前一直将线程阻塞，否则线程被中断 |


#### 示例
