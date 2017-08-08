#### ScheduledExecutorService 在给定的延迟后运行或定期执行的命令
一个 ExecutorService，可安排在给定的延迟后运行或定期执行的命令。



#### API
| 返回 | 方法 | 说明 |
|:---:|:---|:---|
| void | get() | 获取执行结果，这个方法会产生阻塞，会一直等到任务执行完毕才返回。 |
| boolean | isDone() | 任务是否完成，如果完成则返回 true 。|
| boolean | cancel(boolean mayInterruptIfRunning) | 取消任务，如果取消成功则返回 true，如果取消失败则返回 false 。 |



#### 示例
    import static java.util.concurrent.TimeUnit.SECONDS;
	import java.util.Date;
	import java.util.concurrent.Executors;
	import java.util.concurrent.ScheduledExecutorService;
	import java.util.concurrent.ScheduledFuture;
	
	public class TestScheduledThread {
		public static void main(String[] args) {
			final ScheduledExecutorService scheduler = Executors.newScheduledThreadPool(2);
			final Runnable beeper = new Runnable() {
				int count = 0;
	
				public void run() {
					System.out.println(new Date() + " beep " + (++count));
				}
			};
			// 1秒钟后运行，并每隔2秒运行一次
			final ScheduledFuture beeperHandle = scheduler.scheduleAtFixedRate(beeper, 1, 2, SECONDS);
			// 2秒钟后运行，并每次在上次任务运行完后等待5秒后重新运行
			final ScheduledFuture beeperHandle2 = scheduler.scheduleWithFixedDelay(beeper, 2, 5, SECONDS);
			// 30秒后结束关闭任务，并且关闭Scheduler
			scheduler.schedule(new Runnable() {
				public void run() {
					beeperHandle.cancel(true);
					beeperHandle2.cancel(true);
					scheduler.shutdown();
				}
			}, 30, SECONDS);
		}
	}