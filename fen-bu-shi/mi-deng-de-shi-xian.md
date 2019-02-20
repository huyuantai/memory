# 幂等
- 系统中有很多操作，是不管做多少次，都应该产生一样的效果或返回一样的结果

# 例如

- 前端重复提交选中的数据，应该后台只产生对应这个数据的一个反应结果。 
- 我们发起一笔付款请求，应该只扣用户账户一次钱，当遇到网络重发或系统bug重发，也应该只扣一次钱； 
- 发送消息，也应该只发一次，同样的短信发给用户，用户会哭的； 
- 创建业务订单，一次业务请求只能创建一个，创建多个就会出大问题

# 幂等的保证如下

- 查询
> 查询一次和查询多次，在数据不变的情况下，查询结果是一样的。select是天然的幂等操作 
-----
- 删除
> 删除也是幂等的，删除一次和多次删除都是把数据删除
-----
- 唯一索引，防止新增脏数据 
> 只能插入一条数据
  当表存在唯一索引，并发时新增报错时，再查询一次就可以了，数据应该已经存在了，返回结果即可
-----
- token机制，防止页面重复提交，幂等 
> 处理流程： 
1.数据提交前要向服务的申请token，token放到redis或jvm内存，token有效时间,token返回前端form中 
2.数据连同toke提交到后台，校验token，同时删除token，生成新的token返回 

#### 注意：redis要用删除操作来判断token，删除成功代表token校验通过，如果用select+delete来校验token，存在并发问题，不建议使用
-----


- 悲观锁 
> select * from table_xxx where id='xxx' for update; 

####  注意：id字段一定是主键或者唯一索引，不然是锁表，会死人的, 悲观锁使用时一般伴随事务一起使用，数据锁定时间可能会很长，根据实际情况选用 
-----

- 乐观锁

1.通过版本号实现 
update table_xxx set name=#name#,version=version+1 where version=#version# 
2. 通过条件限制 
update table_xxx set avai_amount=avai_amount-#subAmount# where avai_amount-#subAmount# >= 0 

####   注意：乐观锁的更新操作，最好用主键或者唯一索引来更新,这样是行锁，否则更新时会锁表，上面两个sql改成下面的两个更好 
update table_xxx set name=#name#,version=version+1 where id=#id# and version=#version# 
update table_xxx set avai_amount=avai_amount-#subAmount# where id=#id# and avai_amount-#subAmount# >= 0 

-----

- 分布式锁(redis,zookeeper)
-----


- select + insert 

并发不高的后台系统，或者一些任务JOB，为了支持幂等，支持重复执行，简单的处理方法是，先查询下一些关键数据，判断是否已经执行过，在进行业务处理，就可以了 
注意：核心高并发流程不要用这种方法 

-----


