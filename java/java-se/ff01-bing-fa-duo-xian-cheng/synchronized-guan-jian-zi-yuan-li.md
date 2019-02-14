# 实现原理
JVM 是通过进入、退出对象监视器( Monitor )来实现对方法、同步块的同步的

实现是在编译之后在同步方法调用前加入一个 monitor.enter 指令，在退出方法和异常处插入 monitor.exit 的指令

![](/assets/monitor.jpg)


## 代码示例
```java
public static void main(String[] args) {
        synchronized (Synchronize.class){
            System.out.println("Synchronize");
        }
    }
```

## 使用 javap -c Synchronize 可以查看编译之后的具体信息
![](/assets/monitor_comp.png)




- synchronize(this){ // code } 

- synchronize(MyClass.class){ //code }

this - is the reference to particular this instance of class,

MyClass.class - is the reference to MyClass description object.

此同步块的不同之处在于，第一个将同步与MyC类实例具体地处理的所有线程
而第二个线程将同步所有线程，而独立于调用该方法的对象

