## 插入数据

```py
from django.http import HttpResponse
from .models import Department,Student,Course,Stu_detail

def add_user(request):
    Department.objects.create(d_name='软件')
    Department.objects.create(d_name='设计')
    Department.objects.create(d_name='语言')
    Department.objects.create(d_name='艺术')
    Department.objects.create(d_name='综合')
    Student.objects.create(s_name='小明',department_id=1)
    Student.objects.create(s_name='小红',department_id=2)
    Student.objects.create(s_name='小花',department_id=3)
    Student.objects.create(s_name='小卡',department_id=4)
    Student.objects.create(s_name='小黑',department_id=5)
    return HttpResponse('数据添加成功')
```



