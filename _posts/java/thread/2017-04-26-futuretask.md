---
layout: post
title: FutureTask java异步计算
date: 2017-04-26 17:33:17 +0800
category : 技术文档
tag :
- java
- thread
---
* content
{:toc}

#### FutureTask
可取消的异步计算。利用开始和取消计算的方法、查询计算是否完成的方法和获取计算结果的方法，此类提供了对 Future 的基本实现。仅在计算完成时才能获取结果；如果计算尚未完成，则阻塞 get 方法。一旦计算完成，就不能再重新开始或取消计算。

FutureTask 有点类似Runnable，都可以通过Thread来启动，不过FutureTask可以返回执行完毕的数据，并且FutureTask的get方法支持阻塞。

由于：FutureTask可以返回执行完毕的数据，并且FutureTask的get方法支持阻塞这两个特性，我们可以用来预先加载一些可能用到资源，然后要用的时候，调用get方法获取（如果资源加载完，直接返回；否则继续等待其加载完成）。

#### 示例
    import java.util.concurrent.Callable;
	import java.util.concurrent.ExecutionException;
	import java.util.concurrent.FutureTask;
	
	/**
	 * 使用FutureTask模拟预加载下一页图书的内容
	 */
	public class BookInstance {
	
		// 当前的页码
		private volatile int currentPage = 1;
	
		// 异步的任务获取当前页的内容
		FutureTask<String> futureTask = new FutureTask<String>(new Callable<String>() {
			public String call() throws Exception {
				return loadDataFromNet();
			}
		});
	
		// 实例化一本书，并传入当前读到的页码
		public BookInstance(int currentPage) {
			this.currentPage = currentPage;
			
			// 直接启动线程获取当前页码内容
			Thread thread = new Thread(futureTask);
			thread.start();
		}
	
		// 获取当前页的内容
		public String getCurrentPageContent() throws InterruptedException, ExecutionException {
			String con = futureTask.get();
			this.currentPage = currentPage + 1;
			Thread thread = new Thread(futureTask = new FutureTask<String>(new Callable<String>() {
				public String call() throws Exception {
					return loadDataFromNet();
				}
			}));
			thread.start();
			return con;
		}
	
		// 根据页码从网络抓取数据
		private String loadDataFromNet() throws InterruptedException {
			Thread.sleep(1000);
			return "Page " + this.currentPage + " : the content ....";
	
		}
	
		public static void main(String[] args) throws InterruptedException, ExecutionException {
			BookInstance instance = new BookInstance(1);
			for (int i = 0; i < 10; i++) {
				long start = System.currentTimeMillis();
				String content = instance.getCurrentPageContent();
				System.out.println("[1秒阅读时间]read:" + content);
				Thread.sleep(1000);
				System.out.println(System.currentTimeMillis() - start);
			}
	
		}
	}