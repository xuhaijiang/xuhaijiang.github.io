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
    import java.text.SimpleDateFormat;
	import java.util.Date;
	import java.util.concurrent.BrokenBarrierException;
	import java.util.concurrent.CyclicBarrier;
	import java.util.concurrent.ExecutorService;
	import java.util.concurrent.Executors;
	
	public class TestCyclicBarrier {
		// 徒步需要的时间: 北京, 上海, 广州, 深圳, 杭州
		private static int[] timeWalk = { 5, 8, 15, 15, 10 };
		// 自驾游
		private static int[] timeSelf = { 1, 3, 4, 4, 5 };
		// 旅游大巴
		private static int[] timeBus = { 2, 4, 6, 6, 7 };
	
		static String now() {
			SimpleDateFormat sdf = new SimpleDateFormat("HH:mm:ss");
			return sdf.format(new Date()) + ": ";
		}
	
		static class Tour implements Runnable {
			private int[] times;
			private CyclicBarrier barrier;
			private String tourName;
	
			public Tour(CyclicBarrier barrier, String tourName, int[] times) {
				this.times = times;
				this.tourName = tourName;
				this.barrier = barrier;
			}
	
			public void run() {
				try {
					Thread.sleep(times[0] * 1000);
					System.out.println(now() + tourName + " 到达    北京");
					barrier.await();
					Thread.sleep(times[1] * 1000);
					System.out.println(now() + tourName + " 到达    上海");
					barrier.await();
					Thread.sleep(times[2] * 1000);
					System.out.println(now() + tourName + " 到达    广州");
					barrier.await();
					Thread.sleep(times[3] * 1000);
					System.out.println(now() + tourName + " 到达    深圳");
					barrier.await();
					Thread.sleep(times[4] * 1000);
					System.out.println(now() + tourName + " 到达    杭州");
					barrier.await();
				} catch (InterruptedException e) {
				} catch (BrokenBarrierException e) {
				}
			}
		}
	
		public static void main(String[] args) {
			// 三个旅行团
			CyclicBarrier barrier = new CyclicBarrier(3);
			ExecutorService exec = Executors.newFixedThreadPool(3);
			exec.submit(new Tour(barrier, "徒步游", timeWalk));
			exec.submit(new Tour(barrier, "自驾游", timeSelf));
			// 当我们把下面的这段代码注释后，会发现，程序阻塞了，无法继续运行下去。
			exec.submit(new Tour(barrier, "旅游大巴", timeBus));
			exec.shutdown();
		}
	}