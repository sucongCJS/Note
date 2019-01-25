### makemigrations
`python manage.py makemigrations app_name`
> every you make some changes to your models, you can stored the changes as a migration by do so.

### sqlmigrate
`python manage.py sqlmigrate app_name migrate_file_name(eg.0001)`
> generate the sql command without making migrations

### migrate
`python manage.py migrate`
> apply changes to the database
