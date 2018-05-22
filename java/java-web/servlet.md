# servlet 是什么
servlet 是服务端程序，只能由servlet容器来运行，且管理，常见的容器有Tomcat容器

# servlet生命周期
加载、创建、init初始化、服务Service（doGet、doPost）、销毁destroy、容器卸载
![](/assets/xwuusnjs.aao.jpg)

# ServletConfig
ServletConfig:Servlet在web.xml中的配置信息
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