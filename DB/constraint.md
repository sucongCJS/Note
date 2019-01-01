# not null
- 太多会消耗数据库性能

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
```

# DEFAULT约束


# CHECK约束

<br>
references:
- [MySQL——约束](https://segmentfault.com/a/1190000006671061)
