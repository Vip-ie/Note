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
    

    return HttpResponse("查询所有信息")
```



