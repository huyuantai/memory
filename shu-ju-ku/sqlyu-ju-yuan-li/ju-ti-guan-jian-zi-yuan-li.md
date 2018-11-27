
# 具体join in exist group by  order by min max  count 原理

---
## join
### join 连接算法
表之间的连接用了hash Join， Nested loops，Sort Merge Join
Oracle 使用这三种hash Join， Nested loops，Sort Merge Join

> Mysql 只使用了Nested loops

##### hash Join
大数据集连接时的常用方式
步骤：将两个表中较小的一个在内存中构造一个HASH表（对JOIN KEY），扫描另一个表，同样对JOIN KEY进行HASH后探测是否可以JOIN。适用于记录集比较大的情况。需要注意的是：如果HASH表太大，无法一次构造在内存中，则分成若干个partition，写入磁盘的temporary segment，则会多一个写的代价，会降低效率


##### Nested loops 
类似一个嵌套的循环,for里for

##### Sort Merge Join
通常情况下散列连接的效果都比排序合并连接要好，然而如果行源已经被排过序，在执行排序合并连接时不需要再排序了，这时排序合并连接的性能会优于散列连接。可以使用USE_MERGE(table_name1 table_name2)来强制使用排序合并连接.

Sort Merge join 用在没有索引，并且数据已经排序的情况






### join 连接对比
From A 
Left Join B ON A.t_id = B.t_id 
Left Join C ON A.p_id = C.p_id 

首先A 与 B 连接得到 AB的连接后结果集【AB集】，
然后【AB集】在与C连接得到【AB集】C集

连接可以=，>,< 等等，如
> ON A.t_id = B.t_id 
> ON A.t_id > B.t_id 
> ON A.t_id < B.t_id 

a:  From A  Left Join B ON A.t_id = B.t_id AND B.status = 1
与
b:  From A  Left Join B ON A.t_id = B.t_id Where B.status = 1
的区别

a中当 A.t_id = B.t_id AND B.status = 1 的数据会被匹配，不符合的都会以A为准 补 NULL记录，返回的结果集 可能是 A的行数， 或是A的倍数（1对多时）

b中当A.t_id = B.t_id的数据会被匹配，不符合的都会以A为准 补 NULL记录，然后再进行where 条件过滤



















