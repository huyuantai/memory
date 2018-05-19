# 类加载器定义
负责读取 Java 字节代码，将字节码数据放到内存方法区，生成Class对象，成为访问该方法区的入口

Class ---> 方法区
          （Java 字节代码）
#　判断类相同，不同的两个类加载器加载A类，不相同

# 分类
启动扩展应用（启动扩展应用功能）
启动lib类库 （javahome）
扩展lib/ext类库
应用ClassPath，path的

# 双亲模型
通过组合实现父子关系，非继承，顶启动没父亲，其他都有父亲
![](/assets/20170625231013755.png)

组合实现父子关系，加载类一直向上委托给父亲，（直到启动顶端）
上层加载得到即结束，父亲加载失败即交给子加载处理
像爬梯子，一直往上爬，下来再一步一步往下

> 爬梯子 双亲，组合父子关系，非继承

好处：安全，杜绝通过使用和JRE相同的类名冒充现有JRE的类达到替换的攻击方式
双亲向上委派保证在各种类加载器环境中都是同一个类Object
不用双亲让各自类加载加载的话，如果在ClassPath被加入自己编写Object类，那么不同类加载就存在两个不同的Object，造成混乱

> 双亲保证不同类加载器同个Object类，不用双亲造成两个Object类（自己定义另一个Object），混乱


# 破坏双亲   
常见的 SPI 有 JDBC、JCE、JNDI、JAXP 和 JBI 等
启动加载器加载核心类库的SPI接口； 
应用器加载SPI实现类
启动类加载器是无法找到 SPI 的实现类的，因为它只加载 Java 的核心库
双亲委派模型无法解决这个问题

> 启动加载器要依赖应用加载器的实现类，双亲做不到，使用破坏双亲
> 线程上下文类加载器: 父类加载器请求子类加载器去完成类加载器(破坏双亲)

# 自定义类加载器
继承ClassLoader，Override findClass方法，defineClass()方法创建了类的class对象

# 自定义类加载器的意义？
1.class文件不在ClassPath路径，类加载找不到它
2.class文件加密后传输网络，自定义类加器可实现对它加密
3.热部署功能
> 找不到class文件、加密class文件、热部署

# 自定义类加载器也是双亲模型
![](/assets/20170625231013755.png)

# 抽象类ClassLoader，双亲模型的实现逻辑在此
> ExtClassLoader、AppClassLoader都继承于抽象类ClassLoader，而在ClassLoader中的loadClass实现了双亲模型的逻辑

```java
public static void main(String[] args) {  
String x = new String("ab");
change(x);
System.out.println(x);
}
public static void change(String x) {
x = "cd";
}
```





