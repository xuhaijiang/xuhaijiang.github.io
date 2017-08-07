#### CompletionService 异步任务的服务





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
	
		// 无序执行
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
	
		// 按创建顺序有序执行
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
					// 返回结果
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