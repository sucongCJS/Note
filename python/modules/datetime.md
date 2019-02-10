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

# 正确存储时间的方法
基于"**数据的存储和显示相分离**"的设计原则, 存入数据库应该是表示绝对时间的时间戳, 在显示的时候根据用户设置的时区格式化为正确的字符串

BTW:数据的存储和显示相分离的例子
- 存储柱状图时应该存储表格数据, 而不是图片信息
- HTML和CSS

<br/><br/>拓展阅读:
- [time模块和datetime模块](http://gracece.com/2014/10/the-distinction-between-date-and-datetime-in-python/)

<br/><br/>reference list:
- [廖雪峰 datetime](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/001431937554888869fb52b812243dda6103214cd61d0c2000)
- [廖雪峰 正确处理时间](https://www.liaoxuefeng.com/article/0014132675721847f569c3514034f099477472c73b5dee2000)
