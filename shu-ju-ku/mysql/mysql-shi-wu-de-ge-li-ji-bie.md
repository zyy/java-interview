# MySQL事务的隔离级别

### MySQL事务的隔离级别

MySQL的事务隔离级别一共有四个，分别是**读未提交**、**读已提交**、**可重复读**以及**可串行化**。

MySQL的隔离级别的作用就是让事务之间互相隔离，互不影响，这样可以保证事务的一致性。

隔离级别比较：可串行化>可重复读>读已提交>读未提交

隔离级别对性能的影响比较：可串行化>可重复读>读已提交>读未提交

由此看出，隔离级别越高，所需要消耗的MySQL性能越大（如事务并发严重性），为了平衡二者，一般建议设置的隔离级别为可重复读，MySQL默认的隔离级别也是可重复读。

### 测试数据准备

```
mysql> create table city(
    -> id int(10) auto_increment,
    -> name varchar(30),
    -> primary key (id)
    -> )engine=innodb charset=utf8mb4;

insert into city(name) values('武汉市');

mysql> select * from city;
+----+-----------+
| id | name |
+----+-----------+
| 1 | 武汉市 |
+----+-----------+
```

### 事务并发可能出现的问题

#### 脏读（**Dirty Read**）

|   | 事务A                                                       | 事务B                                        |   |
| - | --------------------------------------------------------- | ------------------------------------------ | - |
| 1 | begin;                                                    |                                            |   |
| 2 |                                                           | begin;                                     |   |
| 3 |                                                           | update city set name='温州市'  where  id = 1; |   |
| 4 | <p>select * from city where id =1;<br>读取的记录为温州市，出现了脏读</p> |                                            |   |
| 5 | commit;                                                   |                                            |   |
| 6 |                                                           | rollback;                                  |   |

