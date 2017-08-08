#### CountDownLatch 简单的开/关锁存器
CountDownLatch如其所写，是一个倒计数的锁存器，当计数减至0时触发特定的事件。利用这种特性，可以让主线程等待子线程的结束。
- 计数到达零之前，await 方法会一直受阻塞
- 计数无法被重置
- 一个简单的开/关锁存器

#### 场景
- 最大的并行性
  - 例如：有时我们想同时启动多个线程，实现最大程度的并行性。
- 开始执行前等待n个线程完成各自任务
  - 例如：应用程序启动类要确保在处理用户请求前，所有N个外部系统已经启动和运行了。

#### API
| 返回 | 方法 | 说明 |
|:---:|:---|:---|
| void | await() | 使当前线程在锁存器计数至0之前一直等待，除非线程被中断。 |
| void | countDown() | 递减锁存器的技术，如果技术到达0，则释放所有等待的线程。如果当前计数大于0，则将技术减少。 |
| long | getCount() | 返回当前计数。 |


#### 示例
    import java.util.concurrent.CountDownLatch;
	import java.util.concurrent.ExecutorService;
	import java.util.concurrent.Executors;
	
	public class TestCountDownLatch {
		public static void main(String[] args) throws InterruptedException {
			// 开始的倒数锁
			final CountDownLatch begin = new CountDownLatch(1);
			// 结束的倒数锁
			final CountDownLatch end = new CountDownLatch(10);
			// 十名选手
			final ExecutorService exec = Executors.newFixedThreadPool(10);
	
			for (int index = 0; index < 10; index++) {
				final int NO = index + 1;
				Runnable run = new Runnable() {
					public void run() {
						try {
							// 一直阻塞,等待发令枪开跑
							begin.await();
							Thread.sleep((long) (Math.random() * 10000));
							System.out.println("No." + NO + " arrived");
						} catch (InterruptedException e) {
						} finally {
							// 选手到达终点
							end.countDown();
						}
					}
				};
				exec.submit(run);
			}
			System.out.println("Game Start");
			// 发令枪开跑
			begin.countDown();
			
			// 等待全部选手到达终点
			end.await();
			System.out.println("Game Over");
			exec.shutdown();
		}
	}



