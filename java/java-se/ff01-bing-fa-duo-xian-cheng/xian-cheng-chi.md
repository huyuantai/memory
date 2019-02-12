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
一般说来，大家认为线程池的大小经验值应该这样设置：（其中N为CPU的个数）
如果是CPU密集型应用，则线程池大小设置为N+1
如果是IO密集型应用，则线程池大小设置为2N+1

如果一台服务器上只部署这一个应用并且只有这一个线程池，那么这种估算或许合理，具体还需自行测试验证。但是，IO优化中，这样的估算公式可能更适合：最佳线程数目 = （（线程等待时间+线程CPU时间）/线程CPU时间 ）* CPU数目因为很显然，线程等待时间所占比例越高，需要越多线程。线程CPU时间所占比例越高，需要越少线程。下面举个例子：比如平均每个线程CPU运行时间为0.5s，而线程等待时间（非CPU运行时间，比如IO）为1.5s，CPU核心数为8，那么根据上面这个公式估算得到：((0.5+1.5)/0.5)*8=32。这个公式进一步转化为：最佳线程数目 = （线程等待时间与线程CPU时间之比 + 1）* CPU数目

作者：zhangya
链接：https://www.zhihu.com/question/38128980/answer/75041041
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
