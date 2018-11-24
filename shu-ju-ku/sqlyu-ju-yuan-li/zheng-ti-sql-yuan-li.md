
# SQL查询之执行顺序解析
http://zouzls.github.io/2017/03/23/SQL%E6%9F%A5%E8%AF%A2%E4%B9%8B%E6%89%A7%E8%A1%8C%E9%A1%BA%E5%BA%8F%E8%A7%A3%E6%9E%90/


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

* > where 不能使用select 中的别名，因为该别名尚未确定


* > mysql中，在GROUP BY和HAVING子句中允许使用SELECT列表中创建的别名，
即使这些子句出现在SELECT子句之前（并且比SELECT子句更早地进行评估）

* > 在同一个SELECT列表中的其他表达式不能使用表达式别名。这是因为计算表达式的逻辑顺序无关紧要，也不能保证。例如，这个SELECT子句可能不如预期的那样工作，因此不支持：SELECT a+1AS x，x+1AS y



* > 当使用INNER JOIN时，在WHERE子句或ON子句中指定逻辑表达式并不重要。这是真的，因为ON和WHERE之间没有逻辑差异（除了使用OUTER JOIN或GROUP BY ALL选项时）
