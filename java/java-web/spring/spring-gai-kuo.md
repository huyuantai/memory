# 流程
IOC
AOP
MVC
Mapping

# IOC（存BeanDefinition到Map，从Map中获取BeanDefinition 反射实例化）
1.AbstractApplicationContext的refresh()，将Bean信息转化为BeanDefinition，存储到Map中
2.refresh中finishBeanFactoryInitialization()的getBean()，从Map中获取
BeanDefinition，通过反射实例化

转化：Xml信息-->Dodument-->BeanDefinition
BeanName的存储在List中，BeanDefinition的存储在Map中

# AOP
1.读取xml时用delegate.parseCustomElement(ele)方法解析，也是转成BeanDefinition放到Map中，
2.getBean()返回的是代理对象

>org.springframework.aop.config.internalAutoProxyCreator
org.springframework.aop.aspectj.AspectJPointcutAdvisor


# MVC
DispatcherServlet
HandlerMapping 获取HandlerExecutionChain（Handler对象以及Handler对象对应的拦截器）
HandlerAdapter ModelAndView
ModelAndView 选择 ViewResolver
的preHandler(...)方法）
4. 提取Request中的模型数据，填充Handler入参，开始执行Handler（Controller)。 在填充Handler的入参过程中，根据你的配置，Spring将帮你
做一些额外的工作：
HttpMessageConveter： 将请求消息（如Json、xml等数据）转换成一个对象，将对象转换为指定的响应信息数据转换：对请求消息进行数据转
换。如String转换成Integer、Double等数据根式化：对请求消息进行数据格式化。 如将字符串转换成格式化数字或格式化日期等数据验证： 验证数
据的有效性（长度、格式等），验证结果存储到BindingResult或Error中.
5. Handler执行完成后，向DispatcherServlet 返回一个ModelAndView对象；
6. 根据返回的ModelAndView，选择一个适合的ViewResolver（必须是已经注册到Spring容器中的ViewResolver)返回给DispatcherServlet ；
7. ViewResolver 结合Model和View，来渲染视图
8. 将渲染结果返回给客户端




# RequestMappingHandlerMapping 
###### (url->RequestMappingInfo->HandlerMethod)
2个Map
Map1：url->RequestMappingInfo
Map2：RequestMappingInfo->HandlerMethod
用url通过2个Map定位到HandlerMethod，HandlerMethod里面包含Controller、和方法名
