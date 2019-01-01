# 创建索引
## alter
```sql
-- 普通索引
ALTER TABLE table_name ADD INDEX index_name (column_list);
-- index_name: 索引名，可选，缺省时MySQL将根据第一个索引列赋一个名称
-- column_list: 要进行索引的列，多列的话用逗号分开
-- unique索引
ALTER TABLE table_name ADD UNIQUE (column_list);
-- PK索引
ALTER TABLE table_name ADD PRIMARY KEY (column_list);
```

## create
```sql
-- 普通索引
CREATE INDEX index_name ON table_name (column_list);
-- 索引名一定要
-- unique索引
CREATE UNIQUE INDEX index_name ON table_name (column_list);
-- 不能创建PK索引
```
# 索引类型
- 多指索引可以规定索引能否包含重复值，不包含的话应该创建为PK或unique索引

# 删除索引
## drop
```sql
-- 类似create index
DROP INDEX index_name ON table_name;

ALTER TABLE table_name DROP INDEX index_name;

ALTER TABLE table_name DROP INDEX PRIKMARY KEY;
-- 如果表没有PK索引，但有一个或多个UNIQUE索引，则MySQL将删除第一个UNIQUE索引
-- 如果删除了多值索引中的一个，则该列也会从索引中删除，但多值索引中的所有值被删除的时候，整个索引被删除
```

# 查看索引
```sql
show index from table_name;
show keys from table_name;
```
# 不建或少建索引的情况
- 表记录太少
- 经常插入、删除、修改的表
-

# 注意事项
- 建立索引的时候要加锁，因此要在业务空闲的时候进行操作

# 性能调试方面
- 最佳左前缀：把最常用的限制条件的列放在最左边，依次递减


<br><br>
references:
- (MySQL索引的查看创建和删除)[https://www.jianshu.com/p/e109aea6eb7c]
