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
2.web容器启动时，web.xml的contextLoaderListener被触发，contextInitialized方法被调用，在这方法创建WebApplicationContext（实现类XmlWebApplicationContext）这就是spring的IoC容器，
这个WebApplicationContext容器被放到ServletContext中，便于获取
接着IOC容器通过scan扫描Bean定义信息存到BeanDefinition，并将这些
BeanDefinition,放到Map中，如下所示：

```java
private final Map<String, BeanDefinition> beanDefinitionMap = new ConcurrentHashMap<String, BeanDefinition>();
this.beanDefinitionMap.put(beanName, beanDefinition); 
```
调用getBean，对Bean进行创建初始化



