`from datetime import datetime`
> datetime 模块中还有一个datetime类

# Unix timestamp时间戳
> 我们把1970年1月1日 00:00:00 UTC+00:00时区的时刻称为*epoch time* 记为`0`(1970年以前的时间**timestamp**为负数), 当前时间就是相对与epoch time的秒数, 称为**timestamp**

- [在线时间戳](http://tool.chinaz.com/Tools/unixtime.aspx)
- timestamp与时区无关

# datetime
datetime是有时区的

## timestamp, datetime转换
```python
# timestamp 转 datetime
In [80]: import time
In [81]: t = time.time() # 获得时间戳

In [82]: from datetime import datetime
In [83]: print(datetime.fromtimestamp(t)) # 本地时间
2019-02-11 05:31:28.981512
In [84]: print(datetime.utcfromtimestamp(t)) # UTC标准时区的时间
2019-02-10 21:31:28.981512

# datetime 转 timestamp
In [91]: dt = datetime(2019,1,1,12,20,40,123)

In [92]: dt.timestamp()
Out[92]: 1546316440.000123
```

## datetime 转 str
```python
In [101]: from datetime import datetime
In [102]: now = datetime.now()
In [103]: print(now.strftime('%a, %b %d %H:%M'))
Mon, Feb 11 05:57
In [104]: print(now.strftime('%a, %m %d %H:%M'))
Mon, 02 11 05:57
```

## datetime 加减
用timedelta

## 参考代码
```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

from datetime import datetime, timedelta, timezone

# 获取当前datetime:
now = datetime.now()
print('now =', now)
print('type(now) =', type(now))

# 用指定日期时间创建datetime:
dt = datetime(2015, 4, 19, 12, 20)
print('dt =', dt)

# 把datetime转换为timestamp:
print('datetime -> timestamp:', dt.timestamp())

# 把timestamp转换为datetime:
t = dt.timestamp()
print('timestamp -> datetime:', datetime.fromtimestamp(t))
print('timestamp -> datetime as UTC+0:', datetime.utcfromtimestamp(t))

# 从str读取datetime:
cday = datetime.strptime('2015-6-1 18:19:59', '%Y-%m-%d %H:%M:%S')
print('strptime:', cday)

# 把datetime格式化输出:
print('strftime:', cday.strftime('%a, %b %d %H:%M'))

# 对日期进行加减:
print('current datetime =', cday)
print('current + 10 hours =', cday + timedelta(hours=10))
print('current - 1 day =', cday - timedelta(days=1))
print('current + 2.5 days =', cday + timedelta(days=2, hours=12))

# 把时间从UTC+0时区转换为UTC+8:
utc_dt = datetime.utcnow().replace(tzinfo=timezone.utc)
utc8_dt = utc_dt.astimezone(timezone(timedelta(hours=8)))
print('UTC+0:00 now =', utc_dt)
print('UTC+8:00 now =', utc8_dt)
```

# 正确存储时间的方法
基于"**数据的存储和显示相分离**"的设计原则, 存入数据库应该是表示绝对时间的时间戳, 在显示的时候根据用户设置的时区格式化为正确的字符串

BTW:数据的存储和显示相分离的例子
- 存储柱状图时应该存储表格数据, 而不是图片信息
- HTML和CSS

# django中时间保存
## 时间类型
| django 中     | database 中 |
|:--------------|:------------|
| DateTimeField | datetime    |
| DateField     | date        |
| TimeField     | time        |
这三种类型中都有`auto_now`和`auto_now_add`属性, 默认值是False

- `auto_now = True`
  - 字段保存时会自动保存当前时间, 但要注意每次对其实例执行save()的时候, 都会将当前时间保存, 也就是**不能手动给它存非当前时间的值**
  - 如果使用django自带的admin管理器，那么该字段在admin中是只读的，并且无法进行修改
  - 这个参数在需要存储"最后修改时间"的场景下, 十分方便，常用类似“last-modified”或者"update_time"字段

- `auto_now_add = True`
  - 字段在实例第一次保存的时候会保存当前时间, 不管你在这里是否对其赋值, 此时的值就是创建时间, **以后修改对象时, 字段的值不会自动更新**.
  - 无法在程序中手动为字段赋值, 在admin中该字段是只读的
  - 用在存储"创建时间"的场景下

- 实现可编辑可以用`default = timezone.now()`代替

## default time zone and current time zone
The **default time zone **is the time zone defined by the TIME_ZONE setting.

The current time zone is the time zone that's used for rendering.

You should set the current time zone to the end user's actual time zone with **activate()**. Otherwise, the default time zone is used.

<br/><br/>拓展阅读:
- [time模块和datetime模块](http://gracece.com/2014/10/the-distinction-between-date-and-datetime-in-python/)

<br/>reference list:
- [廖雪峰 datetime](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/001431937554888869fb52b812243dda6103214cd61d0c2000)
- [廖雪峰 正确处理时间](https://www.liaoxuefeng.com/article/0014132675721847f569c3514034f099477472c73b5dee2000)
- [django Time zones](https://docs.djangoproject.com/zh-hans/2.1/topics/i18n/timezones/)
- [django中时间保存](https://blog.csdn.net/liereli/article/details/79790303)
- [django中的日期处理注意事项和自定义时间格式](http://blog.51cto.com/xujpxm/2090382)
