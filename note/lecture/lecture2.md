> SQL：structured query language
> 

sql语句分为三个语种（是这样形容吗？）

- Data Manipulation Language(DML)
- Data Definition Language(DDL)
- Data Control Language(DCL)

<aside>
💡 SQL 是以重复元素为基础的而不是集合，集合不可以有重复的元素

</aside>

重要知识点：

1. 集成+分组（group by）
2. 字符串/日期/时间操作
3. 输出控制+重定向
4. 嵌套查询
5. 普通表表达式
6. 窗口功能

数据库例子：

![image1](/image/lecture2/image1.png)

1. 集成：

有很多从元组中返回一个单一的值得函数：

AVG(col)

MIN(col)

MAX(col)

SUM(col)

COUNT(col)    ：返回一列中行的个数

在SQL中，由于元素是可以重复的，所以满足选择条件的所有元素都会作为结果。而COUNT,SUM,AVG支持了关键字DISTINCT去选择不同的元素

```sql
#get the number of unique student that have an "@cs" login.

SELECT COUNT(DITIINCT login)
	FROM student WHERE login LIKE '%@cs'
```

1. 分组(GROUP BY)

可以实现列中的元素分组，满足选择要求

<aside>
💡 SELECT输出子句的非聚合值必须出现在GROUP BY子句中

</aside>

1. HAVING

以集成计算为基础进行结果过滤，相当于对于GROUP BY语句的WHRER语句

![image2](/image/lecture2/image2.png)

因为SELECT语句是作为最后的一个环节，所以不能在HAVING语句里对s.gpa采用SELECT语句中定义的简写

1. 字符串操作

LIKE 这个关键字是用于字符串匹配的

‘%’ 可以匹配任何子串（包括空串）

‘_’ 可以匹配任意一个字符

|| 可以将两个或者以上的字符连接在一起

1. 日期/时间操作

demo：获取从一年开始到现在过了多少天（自行上网搜索，不同数据库管理系统方式不一样）

1. 输出重定向

将查询结果存储于另外一个表中

- 表必须没有被定义过
- 新表会和旧表拥有同样的列的类型
1. 输出控制

对输出的内容进行排序

- LIMIT <count> [offset]
    1. 限制输出中的元组的#
    2. 可以设置一个偏移量来返回一个范围
1. 嵌套循环
2. 窗口功能
3. 普通表表达式