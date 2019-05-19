## **常用的查询方法**

```py
from django.http import HttpResponse
from .models import User

def add_user(request):

#获取所有记录
    rs = User.objects.all()

#获取第一条数据
    rs = User.objects.first()

#获取最后一条数据
    rs = User.objects.last()

#根据参数提供的条件获取过滤后的记录
    rs = User.objects.filter(name='xiaoming')
    #注意：filter（**kwargs）方法：根据参数提供的提取条件，获取一个过滤后的QuerySet。   

#排除name等于xiaoming的记录
    rs = User.objects.exclude(name='xiaoming')

#获取一个记录对象
    rs = User.objects.get(name='xiaoming')
    #注意：get返回的对象具有唯一性，如果符合条件的对象有多个，则get报错！

#对结果排序order_by
    rs = User.objects.order_by('age')

#多项排序
    rs = User.objects.order_by('age', 'id')

#逆向拍讯
    rs = User.objects.order_by（'-age'）
    #将返回来的QuerySet中Model转换为字典

#获取所有值
    rs = User.objects.all().values()

#获取当前查询到的数据的总数
    rs = User.objcets.count()

    return HttpResponse("查询所有信息")
```

## **常用的查询条件**

查找对象的条件的意思是传给以上方法的一些参数。相当于是SQL语句中的where语句后面的条件，语法为字段名\_\_规则\(是连着连个下划线哦\)

```py
from django.http import HttpResponse
from .models import User

def add_user(request):

#exact相当于等于号
    rs = User.objects.filter(name__exact='xiaoming')

#contains 包含
    rs = User.objects.filter(name__contains='xiao')

#startwith以什么开始,
    rs = User.objects.filter(name__startswith='xiao')

#istartswith 同 startswith相同方法，忽略大小写
    rs = User.objects.filter(name__istartswith='xiao')

#endswith 同 startswith相同用法，以什么结尾
    rs = User.objects.filter(name__endswith='o')

#iendswith 同 istartswith相同用法，以什么结尾，忽略大小写。
    rs = User.objects.filter(name__iendswith='o')

#in 成员所属
    rs = User.objects.filter(age__in=[18,19,20])

#gt大于
    rs = User.objects.filter(age__gt=19)

#gte大于等于
    rs = User.objects.filter(age__gte=19)

#lt小于
    rs = User.objects.filter(age__lt=19)

#lte 小于等于
    rs = User.objects.filter(age__lte=19)

#range 区间
    rs = User.objects.filter(age__range=(18, 20))

#isnull 判断是否为空
    rs = User.objects.filter(city__isnull=True)

    return HttpResponse("查询所有信息")

```

## **常用的字段类型映射关系**

| int | IntegetField |
| :--- | :--- |
| varchar | CharField |
| longtext | TextField |
| date | DateField |
| datetime | DateTimeField |



