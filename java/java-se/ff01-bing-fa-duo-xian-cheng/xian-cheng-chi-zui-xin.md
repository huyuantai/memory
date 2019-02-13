https://github.com/crossoverJie/JCSprout/blob/master/MD/ThreadPoolExecutor.md
https://zhuanlan.zhihu.com/p/33264000
同步错误和死锁，资源不足和线程泄漏
http://blog.163.com/wm_at163/blog/static/132173490201242984518354/

# 为什么使用线程池
- 减少线程创建和销毁线程,减少系统资源的开销
- 减少线程之间过度切换
- 解耦，线程的创建于执行分开，方便维护
- 提高速度,请求到来时，由于线程已创建，故直接执行任务，提高了响应速度


# 线程池原理流程
线程池角色：多个工作线程 和 一个阻塞队列
- 工作线程 
运行中的线程，不断从阻塞队列领取任务执行
- 阻塞队列 
存储工作线程来不及处理的任务


# 队列
无界队列、有界队列、同步队列
无界队列：LinkedBlockingQueue
有界队列：有界的LinkedBlockingQueue、有界的ArrayBlockingQueue

同步队列：SynchronousQueue 大小为1， 生产者和消费者互相等待对方，握手，然后一起离开，
不存数据，不能调用peek()方法来看队列中是否有数据元素，因为数据元素只有当你试着取走的时候才可能存在


# 拒绝策略 RejectedExecutionHandler
- 不处理的：抛异常、不处理、
- 处理的：调用者线程、丢弃队列最近任务再执行

AbortPolicy：直接抛出异常
DiscardPolicy：不处理，丢弃掉

CallerRunsPolicy：只用调用者所在线程来运行任务
DiscardOldestPolicy：丢弃队列里最近的一个任务，并执行当前任务

# 原理流程
核心线程数-最大线程数-队列满-饱和策略
创建线程-进队列-创建线程-饱和策略           

> x<核心线程数:创建线程
核心线程数<x<最大线程数 且队列不满:进队列
核心线程数<x<最大线程数 且队列满：创建线程 
最大线程数<x 且队列满 ：饱和策略


# keepAliveTime：线程空闲时间
- 当线程空闲时间达到keepAliveTime时，线程会退出，直到线程数量=corePoolSize
- 如果allowCoreThreadTimeout=true，则会直到线程数量=0


# 线程池分类
## 四种线程池
> 记忆：单个固定的缓存，定时（更新）

- 固定线程数、无界队列LinkedBlockingQueue、keepAliveTime为0
newSingleThreadExecutor:一个任务一个任务执行的场景
newFixedThreadPool:执行长期的任务，性能好很多

- 无限线程数、固定队列、keepAliveTime为60
newCachedThreadPool:执行很多短期异步的小程序或者负载较轻的服务器（固定队列大小为1：SynchronousQueue）
newScheduledThreadPool：周期性执行任务的场景

FixedThreadPool、newSingleThreadExecutor 都是有无界的队列，保证新任务都能够放入队列，不会被拒绝；缺点：当处理任务无限等待的时候会造成内存问题。
Executors.newCachedThreadPool()就使用了SynchronousQueue，这个线程池根据需要（新任务到来且没有空闲线程时）创建新的线程，如果有空闲线程则会重复使用，线程空闲了60秒后会被回收


各自特征及应用场景

# 优雅的关闭线程池
- shutdown() 执行后停止接受新任务，会把队列的任务执行完毕。
- shutdownNow() 也是停止接受新任务，但会中断所有的任务，将线程池状态变为 stop。

```java
        long start = System.currentTimeMillis();
        for (int i = 0; i <= 5; i++) {
            pool.execute(new Job());
        }

        pool.shutdown();

        while (!pool.awaitTermination(1, TimeUnit.SECONDS)) {
            LOGGER.info("线程还在执行。。。");
        }
        long end = System.currentTimeMillis();
        LOGGER.info("一共处理了【{}】", (end - start));
```
# 如何使用（调优与参数计算、监控定位错误）
## 错误使用引起oom 
- FixedThreadPool 和 SingleThreadPool :允许的请求队列长度为 Integer.MAX_VALUE ，可能会堆积大量的请求，从而导致 OOM 。
- CachedThreadPool 和 ScheduledThreadPool :允许的创建线程数量为 Integer.MAX_VALUE ，可能会创建大量的线程，从而导致 OOM 


# 设置参数
- tasks ：每秒的任务数，假设为500~1000
- taskcost：每个任务花费时间，假设为0.1s
- responsetime：系统允许容忍的最大响应时间，假设为1s

- corePoolSize = 每秒需要多少个线程处理？ 
* threadcount = tasks/(1/taskcost) =tasks*taskcout =  (500~1000)*0.1 = 50~100 个线程。
  corePoolSize设置应该大于50
* 根据8020原则，如果80%的每秒任务数小于800，那么corePoolSize设置为80即可

- queueCapacity = (coreSizePool/taskcost)*responsetime
* 计算可得 queueCapacity = 80/0.1*1 = 80。意思是队列里的线程可以等待1s，超过了的需要新开线程来执行
* 切记不能设置为Integer.MAX_VALUE，这样队列会很大，线程数只会保持在corePoolSize大小，当任务陡增时，不能新开线程来执行，响应时间会随之陡增。

- maxPoolSize = (max(tasks)- queueCapacity)/(1/taskcost)
* 计算可得 maxPoolSize = (1000-80)/10 = 92

* （最大任务数-队列容量）/每个线程每秒处理能力 = 最大线程数
- rejectedExecutionHandler：根据具体情况来决定，任务不重要可丢弃，任务重要则要利用一些缓冲机制来处理
- keepAliveTime和allowCoreThreadTimeout采用默认通常能满足


# 线程池的异常处理
百度云盘-书籍-java目录中的java高并发设计.pdf -- 3.2.8节 113页多线程堆栈信息


