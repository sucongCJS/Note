
# 权限管理
## grant 权限 on 数据库对象 to 用户
0. 可以通过`show privileges;`查看有什么权限、对什么的权限和权限的具体内容
1. grant 普通数据用户权限
  ```sql
  grant select, insert, update, delete on testdb.* to common_user@'%';
  -- %表示任何主机（但不包括’localhost’和’127.0.0.1’）
  ```
2. grant 数据库开发人员 创建表、索引、视图、存储过程、函数等权限
  ```sql
  -- 创建、修改、删除数据表结构
  grant create on testdb.* to developer@'192.168.0.%';
  grant alter on testdb.* to developer@'192.168.0.%';
  grant drop on testdb.* to developer@'192.168.0.%';

  -- 操作外键的权限
  grant references on testdb.* to developer@'192.168.0.%';

  -- 操作临时表权限
  grant create temporary tables on testdb.* to developer@'192.168.0.%';

  -- 操作索引权限
  grant index on testdb.* to developer@'192.168.0.%';

  -- 操作视图、查看视图源代码权限
  grant create view on testdb.* to developer@'192.168.0.%';
  grant show view on testdb.* to developer@'192.168.0.%';

  -- 操作存储过程、函数权限
  -- can show procedure status
  grant create routine on testdb.* to developer@'192.168.0.%';
  -- can drop a procedure
  grant alter routine on testdb.* to developer@'192.168.0.%';
  grant execute on testdb.* to developer@'192.168.0.%';
  ```

3. grant 普通DBA管理某个数据库的权限
  ```sql
  grant all on testdb.* to dba@'192.168.0.%';
  ```

4. grant 高级DBA管理所有数据库的权限
  ```sql
  grant all on *.* to dba@'192.168.0.%';
  ```
5. MySQL grant 权限，分别可以作用在多个层次上。
  - 可以作用与表中的列

## 查看用户权限
  ```sql
  -- 查看当前用户权限
  show grants;
  -- 查看其他用户权限
  show grants for sb@localhost;
  ```
## 撤销用户权限
  ```sql
  revoke all on *.* from dba@localhost;
  ```

## MySQL grant、revoke 用户权限注意事项



<br>
<br>
reference:
- [mysql的grant权限](https://www.jianshu.com/p/fd1cb8657702)
- [MySQL里host为%是什么意思](https://blog.csdn.net/qq_26291823/article/details/51931453)
