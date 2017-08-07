#### Semaphore

一个计数信号量。从概念上讲，信号量维护了一个许可集合。如有必要，在许可可用前会阻塞每一个 acquire()，然后再获取该许可。每个 release() 添加一个许可，从而可能释放一个正在阻塞的获取者。但是，不使用实际的许可对象，Semaphore 只对可用许可的号码进行计数，并采取相应的行动。
Semaphore 通常用于限制可以访问某些资源（物理或逻辑的）的线程数目。

#### API
| 返回 | 方法 | 说明 |
|---|:---|:---:|
| void | acquire() |从此信号量获取一个许可,在提供一个许可前一直将线程阻塞，否则线程被中断 |
| int | availablePermits() | 返回此信号量中当前可用的许可数 |
| void | release() | 释放一个许可,将其返回给信号量 |
| boolean | tryAcquire() | 仅在调用时此信号量存在一个可用许可,才从信号量获取许可 |

#### 示例
_说明：大家排队上厕所，厕所只有两个位置，来了10个人需要排队_

    import java.util.concurrent.ExecutorService;
	import java.util.concurrent.Executors;
	import java.util.concurrent.Semaphore;
	
	public class MySemaphore extends Thread {
		Semaphore position;
		private int id;
	
		public MySemaphore(int i, Semaphore s) {
			this.id = i;
			this.position = s;
		}
	
		public void run() {
			try {
				// 判断信号量中当前可用的许可数
				if (position.availablePermits() > 0) {
					System.out.println("顾客[" + this.id + "]进入厕所，有空位");
				} else {
					System.out.println("顾客[" + this.id + "]进入厕所，没空位，排队");
				}
				// 获取一个许可,在提供一个许可前一直将线程阻塞，否则线程被中断
				position.acquire(); 
				System.out.println("顾客[" + this.id + "]获得坑位");
				Thread.sleep((int) (Math.random() * 1000));
				System.out.println("顾客[" + this.id + "]使用完毕");
				// 释放一个许可，将其返回给信号量
				position.release();
			} catch (Exception e) {
				e.printStackTrace();
			}
		}
	
		public static void main(String args[]) {
			ExecutorService list = Executors.newCachedThreadPool();
			Semaphore position = new Semaphore(2);
			for (int i = 0; i < 10; i++) {
				list.submit(new MySemaphore(i + 1, position));
			}
			list.shutdown();
			position.acquireUninterruptibly(2);
			System.out.println("使用完毕，需要清扫了");
			position.release(2);
		}
	}