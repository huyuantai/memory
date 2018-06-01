
# 实现多线程的方式：
1.继承Thread类
2.实现Runnable接口
3.实现Callable接口
4.使用ExecutorService、Callable、Future实现有返回结果的多线程

# 同步有几种实现
synchronized同步方法/同步块
wait与notify（与锁结合） 
Lock/ReenreantLock
线程封闭/局部变量
ThreadLocal
voliate 单变量


# wait与notify+锁  
生产者/消费者
join() A线程等待 B线程执行完后 再执行