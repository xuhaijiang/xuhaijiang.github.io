#### CompletionService 批量执行任务的服务
CompletionService接口提供了可以操作异步任务的功能，其唯一实现的API为ExecutorCompletionService。

CompletionService可实现生产者提交任务和消费者获取结果的解耦，生产者和消费者都不用关心任务的完成顺序，由CompletionService来保证，消费者一定是按照任务完成的先后顺序来获取执行结果。

#### API

| 返回 | 方法 | 说明 |
|---|:---:|:---|
| Future<V> | submit(Callable<V> task) | 提交任务，并获取任务执行结果的句柄。 |
| Future<V> | take() | 获取并移除第一个执行完成的任务，阻塞，直到有任务返回。 |
| Future<V> | poll() | 同步操作，获取并移除第一已经完成的任务，否则返回null。 |



#### 示例
    import java.util.ArrayList;
	import java.util.List;
	import java.util.concurrent.BlockingQueue;
	import java.util.concurrent.Callable;
	import java.util.concurrent.CompletionService;
	import java.util.concurrent.ExecutionException;
	import java.util.concurrent.ExecutorCompletionService;
	import java.util.concurrent.ExecutorService;
	import java.util.concurrent.Executors;
	import java.util.concurrent.Future;
	import java.util.concurrent.LinkedBlockingDeque;
	
	public class MyCompletionService implements Callable<String> {
		private String id;
	
		public MyCompletionService(String i) {
			this.id = i;
		}
	
		public static void main(String[] args) throws Exception {
			System.out.println("syn  start ");
			syn();
			System.out.println("syn  end ");
			System.out.println("aSyn  start ");
			aSyn();
			System.out.println("aSyn  end ");
		}
	
		public String call() throws Exception {
			Integer time = (int) (Math.random() * 1000);
			try {
				System.out.println(this.id + " start");
				Thread.sleep(time);
				System.out.println(this.id + " end");
			} catch (Exception e) {
				e.printStackTrace();
			}
			return this.id + ":" + time;
		}
	
		public static List<Future<String>> syn() {
			try {
				ExecutorService exec = Executors.newCachedThreadPool();
				// 任务集合
				List<Callable<String>> tasks = new ArrayList<Callable<String>>();
				for (int i = 0; i < 10; i++) {
					// 组装任务
					exec.submit(new MyCompletionService("syn " + i));
				}
				// 同步执行任务
				List<Future<String>> results = exec.invokeAll(tasks);
				exec.shutdown();
				return results;
			} catch (InterruptedException e2) {
				e2.printStackTrace();
				return null;
			}
		}
	
		public static List<Future<String>> aSyn() {
	
			StringBuffer results = new StringBuffer();
			try {
				ExecutorService exec = Executors.newSingleThreadExecutor();
				// 阻塞队列
				BlockingQueue<Future<String>> queue = new LinkedBlockingDeque<Future<String>>(10);
	
				// 实例化CompletionService
				CompletionService<String> completionService = new ExecutorCompletionService<String>(exec, queue);
	
				// 返回结果集
				List<Future<String>> resultsFutures = new ArrayList<Future<String>>();
				for (int i = 0; i < 10; i++) {
					// 创建任务
					completionService.submit(new MyCompletionService("aSyn " + i));
					// 返回结果，谁最先执行完成，谁先返回
					resultsFutures.add(completionService.take());
				}
	
				exec.shutdown();
				// 计算结果集
				if (null != resultsFutures && resultsFutures.size() > 0) {
					for (Future<String> future : resultsFutures) {
						String str = future.get();
						results.append(str);
					}
				}
				return resultsFutures;
	
			} catch (InterruptedException e1) {
				e1.printStackTrace();
				return null;
			} catch (ExecutionException e) {
				e.printStackTrace();
				return null;
			}
		}
	}


#### 注意区别
##### CompletionService：Executor + BlockingQueue 
最先执行完成的直接返回，并不需要按任务提交的顺序执行

##### ExecutorService.invokeAll
ExecutorService的invokeAll方法也能批量执行任务，并批量返回结果，但是呢，有个缺点，必须等待所有的任务执行完成后统一返回。


