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

[link](https://realpython.com/django-migrations-a-primer/)

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
如果USE_TZ 设置为False，而TIME_ZONE设置为None，则Django还是会使用默认的America/Chicago时间

# admin
[有用的设置](https://www.cnblogs.com/wumingxiaoyao/p/6928297.html)

# 注意事项

- `runserver`提供的是一个用于开发的web服务器, 你就无需配置一个类似Ngnix的生产服务器, 就能让站点运行起来, 但这是简易并且不安全的, 不能用于生产环境

# useful tips

## 渲染页面

```python
from django.shortcuts import render

from .models import Question


def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    context = {'latest_question_list': latest_question_list}
    return render(request, 'polls/index.html', context)

# 通用模板版本 得改url.py, 见`通用模板`
class IndexView(generic.ListView):
    template_name = 'polls/index.html'
    context_object_name = 'latest_question_list'

    def get_queryset(self):
        """Return the last five published questions."""
        return Question.objects.order_by('-pub_date')[:5]
```

## 404

```python
# polls/views.py

from django.http import Http404
from django.shortcuts import render

from .models import Question
# ...
def detail(request, question_id):
    try:
        question = Question.objects.get(pk=question_id)
    except Question.DoesNotExist:
        raise Http404("Question does not exist")
    return render(request, 'polls/detail.html', {'question': question})
```

- 就像render函数一样，Django同样为你提供了一个偷懒的方式，替代上面的多行代码，那就是`get_object_or_404()`方法，参考下面的代码：

  polls/views.py

  ```python
  from django.shortcuts import get_object_or_404, render
  
  from .models import Question
  # ...
  def detail(request, question_id):
      question = get_object_or_404(Question, pk=question_id)
      return render(request, 'polls/detail.html', {'question': question})
  ```

  - 一些受控的耦合将会被包含在 `django.shortcuts` 模块中, 捕获异常并调用视图显示是一个耦合
  - 为什么我们使用辅助函数`get_object_or_404()`而不是自己捕获`ObjectDoesNotExist`异常呢？还有，为什么模型 API 不直接抛出`ObjectDoesNotExist`而是抛出 `Http404`呢？因为这样做会增加模型层和视图层的耦合性。指导 Django 设计的最重要的思想之一就是要保证松散耦合

## 模板

```django
<h1>{{ question.question_text }}</h1>
<ul>
{% for choice in question.choice_set.all %}
    <li>{{ choice.choice_text }}</li>
{% endfor %}
</ul>
```

在模板系统中圆点`.`是万能的魔法师，你可以用它访问对象的属性。在例子`{{ question.question_text }}`中，DJango首先会在question对象中尝试查找一个字典，如果失败，则尝试查找属性，如果再失败，则尝试作为列表的索引进行查询

### 通用模板

[link](https://www.liujiangblog.com/course/django/90)

- DetailView

  - 使用模型Queation的话, `question`变量会被自动提供, 可以在html中使用

    ```
    class ResultsView(generic.DetailView):
        model = Question
        template_name = 'polls/results.html'
    ```

- ListView

  - 使用模型Queation的话, `question_list`变量会被自动提供, 可以用`context_object_name`替换掉

    ```
    class IndexView(generic.ListView):
        template_name = 'polls/index.html'
        context_object_name = 'latest_question_list'
    
        def get_queryset(self):
            """Return the last five published questions."""
            return Question.objects.order_by('-pub_date')[:5]
    ```

### url

```django
<li><a href="/polls/{{ question.id }}/">{{ question.question_text }}</a></li>

// 等价于
<li><a href="{% url 'detail' question.id %}">{{ question.question_text }}</a></li> # polls/index.html
path('<int:question_id>/', views.detail, name='detail') # polls/urls.py
```

#### 命名空间

只有一个app可以不写命名空间，但是在现实中很显然会有5个、10个、更多的app同时存在一个项目中。这些app的url可能会相同, 要区分这些app之间的URL name要用命名空间

```python
from django.urls import path

from . import views

app_name = 'polls' # 注意这里!!!
urlpatterns = [
    path('', views.index, name='index'),
    path('<int:question_id>/', views.detail, name='detail'),
    path('<int:question_id>/results/', views.results, name='results'),
    path('<int:question_id>/vote/', views.vote, name='vote'),
]
```

```django
<li><a href="{% url 'polls:detail' question.id %}">{{ question.question_text }}</a></li>
```

### form

[link](https://www.liujiangblog.com/course/django/90)

#### 提交

```django
<h1>{{ question.question_text }}</h1>

{% if error_message %}<p><strong>{{ error_message }}</strong></p>{% endif %}

<form action="{% url 'polls:vote' question.id %}" method="post">
{% csrf_token %}
{% for choice in question.choice_set.all %}
    <input type="radio" name="choice" id="choice{{ forloop.counter }}" value="{{ choice.id }}">
    <label for="choice{{ forloop.counter }}">{{ choice.choice_text }}</label><br>
{% endfor %}
<input type="submit" value="Vote">
</form>
```

- forloop.counter是DJango模板系统专门提供的一个变量，用来表示你当前循环的次数，一般用来给循环项目添加有序数标。
- 由于我们发送了一个POST请求，就必须考虑一个跨站请求伪造的安全问题，简称CSRF（具体含义请百度）。Django为你提供了一个简单的方法来避免这个困扰，那就是在form表单内添加一条{% csrf_token %}标签，标签名不可更改，固定格式，位置任意，只要是在form表单内。这个方法对form表单的提交方式方便好使，但如果是用ajax的方式提交数据，那么就不能用这个方法了。

#### 接收

```python
from django.http import HttpResponse, HttpResponseRedirect
from django.shortcuts import get_object_or_404, render
from django.urls import reverse

from .models import Choice, Question
# ...
def vote(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    try:
        selected_choice = question.choice_set.get(pk=request.POST['choice'])
    except (KeyError, Choice.DoesNotExist):     
        return render(request, 'polls/detail.html', {
            'question': question,
            'error_message': "You didn't select a choice.",
        })
    else:
        selected_choice.votes += 1
        selected_choice.save()       
        return HttpResponseRedirect(reverse('polls:results', args=(question.id,)))

def results(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    return render(request, 'polls/results.html', {'question': question})
```

- 在选择计数器加一后，返回的是一个`HttpResponseRedirect`而不是先前我们常用的`HttpResponse`。HttpResponseRedirect需要一个参数：重定向的URL。这里有一个建议，当你成功处理POST数据后，应当保持一个良好的习惯，始终返回一个HttpResponseRedirect。这不仅仅是对Django而言，它是一个良好的WEB开发习惯