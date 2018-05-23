* 运行模式Client、Server
* 各代内存大小
* 收集器
* CMS相关参数
* 辅助日志

# 运行模式 Client 和 Server

> 当虚拟机运行在-client模式的时候,使用的是一个代号为C1的轻量级编译器, 而-server模式启动的虚拟机采用相对重量级,代号为C2的编译器. C2比C1编译器编译的相对彻底,,服务起来之后,性能更高

> Client JVM适合需要快速启动和较小内存空间的应用，它适合交互性的应用，比如GUI；而Server JVM则是看重执行效率的应用的最佳选择和较大的内存空间。不同之处包括：编译策略、默认堆大小、内嵌策略。


> Server JVM 比 Client JVM InitialHeapSize和MaxHeapSize明显比Client JVM大出许多


> Server JVM  比 Client JVM 编译器作了很多优化

# 各代内存大小
初始化堆、最大堆、年轻代、永久代初始化、永久代最大、-Xss线程栈大小
-XX:SurvivorRatio Eden与Survivor的比例、-XX:MaxTenuringThreshold垃圾最大年龄

# 收集器
年轻代为并行收集、老年代用CMS

# CMS相关参数
XX+UseCMSCompactAtFullCollection	在FULL GC的时候， 对年老代的压缩	 	CMS是不会移动内存的， 因此， 这个非常容易产生碎片， 导致内存不够用， 因此， 内存的压缩这个时候就会被启用。 增加这个参数是个好习惯。
可能会影响性能,但是可以消除碎片
-XX:+UseCMSInitiatingOccupancyOnly	使用手动定义初始化定义开始CMS收集	 	禁止hostspot自行触发CMS GC
-XX:CMSInitiatingOccupancyFraction=70	使用cms作为垃圾回收
使用70％后开始CMS收集	92	为了保证不出现promotion failed(见下面介绍)错误,该值的设置需要满足以下公式CMSInitiatingOccupancyFraction计算公式
-XX:CMSInitiatingPermOccupancyFraction	设置Perm Gen使用到达多少比率时触发

# 辅助日志


