CAS https://zl198751.iteye.com/blog/1848575

# CAS (乐观锁实现)
- CAS有3个操作数，内存值V，旧的预期值A，要修改的新值B
- 当且仅当预期值A和内存值V相同时，将内存值V修改为B，否则什么都不做

# Java CAS 都是使用unsafe 如
- unsafe.compareAndSwapInt(this, valueOffset, expect, update)

# compareAndSwapInt 底层原理【CPU（intel x86)】
- 调用JNI的代码C代码实现
- openjdk中依次调用的c++代码为：unsafe.cpp，atomic.cpp和atomicwindowsx86.inline.hpp

# atomicwindowsx86.inline.hpp 关键代码
```c
// Adding a lock prefix to an instruction on MP machine
// VC++ doesn't like the lock prefix to be on a single line
// so we can't insert a label after the lock prefix.
// By emitting a lock prefix, we can define a label after it.
#define LOCK_IF_MP(mp) __asm cmp mp, 0  \
                       __asm je L0      \
                       __asm _emit 0xF0 \
                       __asm L0:

inline jint     Atomic::cmpxchg    (jint     exchange_value, volatile jint*     dest, jint     compare_value) {
  // alternative for InterlockedCompareExchange
  int mp = os::is_MP();
  __asm {
    mov edx, dest
    mov ecx, exchange_value
    mov eax, compare_value
    LOCK_IF_MP(mp)
    cmpxchg dword ptr [edx], ecx
  }
}

```
# 关键代码分析
- 如果是多处理器，为cmpxchg指令添加lock前缀
- 如果是单处理器，就省略lock前缀

# lock前缀 保证CPU操作原子性
- 为CPU添加总线锁
- 或CPU添加缓存锁

# 总线锁
总线锁就是使用处理器提供的一个LOCK＃信号，当一个处理器在总线上输出此信号时
其他处理器的请求将被阻塞住,那么该处理器可以独占使用共享内存


# 缓存锁（优化总线锁的独占，提高性能）
处理器不在总线上声言LOCK＃信号，而是锁定缓存行
缓存一致性机制 两个以上处理器缓存的内存区域数据，不允许同时修改
> 如：当CPU1修改缓存行中的i时使用缓存锁定，那么CPU2就不能同时缓存了i的缓存行

# 当数据跨多个缓存行（cache line），使用不了缓存锁，则处理器会调用总线锁

# CAS 三大缺点
1.ABA问题
2.循环时间长
3.只能保证一个共享变量的原子操作

### ABA问题
ABA问题的解决思路就是使用版本号
在变量前面追加上版本号，每次变量更新的时候把版本号加1，那么A－B－A 就会变成1A-2B－3A

atomic包里提供了一个类AtomicStampedReference来解决ABA问题
compareAndSet方法作用是首先检查“当前引用是否等于预期引用”，并且“当前标志是否等于预期标志”，如果全部相等，则以原子方式将该引用和该标志的值设置为给定的更新值

### 循环时间长
自旋CAS如果长时间不成功，会给CPU带来非常大的执行开销。如果JVM能支持处理器提供的pause指令那么效率会有一定的提升，pause指令有两个作用，第一它可以延迟流水线执行指令（de-pipeline）,使CPU不会消耗过多的执行资源，延迟的时间取决于具体实现的版本，在一些处理器上延迟时间是零。第二它可以避免在退出循环的时候因内存顺序冲突（memory order violation）而引起CPU流水线被清空（CPU pipeline flush），从而提高CPU的执行效率

### 只能保证一个共享变量的原子操作
多个共享变量可以合并成一个共享变量





