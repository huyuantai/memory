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