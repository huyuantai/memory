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

# Redis 异步队列
一般使用list结构作为队列，rpush生产消息，lpop消费消息。当lpop没有消息的时候，要适当sleep一会再重试。

如果对方追问可不可以不用sleep呢？list还有个指令叫blpop，在没有消息的时候，它会阻塞住直到消息到来。

如果对方追问能不能生产一次消费多次呢？使用pub/sub主题订阅者模式，可以实现1:N的消息队列。

如果对方追问pub/sub有什么缺点？在消费者下线的情况下，生产的消息会丢失，得使用专业的消息队列如rabbitmq等。

# redis 实现延时队列
使用sortedset，拿时间戳作为score，消息内容作为key调用zadd来生产消息，消费者用zrangebyscore指令获取N秒之前的数据轮询进行处理

# key同时间雪崩解决
在时间上加一个随机值，使得过期时间分散一些


# Redis 持久化

