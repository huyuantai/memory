
# 拦截器 vs 过滤器
1、拦截器是基于java的反射机制的，而过滤器是基于函数回调 
2、过滤器依赖与servlet容器，而拦截器不依赖与servlet容器 
3、拦截器只能对action请求起作用，而过滤器则可以对几乎所有的请求起作用 
4、拦截器可以访问action上下文、值栈里的对象，而过滤器不能 
5、在action的生命周期中，拦截器可以多次被调用，而过滤器只能在容器初始化时被调用一次 


# 过滤器
![](/assets/20180411154043618)

* Tomcat的Filter主要由Filter、FilterChain组成，
FilterChain含Filter数组.当Wrapper执行FilterChain的doFilter(request,response)方法时，
FilterChain首先调用第一个Filter的doFilter(request,response,filterchain)方法，

当第一个filter做完过滤操作后，它又会调用filterchain的doFilter方法，此时filterchain的当前filter已变为第二个filter，第二个filter又执行dofilter方法，依此类推，直至所有过滤器都执行完毕 
