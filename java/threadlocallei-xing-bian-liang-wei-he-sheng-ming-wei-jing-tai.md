https://blog.csdn.net/chicm/article/details/40894299


Java 中每个线程都有与之关联的Thread对象，Thread对象中有一个ThreadLocal.ThreadLocalMap类型的成员变量，该变量是一个Hash表， 所以每个线程都单独维护这样一个Hash表

当ThreadLocal类型对象调用set方法时，即上面的threadLocalID.set(id)，这个set方法会使用当前线程维护的Hash表，把自己作为key, id作为value插入到Hash表中。由于每个线程维护的Hash表是独立的，因此在不同的Hash表中，key值即使相同也是没问题的


如果把threadLocal声明为非静态，则在类A的每个实例中都会产生一个新对象，这是毫无意义的，只是增加了内存消耗


ThreadLocal内存泄漏的根源是：由于ThreadLocalMap的生命周期跟Thread一样长，如果没有手动删除对应key就会导致内存泄漏，而不是因为弱引用。

想要避免内存泄露就要手动remove()掉！


![](/assets/20141107163750671)
