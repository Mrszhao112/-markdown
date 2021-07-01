# MySQL
## mysql的操作基础语句
## 三大范式
1. 第一范式：确保每列保持原子性
2. 第二范式：确保表中的每列都和主键相关 （考虑建立多张表而不导致数据冗余）
3. 第三范式：确保每列都和主键直接相关 而不是间接相关 (考虑建立多张表)
五大约束: 主键约束 唯一约束 默认约束 外键约束(innodb支持) 非空约束 

## 事务的四种隔离机制和四大特性
原子性  一致性  隔离性(并发状态多 多线程处理 a不会看到b所做的改变) 持久性  ACID

锁实现隔离机制：四种隔离级别
1. 读取未提交：事务更新瞬间才加锁（行级共享锁） 读取到了错误的中间数据
2. 读取已提交：读取(读取的时候)时候加行级共享锁读完该行释放，更新时加行级排他锁， 多线程情况a读取后，b读取更改，导致数据不一致(也就是不可重复读的问题)
3. (默认)可重复读 幻读： 开始读取时候加共享锁，事务结束释放，更新加排他锁， 有幻读问题， 别的线程可以插入数据
4. 串行化：一个线程一个线程来

cas锁 版本号机制 
mvcc多线程版本控制 间隙锁(不太清楚)

## 两种常见引擎的区别
myisam：不支持事务 不支持外键 支持表锁读为主  存储为（表定义 表数据 表索引）    非聚簇索引

innodb：支持事务   支持外键   支持行锁写为主  存储为（表空间数据文件 日志文件） 聚簇索引(每张表主键构造)
2-4层高度 1-3次磁盘io操作

聚簇索引遍历查询效率高 修改效率低(b+树的叶分裂)
非聚簇索引 修改效率高(本质是b+树的叶子节点是不是存储的数据还是地址)
https://www.cnblogs.com/jiawen010/p/11805241.html

## b树 b+树 红黑树的区别
b树 叶子节点为空 索引和数据分成两个文件存储
b+ 叶子节点存数据 并有指向下一个的指针 索引和数据存在一个文件
不采用红黑树的原因是因为层数态高IO太多 不适合磁盘 、https://zhuanlan.zhihu.com/p/217875063

