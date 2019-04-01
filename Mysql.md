### Mysql

#### InnoDB数据库引擎

##### B+ 树

B+树作为Innode引擎的索引数据结构，其结构简析为：非叶节点索引项+叶节点数据项，而且Innode数据引擎是按索引来组织表，表中的数据按主键顺序存放。

MyISAM索引方面的对比：

- MyISAM数据引擎同样使用B+树引擎，但是对于主索引，其叶节点仅存储指向行记录的地址，也就是说MyISAM的索引文件和数据文件是分开的。
- 对于辅助索引，InnoDB存储相对应的主键值，也就是说要是通过辅助索引来定位，需要通过辅助索引取主键、根据主键取主索引的数据行两个步骤。MyISAM的主索引和辅助索引没有多大的区别

#### 聚集索引和非聚集索引

- 聚集索引作为一种索引类型，它遵循索引顺序与物理存储顺序一致的规则。（属于Innodb）这种索引的区间查询、尾插入效率十高，但是在随机插入的情况下，效率十分低。
- 非聚集索引：索引的逻辑顺序与实际物理存储数据的顺序不同。对于频繁更新列的情况，非聚集索引效率相对更高（属于MyISAM）

#### 事务支持

- InnoDB支持行锁级别的事务，
- MyISAM锁粒度较大，仅支持表锁级别的事务







#### Mysql指令

添加索引指令：

- CREATE INDEX index_name ON table_name(column_name);
- ALTER TABLE table_name ADD PRIMARY KEY(column_name);
- ALTER TABLE table_name ADD UNIQUE KEY(column_name);

删除索引指令: 

- DROP INDEX index_name ON table_name;
- ALTER TABLE table_name DROP primary key(column_name);
- ALTER TABLE table_name DROP UNIQUE KEY(column_name);

查看索引: show index from tablename;



