成员：
切面（Aspect） ：官方的抽象定义为“一个关注点的模块化，这个关注点可能会横切多个对象”。（如事务、日志等等）
连接点（Joinpoint） ：程序执行过程中的某一行为，（程序的方法）
通知（Advice） ：“切面”对于某个“连接点”所产生的动作。（拦截后要调用的方法）
切入点（Pointcut） ：匹配连接点的断言，在AOP中通知和一个切入点表达式关联。
（在哪些方法应用切面的调用的方法）
目标对象（Target Object） ：被一个或者多个切面所通知的对象。
AOP代理（AOP Proxy） 在Spring AOP中有两种代理方式，JDK动态代理和CGLIB代理
织入：将通知的方法（增强方法） 植入 目标对象业务方法的过程


# JDK代理 implements  InvocationHandler 

通过newProxyInstance（类加载器、接口、InvocationHandler）获取真正的代理对象
```java
/** 
     * 获取目标对象的代理对象 
     * @return 代理对象 
     */  
    public Object getProxy(){  
        return Proxy.newProxyInstance(Thread.currentThread().getContextClassLoader(),   
                this.target.getClass().getInterfaces(),this);  
    }  
```

# CGLIB代理 implements  MethodInterceptor 


```java
 /**  
     * 创建代理对象  
     *   
     * @param target  
     * @return  
     */    
    public Object getInstance(Object target) {    
        this.target = target;    
        Enhancer enhancer = new Enhancer();    
        enhancer.setSuperclass(this.target.getClass());    
        // 回调方法    
        enhancer.setCallback(this);    
        // 创建代理对象    
        return enhancer.create();    
    }    
```
  