# 函数

  - ## Aggregate函数 - 函数计算从列中取得的值，返回一个单一的值

      - AVG() - 返回平均值
      - COUNT() - 返回行数
      - FIRST() - 返回第一个记录的值
      - LAST() - 返回最后一个记录的值
      - MAX() - 返回最大值
      - MIN() - 返回最小值
      - SUM() - 返回总和

  - ## Scalar 函数 - 基于输入值，返回一个单一的值

      - UCASE() - 将某个字段转换为大写
      - LCASE() - 将某个字段转换为小写
      - MID() - 从某个文本字段提取字符，MySql 中使用
      - SubString(字段，1，end) - 从某个文本字段提取字符
      - LEN() - 返回某个文本字段的长度
      - ROUND() - 对某个数值字段进行指定小数位数的四舍五入
      - NOW() - 返回当前的系统日期和时间
      - FORMAT() - 格式化某个字段的显示方式

# GROUP BY

  - ​	GROUP BY 语句用于结合聚合函数，根据一个或多个列对结果集进行分组。

# HAVING子句

# 多表连接 (JOIN)

![连接图](/Users/aixu/Documents/Oracle/assets/sql-join.png)

  ## 1. 笛卡尔积

  - ### 出现在多表连接的时候

      例如：**查询A和B的时候，它会将A表 /* B表的结果显示出来**

  - ### 注意：

      - 为了避免产生笛卡尔积的出现，多表查询时，一定要加入条件。条件可以是：第一个表中和第二个表中包含相同等价意义的列值。
      - 在使用多表连接时，尽量使用别名的方式，来定义表名，一旦使用别名，就只能使用别名

  ## 2. INNER JOIN(内连接)

- ### 两个表中的数据都，满足 - 表中存在至少一个匹配时返回行

- ### 语法

```sql
SELECT column_name(s)
FROM table1
INNER JOIN table2
ON table1.column_name=table2.column_name;
-- 或者
SELECT column_name(s)
FROM table1
JOIN table2
ON table1.column_name=table2.column_name;
```



  ## 3. 外连接(左连接、右连接、全外连接)

  ## 4. 自连接

  ## 5. 

# Where和having的区别

- ## where

  - **可以当成是一般条件判断**

- ## having

  - **需要跟在分组的条件之后的**

- ## 相同点

  - **它们都是可以用逻辑条件的**