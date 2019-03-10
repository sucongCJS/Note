# not null
- 太多会消耗数据库性能
```sql
ALTER TABLE x modify column_name null;
ALTER TABLE x modify column_name varchar(25) not null;
-- 去除not null约束
ALTER TABLE table_name ALTER COLUMN column_name DROP NOT NULL;
```

## BTW:空值(Null)的陷阱
- 空值不一定为空!
&emsp;&emsp;空值是一个比较特殊的字段。在MySQL数据库中，在不同的情形下，空值往往代表不同的含义。这是MySQL数据库的一种特性. 如在普通的字段中(字符型的数据)，空值就是表示空值, 但有特殊情况:
1. 如果将`null`插入到**TimesTamp**类型的字段中，该字段就不为空, 而是插入了插入时的当前时间.
2. 如果向有`auto_increment`属性的列插入`null`值的话, 系统会插入一个正整数序列
- 空值不一定等于空字符



# unique
## 添加约束
- 列级约束
- 表级约束
  - 使用表级约束可以联合多个字段。只有在联合的字段都同时相同的时候才会报错,只有不完全相同时不报错
  - 表级约束可以给约束起名字（方便以后通过这个名字来删除这个约束）
  ```sql
  create table t_user(
    id int(10),
    name varchar(32) not null,
    email varchar(128),
    constraint t_user_email_unique unique(email)
  );
  ```

## 修改约束
```sql
alter table table_name modify char(20) unique key;
```

# PK
## 添加约束
- 主键约束与`not null unique`的区别在于,主键约束还会默认添加`index`
- 单一主键
  - 列级约束
  - 表级约束
  ```sql
  create table t_user(
    id int(10) auto_increment,
    name varchar(32) not null,
    constraint t_user_id_pk primary key(id)
  );
  ```
- 复合主件
  - 表级约束
  ```sql
  create table t_user(
    id int(10),
    name varchar(32) not null,
    email varchar(128),
    primary key(id, name)
  );
  ```

## 修改约束
```sql
-- 删除主键约束
alter table biao drop primary key;
-- 添加主键
alter table biao add primary key;
-- 修改列为主键
alter table biao modify column_name data_type primary key;
```

# FK
## 添加约束
- 只有表级约束
  ```sql
  drop table if exists t_student;
  drop table if exists t_class;

  create table t_class(
    cno int(10) primary key,
    cname varchar(128) not null unique
  );

  create table t_student(
    sno int(10) primary key auto_increment,
    sname varchar(32) not null,
    classno int(3),
    foreign key (classno) references t_class(cno)
  );

  ```

## 修改约束
```sql
alter table table_name add [constraint [symbol]]
foreign key [index_name] (column_name, ...)
references table_name (column_name, ...)
-- index represents a foreign key ID.

-- delete foreign key constraint
alter table table_name drop foreign key foreignKeyName;
-- foreignKeyName is the constraint name
```

## possible reasons for errors when adding a FK
- 两个字段的类型必须严格一致
- 两个字段都必须已经建立了索引
- 检查表的引擎类型
- 外键名字不能重复，必须是唯一的
- 可能给外键设置了默认值
- ……

# DEFAULT约束


# CHECK约束

<br>
references:
- [Mysql的空值与NULL的陷阱](https://www.cnblogs.com/apache-x/p/5386287.html)
- [MySQL——约束](https://segmentfault.com/a/1190000006671061)
- [Mysql无法创建外键的原因](https://blog.csdn.net/wangpeng047/article/details/19624351)
