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

## **常用的字段类型**

1. **IntegerField :整型，映射到数据库中的int类型。**
2. **CharField:字符类型，映射到数据库中的varchar类型，通过max\_length指定最大长度。**
3. **TextField:文本类型，映射到数据库中的text类型。**
4. **BooleanField:布尔类型，映射到数据库中的tinyint类型，在使用的时候，传递True/False进去。如果要可以为空，则用NullBooleanField。**
5. **DateField:日期类型，没有时间。映射到数据库中是date类型，在使用的时候，可以设置DateField.auto\_now每次保存对象时，自动设置该字段为当前时间。设置DateField.auto\_now\_add当对象第一次被创建时自动设置当前时间。**
6. **DateTimeField: 日期时间类型。映射到数据库中的是datetime类型，在使用的时候，传递datetime.datetime\(\)进去。**

## Field**的常用参数**

* **primary\_key:指定是否为主键。**
* **unique:指定是否唯一。**
* **null:指定是否为空，默认为False。**
* **blank:等于True时form表单验证时可以为空，默认为False。**
* **default:设置默认值。**
* **DateField.auto\_now:每次修改都会将当前时间更新进去，只有调用，QuerySet.update方法将不会调用。这个参数只是Date和DateTime以及TimModel.save\(\)方法才会调用e类才有的。**
* **DateField.auto\_now\_add:第一次添加进去，都会将当前时间设置进去。以后修改，不会修改这个值**

## 表关系的实现

## ![](/assets/orm02.png)创建表模型

```

```



