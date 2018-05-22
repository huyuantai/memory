# servlet 是什么
servlet 是服务端程序，只能由servlet容器来运行，且管理，常见的容器有Tomcat容器

# servlet生命周期
加载、创建、init初始化、服务Service（doGet、doPost）、销毁destroy、容器卸载
![](/assets/xwuusnjs.aao.jpg)

# ServletConfig
ServletConfig:Servlet在web.xml中的配置信息(如下的init-param)
web容器在创建servlet实例对象时，会自动将这些初始化参数封装到ServletConfig对象，然后在调用servlet的init方法时，将ServletConfig对象传递给servlet
```xml
<servlet>
        <servlet-name>ServletConfigTest</servlet-name>
        <servlet-class>com.vae.servlet.ServletConfigTest</servlet-class>
        <init-param>
            <param-name>name1</param-name>
            <param-value>value1</param-value>
        </init-param>
        <init-param>
            <param-name>encode</param-name>
            <param-value>utf-8</param-value>
        </init-param>
    </servlet>
```