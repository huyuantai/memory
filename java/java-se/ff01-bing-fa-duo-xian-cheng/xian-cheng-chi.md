四种线程池
newSingleThreadExecutor
newFixedThreadPool

newCachedThreadPool

newScheduledThreadPool


# 拒绝策略
AbortPolicy：直接抛出异常。

CallerRunsPolicy：只用调用者所在线程来运行任务。

DiscardOldestPolicy：丢弃队列里最近的一个任务，并执行当前任务。

DiscardPolicy：不处理，丢弃掉。