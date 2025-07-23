# DQL（查询数据库中表的记录）
语法：
```
select
    字段列表        5
from
    表名列表        1执行顺序
where
    条件列表        2
group by
    分组字段列表    3
having
    分组后条件列表   4
order by
    排序字段列表    6
limit
    分页参数        7
```
## 基本查询
1. 查询多个字段：`slect 字段1，字段2，... from 表名;`或`slect * from 表名;`
2. 设置别名：`slect 字段1[as 别名1]，字段2[as 别名2]，... from 表名;`
3. 去除重复记录：`select distinct 字段列表 from 表名;`
## 条件查询
语法：
```
select 字段列表 from 表名 where 条件列表;
```
## 聚合函数
将一列数据作为一个整体，进行纵向计算。null值不参与计算。
```
count:统计数量
max:最大值
min:最小值
avg:平均值
sum:求和
```
语法：`select 聚合函数（字段列表） from 表名;`
## 分组查询
语法：
```
select 字段列表 from 表名 [where 条件] group by 分组字段名 [having 分组后过滤条件]

where与having区别
1. 执行时机不同，前者是在分组之前，后者是在分组之后。
2. where不能对聚合函数进行判断，而having可以。
```
## 排序查询
语法：
```
select 字段列表 from 表名 order by 字段1 排序方式1，字段2，排序方式2;
排序方式：ASC 升序；DESC 降序；
```
## 分页查询
语法：
```
select 字段列表 from 表名 limit 起始索引，查询记录数;
起始索引从0开始，起始索引=（查询页码-1）*每页显示记录数。
```