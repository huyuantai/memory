# 四种线程池
newSingleThreadExecutor
newFixedThreadPool
执行长期的任务，性能好很多
newCachedThreadPool
执行很多短期异步的小程序或者负载较轻的服务器
newScheduledThreadPool
适用：周期性执行任务的场景

# 拒绝策略
AbortPolicy：直接抛出异常。

CallerRunsPolicy：只用调用者所在线程来运行任务。

DiscardOldestPolicy：丢弃队列里最近的一个任务，并执行当前任务。

DiscardPolicy：不处理，丢弃掉。