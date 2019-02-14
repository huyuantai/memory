# CAS (乐观锁实现)
CAS有3个操作数，内存值V，旧的预期值A，要修改的新值B
当且仅当预期值A和内存值V相同时，将内存值V修改为B，否则什么都不做

# Java CAS 都是使用unsafe 如
- unsafe.compareAndSwapInt(this, valueOffset, expect, update)

# compareAndSwapInt 底层原理
