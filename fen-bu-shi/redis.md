# Redis 类型
String、字典Hash、列表List、集合Set、有序集合SortedSet
数据结构HyperLogLog、Geo、Pub/Sub

# Redis Module
Redis Module，像BloomFilter，RedisSearch，Redis-ML

# Redis分布式锁
setnx + expire
set方法把setnx和expire合成一条指令

# 大量key，查询时不能用keys，会造成阻塞
可以使用scan指令，scan指令可以无阻塞的提取出指定模式的key列表，但是会有一定的重复概率，在客户端做一次去重

# Redis异步队列