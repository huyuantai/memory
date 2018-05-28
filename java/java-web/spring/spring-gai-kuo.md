# 流程
IOC
AOP
MVC
Mapping

# IOC
1.AbstractApplicationContext的refresh()，将Bean信息转化为BeanDefinition，存储到Map中
2.finishBeanFactoryInitialization的getBean()


转化：Xml信息-->Dodument-->BeanDefinition
BeanName的存储在List中，BeanDefinition的存储在Map中
