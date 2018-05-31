聚合函数：Count Min AG Max Sum（call me ag 妈妈桑）


–COUNT：统计行数量
–SUM：获取单个列的合计值
–AVG：计算某个列的平均值
–MAX：计算列的最大值
–MIN：计算列的最小值聚合函数

> Where 不跟聚合函数
> Having 可跟聚合函数




> 1、执行WHERE筛选数据
> 2、执行GROUP BY分组形成中间分组表
> 3、执行WITH ROLLUP/CUBE生成统计分析数据记录并加入中间分组表
> 4、执行HAVING筛选中间分组表
> 5、执行ORDER BY排序