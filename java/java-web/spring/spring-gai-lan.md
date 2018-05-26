* Spring 容器
* Spring MVC 容器
* Spring 容器 与 Spring MVC 容器
* Spring IOC
* Spring AOP


> 是什么？
简要流程
具体包括什么
使用案例

# Spring 容器
对非controller的Bean的创建与维护，由Web.xml中的contextLoaderListener加载创建容器，创建一个WebApplicationContext（实现类XmlWebApplicationContext）
>@Component、@service、@repository 等等

# Spring MVC容器
对controller的Bean的创建与维护，由Web.xml中的DispatcherServlet加载创建容器

# Spring 容器 与 Spring MVC 容器
1.web容器提供ServletContext
2.web容器启动时，web.xml的

