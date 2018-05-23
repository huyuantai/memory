# servlet 是什么

servlet 是服务端程序，只能由servlet容器来运行，且管理，常见的容器有Tomcat容器

# servlet生命周期

加载、创建、init初始化、服务Service（doGet、doPost）、销毁destroy、容器卸载  
![](/assets/xwuusnjs.aao.jpg)

# ServletConfig

ServletConfig:Servlet在web.xml中的配置信息\(如下的init-param\)  
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

# ServletContext

ServletContext：代表当前web应用,在web.xml的context-param  
WEB容器在启动时，它会为每个WEB应用程序都创建一个对应的ServletContext对象，它代表当前web应用

> 整个web应用范围内共享数据
>
> ```xml
> <context-param>
>     <param-name>contextConfigLocation</param-name>
>     <param-value>/WEB-INF/applicationContext.xml,/WEB-INF/action-servlet.xml,/WEB-
> INF/jason-servlet.xml</param-value>
> </context-param>
> <listener>
>     <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
> </listener>
> 又如: --->自定义context-param,且自定义listener来获取这些信息
> <context-param>
>     <param-name>urlrewrite</param-name>
>     <param-value>false</param-value>
> </context-param>
> ```

# 实现Servlet的转发

```java
public void doGet(HttpServletRequest request, HttpServletResponse response)
             throws ServletException, IOException {
         RequestDispatcher dispatcher = this.getServletContext()
                 .getRequestDispatcher("/servlet/ServletTest05");// 参数中写虚拟路径
         dispatcher.forward(request, response); // 执行完这一行代码后，将会跳到ServletTest05中去执行。

    }
```

