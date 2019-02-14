# 实现原理
JVM 是通过进入、退出对象监视器( Monitor )来实现对方法、同步块的同步的

实现是在编译之后在同步方法调用前加入一个 monitor.enter 指令，在退出方法和异常处插入 monitor.exit 的指令

![](/assets/monitor.jpg)

``` java
public static void main(String[] args) {
        synchronized (Synchronize.class){
            System.out.println("Synchronize");
        }
    }
```

