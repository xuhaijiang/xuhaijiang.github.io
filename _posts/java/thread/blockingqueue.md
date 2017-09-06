#### BlockingQueue 阻塞队列
阻塞队列与普通队列的区别在于，当队列是空的时，从队列中获取元素的操作将会被阻塞，或者当队列是满时，往队列里添加元素的操作会被阻塞。试图从空的阻塞队列中获取元素的线程将会被阻塞，直到其他的线程往空的队列插入新的元素。同样，试图往已满的阻塞队列中添加新元素的线程同样也会被阻塞，直到其他的线程使队列重新变得空闲起来。


#### API

| 返回 | 方法 | 说明 |
|:---:|:---|:---|
| boolean | offer(E e) | 将指定元素插入此队列中,成功时返回 true ,如果当前没有可用空间，则返回 false 。 |
| void | put(E e) | 将指定元素插入此队列中，将等待可用的空间（如果有必要）。 |
| E | take() | 获取并移除此队列的头部，在元素变得可用之前一直等待 |
| E | poll(long timeout, TimeUnit unit) | 获取并移除此队列的头部，在指定的等待时间前等待可用的元素 |
| boolean | remove(Object o) | 从此队列中移除指定的单个实例。更确切的讲，如果此队列包含一个或多个满足 o.equals(e) 的元素 e，则移除该元素。|
| boolean | contains(Object o) | 如果此队列包含指定元素，则返回 true。 |
| int | drainTo(Collection<? super E> c) | 移除此队列中所有可用的元素，并将他们添加给指定的 Collection 中。 |

#### 示例
    import java.util.concurrent.BlockingQueue;
	import java.util.concurrent.ExecutorService;
	import java.util.concurrent.Executors;
	import java.util.concurrent.LinkedBlockingQueue;
	
	public class MyBlockingQueue extends Thread {
		public static BlockingQueue<String> queue = new LinkedBlockingQueue<String>(3);
		private int index;
	
		public MyBlockingQueue(int i) {
			this.index = i;
		}
	
		public void run() {
			try {
				queue.put(String.valueOf(this.index));
				System.out.println("{" + this.index + "} in queue!");
			} catch (Exception e) {
				e.printStackTrace();
			}
		}
	
		public static void main(String args[]) {
			ExecutorService service = Executors.newCachedThreadPool();
			for (int i = 0; i < 10; i++) {
				service.submit(new MyBlockingQueue(i));
			}
			Thread thread = new Thread() {
				public void run() {
					try {
						while (true) {
							Thread.sleep((int) (Math.random() * 1000));
							if (MyBlockingQueue.queue.isEmpty())
								break;
							String str = MyBlockingQueue.queue.take();
							System.out.println(str + " has take!");
						}
					} catch (Exception e) {
						e.printStackTrace();
					}
				}
			};
			service.submit(thread);
			service.shutdown();
		}
	}