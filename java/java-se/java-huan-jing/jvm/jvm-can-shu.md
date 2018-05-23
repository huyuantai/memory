* 运行模式Client、Server








JVM 运行模式 Client 和 Server

当虚拟机运行在-client模式的时候,使用的是一个代号为C1的轻量级编译器, 而-server模式启动的虚拟机采用相对重量级,代号为C2的编译器. C2比C1编译器编译的相对彻底,,服务起来之后,性能更高

Client JVM适合需要快速启动和较小内存空间的应用，它适合交互性的应用，比如GUI；而Server JVM则是看重执行效率的应用的最佳选择和较大的内存空间。不同之处包括：编译策略、默认堆大小、内嵌策略。


Server JVM 比 Client JVM InitialHeapSize和MaxHeapSize明显比Client JVM大出许多


Server JVM  比 Client JVM 编译器作了很多优化