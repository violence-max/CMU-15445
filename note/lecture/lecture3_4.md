> DBMS假设主要的数据库的存储位置是在非易失性的磁盘，DBMS的组件管理数据在非易失性存储和易失性存储之间实现
> 
- 序列化 vs 随机访问

随机访问非易失性存储通常会比序列化访问要慢

**DBMS想要最大化序列化访问：**

1. 能够减少向随机页面写数据的算法，以至于能让数据存储在连续的块上
2. 扩展：统一时间分配大量页面
- 系统设计的目标
1. 允许DBMS管理超过可以接触到的内存的数量的数据库
2. 读/写 磁盘是非常”昂贵的“，所以必须仔细地管理以防大范围地停止和性能下降
3. 随机访问磁盘通常比序列化访问要慢，所以DBMS要最大化序列化访问

本次课程主要内容：

1. **文件存储**
2. **页面布局**
3. **元组布局**
4. **数据表示**
5. **系统目录**
6. **存储模型**

- 文件存储

**存储管理：存储管理者负责维护一个数据库的文件**

它组织文件作为页面的集合

→追踪数据对页面的读写

→吹总可以获得的空间

**数据库的页：一页是固定大小的块的数据**

每一页都有一个独特的标识符

→DBMS使用不直接的层次来映射页的id到物理位置

**数据库的堆：一个堆文件时一个没有序列的页的集合，这些页里的元组以随机顺序进行存储**

→必须支持能够迭代所有页

两种代表一个堆文件的方式：

1. 链表
2. 页面目录

- 页面布局

两种页面内存储数据的方式（假设页里面只有元组）

1. 面向元组的
2. 日志结构的

面向元组的页面不距离最常用的布局就是插槽页面：

![image](/image/lecture3andlecture4/image1.png)

日志结构并不直接存储元组，值存储日志记录。为了读记录，DBMS从后开始扫面然后”重建“元组来寻找它需要什么

→创建索引使得它能够跳到这个日志里面的其他位置

→阶段性地压缩日志

- 元组布局

- 数据表示

**很大的变量：大部分DBMS不允许元组超过当个页面的大小**

为了存储大小大于页面的变量，DBMS使用分开的一出的存储页面

一些系统允许你存储一些非常大的变量在一些外部的文件中，这些文件被当作是BLOB形式

DBMS不能操作外部文件的内容：

→没有耐久性的保护

→没有事务保护

- 系统目录

一个DBMS将有关数据库的元数据存储在它自己内部的目录里

数据库运行负载：

On-Line Transaction Processing(OLTP)

→只读或者更新很小的一部分数据时具有很快的速度

On-Line Analytical Processing(OLAP)

→能够执行注入读很多数据来计算聚合实现等复杂的运算

Hybrid Transaction + Analytical Processing

→在一个数据库实例中OLTP和OLAP的结合

- 存储模型

N-ARY STORAGE MODEL(NSM)

→DBMS将单个元组的所有属性连续地存储于一页

→对执行只在个人地季尼汝和频繁插入的工作中的OLTP工作负载是理想的

DECOMPOSITION STORAGE MODEL(DSM)

→DBMS将所有元组的单个属性连续地存储于一页里（列式村粗）

→对于只执行只读查询需要进行对一个表中的属性进行大量扫描的OLAP工作负载是理想的