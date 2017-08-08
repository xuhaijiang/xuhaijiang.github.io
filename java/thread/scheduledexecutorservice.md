#### ScheduledExecutorService 在给定的延迟后运行或定期执行的命令
一个 ExecutorService，可安排在给定的延迟后运行或定期执行的命令。



#### API
| 返回 | 方法 | 说明 |
|:---:|:---|:---|
| ScheduledFuture<?> | schedule(Runnable command,long delay,TimeUnit unit) | 创建并执行在给定延迟后启用的一次性操作。 |
| ScheduledFuture<?> | scheduleAtFixedRate(Runnable command,long initialDelay,long period,TimeUnit unit) | 创建并执行一个在给定初始延迟后首次启动的定期操作，后续操作具有给定的周期，也就是将在 initialDelay 后开始执行，接着在 initialDelay + 2 * period后执行，依次类推。|
| ScheduledFuture<?> | scheduleWithFixedDelay(Runnable command,long initialDelay,long delay,TimeUnit unit) | 创建并执行一个在给定初始延迟后首次启用的定期操作，随后，在每一次执行终止和下一次执行开始之间都存在给定的延迟。 |



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