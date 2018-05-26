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
2.（Spring容器的创建）web容器启动时，web.xml的contextLoaderListener被触发，contextInitialized方法被调用，在这方法创建WebApplicationContext（实现类XmlWebApplicationContext）这就是spring的IoC容器，
这个WebApplicationContext容器被放到ServletContext中，便于获取
接着IOC容器通过scan扫描Bean定义信息存到BeanDefinition，并将这些
BeanDefinition,放到Map中，如下所示：

```java
private final Map<String, BeanDefinition> beanDefinitionMap = new ConcurrentHashMap<String, BeanDefinition>();
this.beanDefinitionMap.put(beanName, beanDefinition); 
```
调用getBean，对读取BeanDefinition，对Bean进行创建初始化
（先从缓存中获取getSingo，没有再用工厂创建，通过反射技术）

3.（Spring MVC容器的创建）contextLoaderListener执行完，web.xml中的DispatcherServlet被创建，接着在DispatcherServlet创建Spring MVC容器
Spring MVC容器会先查看是否存在根容器即（上一步的Spring 容器）
如果存在，作为Spring MVC容器的父容器，然后创建Spring MVC容器
如果不存在，则先创建根WebApplicationContext（即XmlWebApplicationContext）容器
创建完后，Spring MVC容器也被放到ServletContext中，便于获取

接着创建Bean，如Controller，HandlerMapping，HandlerAdapter
等等


IOC容器
基本原理其实就是通过反射解析类及其类的各种信息，包括构造器、方法及其参数，属性。
然后将其封装成bean定义信息类、constructor信息类、method信息类、property信息类，
最终放在一个map里，也就是所谓的container，池等等，其实就是个map。。汗。。。。

当你写好配置文件，启动项目后，框架会先按照你的配置文件找到那个要scan的包，
然后解析包里面的所有类，找到所有含有@bean，@service等注解的类，利用反射解析它们，
包括解析构造器，方法，属性等等，然后封装成各种信息类放到一个map里。每当你需要一个bean的时候，
框架就会从container找是不是有这个类的定义啊？如果找到则通过构造器new出来（这就是控制反转，
不用你new,框架帮你new），再在这个类找是不是有要注入的属性或者方法，比如标有@autowired的属性，
如果有则还是到container找对应的解析类，new出对象，并通过之前解析出来的信息类找到setter方法，
然后用该方法注入对象（这就是依赖注入）。如果其中有一个类container里没找到，则抛出异常，
比如常见的spring无法找到该类定义，无法wire的异常。还有就是嵌套bean则用了一下递归，
container会放到servletcontext里面，每次reQuest从servletcontext找这个container即可，
不用多次解析类定义。如果bean的scope是singleton，则会重用这个bean不再重新创建，
将这个bean放到一个map里，
每次用都先从这个map里面找。如果scope是session，则该bean会放到session里面

# Spring MVC 流程

# Spring RequestMapping
Spring MVC被创建时，会先创建RequestMappingHandlerMapping，然后scan扫描Contrllor，@RequestMapping的信息封装成RequestMappingInfo对象，


