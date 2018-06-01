CyclicBarrier 是起跑线，N个线程准备好了，再执行
CountDownLatch  N个线程执行完，再主线程执行



# A,B,C 三个线程顺序执行
#### join()方法 （start+join）
```java
Thread t1 = new Thread(new Runner("A"));  
Thread t2 = new Thread(new Runner("B"));  
Thread t3 = new Thread(new Runner("C"));  
t1.start();  
t1.join();  
t2.start();  
t2.join();  
t3.start();  
t3.join();  
```

#### 线程run()内join
```java
定义Thread t1;   
Thread t2 {
   run(){
     t1.join();
   }
} 

Thread t3{
   run(){
     t2.join();
   }
}
t3.start();
t2.start();
t1.start();  
```

# join 的原理
```
获锁
while（条件）
   await();

执行条件成立后
   notifyAll();

```





