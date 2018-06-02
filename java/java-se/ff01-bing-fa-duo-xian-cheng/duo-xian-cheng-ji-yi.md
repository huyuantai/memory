| |  |  |
| :--- | :--- | :--- |
| synchronized    | BLOCKED |waiting for monitor|
| sleep\(\) | TIMED\_WAITING   | waiting on condition |
| wait\(\)| WAITING (on object monitor) |  |




synchronized               



  
sleep\(\)        TIMED\_WAITING  


# 进程和线程有什么区别

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
join\(\) A线程等待 B线程执行完后 再执行

wait\(\):使一个线程处于等待状态，并且释放所持有的对象的lock。   
sleep\(\):使一个正在运行的线程处于睡眠状态，是一个静态方法，调用此方法要捕捉InterruptedException异常。   
notify\(\):唤醒一个处于等待状态的线程，注意的是在调用此方法的时候，并不能确切的唤醒某一个等待状态的线程，而是由JVM确定唤醒哪个线程，而且不是按优先级。   
notityAll\(\):唤醒所有处入等待状态的线程，注意并不是给所有唤醒线程一个对象的锁，而是让它们竞争。

面试官：当一个线程进入一个对象的一个synchronized方法后，其它线程是否可进入此对象的其它方法?

我：分几种情况：  
     1.其他方法前是否加了synchronized关键字，如果没加，则能。  
     2.如果这个方法内部调用了wait，则可以进入其他synchronized方法。  
     3.如果其他个方法都加了synchronized关键字，并且内部没有调用wait，则不能。  
     4.如果其他方法是static，它用的同步锁是当前类的字节码，与非静态的方法不能同步，因为非静态的方法用的是this。（这一点非常重要！static方法和非静态方法用的监视器是不一样的！！一个是this, 一个是当前类的字节码！）

