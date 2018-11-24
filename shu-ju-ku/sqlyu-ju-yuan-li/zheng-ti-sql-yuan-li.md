# 整理sql执行顺序
* (7)     SELECT 
* (8)     DISTINCT <select_list>
* (1)     FROM <left_table>
* (3)     <join_type> JOIN <right_table>
* (2)     ON <join_condition>
* (4)     WHERE <where_condition>
* (5)     GROUP BY <group_by_list>
* (6)     HAVING <having_condition>
* (9)     ORDER BY <order_by_condition>
* (10)    LIMIT <limit_number>


# 默认传统顺序
from on join where group by having
select distinct ordery by limit

但是现代的数据库都对以上的顺序做了些优化，并不一定就按该传统顺序，最直接的是数据库的优化器将选择首先评估where，看是否能利用索引，然后再执行from，来避免直接加载from 表的全部大量数据集

# 几点需要注意

> where 不能使用select 中的别名，因为该别名尚未确定

> mysql中，在GROUP BY和HAVING子句中允许使用SELECT列表中创建的别名，即使这些子句出现在SELECT子句之前（并且比SELECT子句更早地进行评估）
