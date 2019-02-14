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

# lock前缀 保证CPU操作 原子性
- 为CPU添加总线锁
- 或CPU添加缓存锁




