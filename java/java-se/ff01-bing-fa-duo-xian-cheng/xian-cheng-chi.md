http://blog.163.com/wm_at163/blog/static/132173490201242984518354/
https://segmentfault.com/a/1190000008394155

# 四种线程池
newSingleThreadExecutor
一个任务一个任务执行的场景
newFixedThreadPool
执行长期的任务，性能好很多
newCachedThreadPool
执行很多短期异步的小程序或者负载较轻的服务器
Executors.newCachedThreadPool()就使用了SynchronousQueue，这个线程池根据需要（新任务到来时）创建新的线程，如果有空闲线程则会重复使用，线程空闲了60秒后会被回收



newScheduledThreadPool
适用：周期性执行任务的场景



FixedThreadPool、newSingleThreadExecutor


# 队列
无界队列、有界队列、同步队列
无界队列：LinkedBlockingQueue
有界队列：有界的LinkedBlockingQueue、有界的ArrayBlockingQueue

同步队列：SynchronousQueue 大小为1， 生产者和消费者互相等待对方，握手，然后一起离开，不存数据，不能调用peek()方法来看队列中是否有数据元素，因为数据元素只有当你试着取走的时候才可能存在


# 拒绝策略 RejectedExecutionHandler
AbortPolicy：直接抛出异常。

CallerRunsPolicy：只用调用者所在线程来运行任务。

DiscardOldestPolicy：丢弃队列里最近的一个任务，并执行当前任务。

DiscardPolicy：不处理，丢弃掉。