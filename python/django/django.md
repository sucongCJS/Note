# 数据库

## 新建数据库

character set: utf8

collation的选择

utf8_general_ci校对速度快，但准确度稍差。
utf8_unicode_ci准确度高，但校对速度稍慢。

如果你的应用有德语、法语或者俄语，请一定使用utf8_unicode_ci。一般用utf8_general_ci就够了，到现在也没发现问题



## 注意事项

- 如果是必填字段, 前期有没有设置值的话, 保存到数据库中是会报错的, 所以要设置 `default=""` 



## makemigrations
`python manage.py makemigrations app_name --name The_Name_of_The_Migration`
> every you make some changes to your models, you can stored the changes as a migration by do so.

## sqlmigrate
`python manage.py sqlmigrate app_name migrate_file_name(eg.0001)`
> generate the sql command without making migrations. (you do not have to do this when migrating)

## migrate
`python manage.py migrate`
> apply changes to the database

## undo migrate
`pythin manage.py migrate app_name 0001_initial`

## 注意事项
- 插入一个留空的字符型字段, 它会插入一个空字符串(而不是`NULL`). 但日期型, 时间型和数字型字段不接受空字符串(得视具体版本而定)

# 通用视图
- 每个通用试图需要知道它将作用于哪个模型. 有**model**属性提供
- 通用视图 **DetailView** 期望从URL中捕获名为"pk"的主键名

# 时间
`setting.py`中, 如果`USE_TZ`设置为`Ture`Django会使用系统默认设置的时区，即America/Chicago，
此时的TIME_ZONE不管有没有设置都不起作用。
如果USE_TZ 设置为False，而TIME_ZONE设置为None，则Django还是会使用默认的America/Chicago时间。

# admin
[有用的设置](https://www.cnblogs.com/wumingxiaoyao/p/6928297.html)


<br/><br/>reference list:
- (Django Migration)[https://realpython.com/django-migrations-a-primer/]
