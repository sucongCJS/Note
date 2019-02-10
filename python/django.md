### makemigrations
`python manage.py makemigrations app_name`
> every you make some changes to your models, you can stored the changes as a migration by do so.

### sqlmigrate
`python manage.py sqlmigrate app_name migrate_file_name(eg.0001)`
> generate the sql command without making migrations

### migrate
`python manage.py migrate`
> apply changes to the database

## 通用视图
- 每个通用试图需要知道它将作用于哪个模型. 有**model**属性提供
- 通用视图 **DetailView** 期望从URL中捕获名为"pk"的主键名
