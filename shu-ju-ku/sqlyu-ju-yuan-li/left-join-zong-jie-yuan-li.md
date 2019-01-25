## 关联两张表
#### A表LEFT JOIN（一个字段）
A表没索引、B表有索引 A表ALL  B表使用索引（Using index）
A表有索引、B表没索引 A表ALL  B表ALL出现（Using where; Using join buffer (Block Nested Loop)）
A表、B表有索引       A表ALL  B表使用索引（Using index）

总结A表 LEFT JOIN B表，A表ALL，主要看B表是否使用索引

A表、B表 以表数量少的为主驱动表，
如crm_coach_arrange 1百万条
  crm_customer_info 30000万条
以crm_customer_info 为主驱动表

crm_customer_info LEFT JOIN 如crm_coach_arrange

> SELECT
	COUNT(r.id)
FROM
	crm_customer_info info
LEFT JOIN  crm_coach_arrange r ON info.customer_id = r.customer_id
WHERE
	1 = 1
AND r.customer_id > 0;


A表LEFT JOIN（一个字段）
A表没索引、B表有索引（存在空值）A表ALL  B表使用索引
A表有索引、B表没索引（存在空值）A表ALL  B表ALL出现（Using where; Using join buffer (Block Nested Loop)）
		