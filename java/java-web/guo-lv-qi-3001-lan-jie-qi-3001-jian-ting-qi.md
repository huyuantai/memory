启动顺序
监听器->过滤器->拦截器

监听器是采用观察者模式实现的，和过滤器和拦截器可以拦截或者中断流程不同的是，监听器只是负责监听，收集信息(事件)， 但是监听器并不会干预这个流程，因为有些事件都是异步监听的，比如消息订阅这些，你只能收到”消息”，根本无法干涉业务流程的进程



# 拦截器 vs 过滤器
1、拦截器是基于java的反射机制的，而过滤器是基于函数回调 
2、过滤器依赖与servlet容器，而拦截器不依赖与servlet容器 
3、拦截器只能对action请求起作用，而过滤器则可以对几乎所有的请求起作用 
4、拦截器可以访问action上下文、值栈里的对象，而过滤器不能 
5、在action的生命周期中，拦截器可以多次被调用，而过滤器只能在容器初始化时被调用一次 


# 过滤器 （回调方式：FilterChain调用Filter，Filter又重新调用FilterChain）

过滤器：https://zsr.github.io/2017/11/15/tomcat-filter%E5%88%86%E6%9E%90/
https://blog.csdn.net/jijianshuai/article/details/77878673
![](/assets/20180411154043618)
![](/assets/0_1328601574JQZh.gif)

* 每一请求就创建一个fiterChain，并将对应的servlet设置到fiterChain中
还将该请求对应的fiter添加到fiter数组中
* fiterChain被调用，执行fiterChain.doFiter


* Tomcat的Filter主要由Filter、FilterChain组成，FilterChain含Filter数组
* 当执行FilterChain的doFilter，FilterChain调用第一个Filter的doFilter
* 当第一个filter做完过滤操作后，它又会调用filterchain的doFilter方法，
* 此时filterchain的当前filter已变为第二个filter，第二个filter又执行dofilter方法，直到Fiter执行完，再执行Servlet 的service方法

# 滤器和拦截器实现的方式的不同. 
> Filter是利用了方法的调用(入栈出栈)完成整个流程, 而Interceptor是利用了for循环完成了整个流程.

> Filter的实现比较占用栈空间, 在Filter多的情况下可能会有栈溢出的风险存在.
Interceptor的实现逻辑更加的清晰简单

# 支持的范围
> Filter组件更加的通用, 只要支持java servlet的容器都可以使用, 而Interceptor必须依赖于Spring

# 顺序
> Filter的优先级是高于Interceptor, 即请求是先到Filter再到Interceptor的, 因为Interceptor的实现主体还是一个servlet