http://blog.163.com/wm_at163/blog/static/132173490201242984518354/
https://segmentfault.com/a/1190000008394155
https://www.cnblogs.com/dolphin0520/p/3932921.html
http://www.cnblogs.com/dolphin0520/p/3932934.html


线程池监控超时
http://www.voidcn.com/article/p-vfishuxg-brg.html
http://matrix-lee.iteye.com/blog/2144630
https://blog.csdn.net/dj2442945707/article/details/56292413



## （内存不足）和线程泄漏

队列太多任务oom
线程数太大 oom

1） FixedThreadPool 和 SingleThreadPool :	允许的请求队列长度为 Integer.MAX_VALUE ，可能会堆积大量的请求，从而导致 OOM 。

2） CachedThreadPool 和 ScheduledThreadPool :	允许的创建线程数量为 Integer.MAX_VALUE ，可能会创建大量的线程，从而导致 OOM 

Executor框架实现了工作单元与执行单元的分离。


# Executor 类图
![](/assets/776259-20160426201537486-1323529733.png)

Executor：一个接口，其定义了一个接收Runnable对象的方法executor，其方法签名为executor(Runnable command),
 
ExecutorService：是一个比Executor使用更广泛的子类接口，其提供了生命周期管理的方法，以及可跟踪一个或多个异步任务执行状况返回Future的方法
 
AbstractExecutorService：ExecutorService执行方法的默认实现
 
ScheduledExecutorService：一个可定时调度任务的接口
 
ScheduledThreadPoolExecutor：ScheduledExecutorService的实现，一个可定时调度任务的线程池
 
ThreadPoolExecutor：线程池，可以通过调用Executors以下静态工厂方法来创建线程池并返回一个ExecutorService对象


# 四种线程池
> 记忆：单个固定的缓存，定时（更新）

newSingleThreadExecutor:一个任务一个任务执行的场景
newFixedThreadPool:执行长期的任务，性能好很多
newCachedThreadPool:执行很多短期异步的小程序或者负载较轻的服务器

Executors.newCachedThreadPool()就使用了SynchronousQueue，这个线程池根据需要（新任务到来时）创建新的线程，如果有空闲线程则会重复使用，线程空闲了60秒后会被回收

newScheduledThreadPool：周期性执行任务的场景

FixedThreadPool、newSingleThreadExecutor 都是有无界的队列，保证新任务都能够放入队列，不会被拒绝；缺点：当处理任务无限等待的时候会造成内存问题。


handle:定义处理被拒绝任务的策略，默认使用ThreadPoolExecutor.AbortPolicy,任务被拒绝时将抛出RejectExecutorException



# 队列
无界队列、有界队列、同步队列
无界队列：LinkedBlockingQueue
有界队列：有界的LinkedBlockingQueue、有界的ArrayBlockingQueue

同步队列：SynchronousQueue 大小为1， 生产者和消费者互相等待对方，握手，然后一起离开，不存数据，不能调用peek()方法来看队列中是否有数据元素，因为数据元素只有当你试着取走的时候才可能存在


# 拒绝策略 RejectedExecutionHandler
抛异常、不处理、调用者线程、丢弃队列最近任务再执行
> 记忆：在调用者线程中抛异常 不处理、丢弃队列最近任务再执行


AbortPolicy：直接抛出异常。

CallerRunsPolicy：只用调用者所在线程来运行任务。

DiscardOldestPolicy：丢弃队列里最近的一个任务，并执行当前任务。

DiscardPolicy：不处理，丢弃掉。


# 线程池的最大线程数目根据什么确定
根据服务器的CPU核数
