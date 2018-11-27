
# 具体join in exist group by  order by min max  count 原理

---
## join
### join 连接算法
表之间的连接用了hash Join， Nested loops，Sort Merge Join





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



















