http://www.cnblogs.com/aspirant/p/7200523.html

# 什么是类加载器
类加载器负责读取 Java 字节代码，并转换成 java.lang.Class类的一个实例。每个这样的实例用来表示一个 Java 类。通过此实例的 newInstance()方法就可以创建出该类的一个对象


# 类加载器与类的”相同“判断
要判断两个类是否“相同”，前提是这两个类必须被同一个类加载器加载，否则这个两个类不“相同”

# 类加载器种类
启动类加载器，Bootstrap ClassLoader，加载JACA_HOME\lib，或者被-Xbootclasspath参数限定的类
扩展类加载器，Extension ClassLoader，加载\lib\ext，或者被java.ext.dirs系统变量指定的类
应用程序类加载器，Application ClassLoader，加载ClassPath中的类库
自定义类加载器，通过继承ClassLoader实现，一般是加载我们的自定义类

#
双亲委派好处

避免同一个类被多次加载；
每个加载器只能加载自己范围内的类；


# 类的初始化时机：

1.遇到new、getstatic、putstatic或invokestatic这4条字节码指令时，如果类没有进行过初始化，则需要触发其初始化。生成这4条指令的最常见的Java代码场景是：使用new关键字实例化对象的时候、读取或设置一个类的静态字段（被final修饰、已在编译期把结果放入常量池的静态字段除外）的时候，以及调用一个类的静态方法的时候

2.使用java.lang.reflect包的方法对类进行反射调用的时候，如果类没有进行过初始化，则需要先触发其初始化

3.当初始化一个类的时候，如果发现其父类还没有进行过初始化，则需要先触发其父类的初始化

4.当虚拟机启动时候，用户需要指定一个要执行的主类（包含main()方法的那个类），虚拟机会先初始化这个主类

5.当使用JDK1.7的动态语言支持时，如果一个java.lang.invoke.MethodHandle实例最后的解析结果REF_getStatic、REF_putStatic、REF_invokeStatic的方法句柄，并且这个方法句柄所对应的类没有进行过初始化，则需要先触发其初始化