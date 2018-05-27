成员：
切面（Aspect） ：官方的抽象定义为“一个关注点的模块化，这个关注点可能会横切多个对象”。
连接点（Joinpoint） ：程序执行过程中的某一行为。
通知（Advice） ：“切面”对于某个“连接点”所产生的动作。
切入点（Pointcut） ：匹配连接点的断言，在AOP中通知和一个切入点表达式关联。
目标对象（Target Object） ：被一个或者多个切面所通知的对象。
AOP代理（AOP Proxy） 在Spring AOP中有两种代理方式，JDK动态代理和CGLIB代理