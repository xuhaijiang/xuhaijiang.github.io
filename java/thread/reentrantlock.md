#### ReentrantLock
一个可重入的互斥锁,它具有与使用 Synchronized 方法和语句所访问的隐式监视器锁相同的一些行为和语义，但功能更强大。
-使用 lock块来调用 try , 在之前/之后的构造，经典代码如下:-
    class X {
        private final ReentrantLock lock = new ReentrantLock();
        // ...
        
        public void m() {
            lock.lock();
            try {
            } finally {
                lock.unlock();
            }
        }
    
    }

#### API


#### 示例
