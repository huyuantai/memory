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
如下：
1.查找缓存中有没Class
2.没有交给父类加载器loadClass，这里是递归，所以父类的loadClass,又交给父类的父类加载器loadClass
3.没有就交给启动类加载器加载
4.没有的话就交给自定义实现的findClass方法去加载并实现

由于自定义类加载器继承ClassLoader，实现findClass方法，所以自定义加载器满足双亲模型，因为类加载还是调用loadClass方法，只是如果都找不到，最后就调用自定义类加载器的findClass方法加载

findClass 实现
getClassData

# loadClass
```java
protected Class<?> loadClass(String name, boolean resolve)
      throws ClassNotFoundException
  {
      synchronized (getClassLoadingLock(name)) {
          // 先从缓存查找该class对象，找到就不用重新加载
          Class<?> c = findLoadedClass(name);
          if (c == null) {
              long t0 = System.nanoTime();
              try {
                  if (parent != null) {
                      //如果找不到，则委托给父类加载器去加载
                      c = parent.loadClass(name, false);
                  } else {
                  //如果没有父类，则委托给启动加载器去加载
                      c = findBootstrapClassOrNull(name);
                  }
              } catch (ClassNotFoundException e) {
                  // ClassNotFoundException thrown if class not found
                  // from the non-null parent class loader
              }

              if (c == null) {
                  // If still not found, then invoke findClass in order
                  // 如果都没有找到，则通过自定义实现的findClass去查找并加载
                  c = findClass(name);

                  // this is the defining class loader; record the stats
                  sun.misc.PerfCounter.getParentDelegationTime().addTime(t1 - t0);
                  sun.misc.PerfCounter.getFindClassTime().addElapsedTimeFrom(t1);
                  sun.misc.PerfCounter.getFindClasses().increment();
              }
          }
          if (resolve) {//是否需要在加载时进行解析
              resolveClass(c);
          }
          return c;
      }
  }
```
# findClass
```java
protected Class<?> findClass(String name) throws ClassNotFoundException {
      // 获取类的字节数组
      byte[] classData = getClassData(name);  
      if (classData == null) {
          throw new ClassNotFoundException();
      } else {
          //使用defineClass生成class对象
          return defineClass(name, classData, 0, classData.length);
      }
  }
```






