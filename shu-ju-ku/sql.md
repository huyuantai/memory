聚合函数：Count Min AG Max Sum（call me ag 妈妈桑）


–COUNT：统计行数量
–SUM：获取单个列的合计值
–AVG：计算某个列的平均值
–MAX：计算列的最大值
–MIN：计算列的最小值聚合函数

> Where 不跟聚合函数
> Having 可跟聚合函数


# 执行顺序

> 1、执行WHERE筛选数据
> 2、执行GROUP BY分组形成中间分组表
> 3、执行WITH ROLLUP/CUBE生成统计分析数据记录并加入中间分组表
> 4、执行HAVING筛选中间分组表
> 5、执行ORDER BY排序

# Group By 原理
group by name 一个字段
![](/assets/162343319172617.jpg)

group by name,number，我们可以把name和number 看成一个整体字段

group by 要得到一条记录


# 同表查询
同表1 where exist （同表2）
同表1 where In （同表2）
同表1 where 字段 = （max（字段）同表2）
同表1 where exist （同表2）
















