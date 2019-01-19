https://blog.csdn.net/xlgen157387/article/details/80389101

https://www.cnblogs.com/rjzheng/p/9302609.html

https://www.cnblogs.com/rjzheng/p/9240611.html


缓存一篇就够了
https://mp.weixin.qq.com/s?__biz=MjM5ODYxMDA5OQ==&mid=2651961368&idx=1&sn=82a59f41332e11a29c5759248bc1ba17&chksm=bd2d0dc48a5a84d293f5999760b994cee9b7e20e240c04d0ed442e139f84ebacf608d51f4342&scene=21#wechat_redirect

从库执行完写操作，向缓存再次发起删除，淘汰这段时间内可能写入缓存的旧数据
思路转化为：在从库同步完成之后，如果有旧数据入缓存，应该及时把这个旧数据淘汰掉



## 缓存的两大方面
1.缓存读取
2.缓存更新（当数据有变动时，必须更新缓存中的数据为新数据）

## 缓存读取
读取缓存
有数据时直接返回客户端
无数据时再读取数据库，再放入缓存中，后返回客户端

## 缓存更新两大策略
1.更新缓存策略（update）
2.淘汰缓存策略（delete）


## 更新缓存策略（线程安全问题！！）
1.先更新缓存，再更新数据库 
更新缓存成功，更新数据库失败，数据不一致，其他线程读取到缓存中的错误新数据了

2.先更新数据库，再更新缓存



