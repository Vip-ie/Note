## 插入数据

创建views.py文件内如如下：

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

## 一对多

**查询**

```py
from django.http import HttpResponse
from .models import Department,Student,Course,Stu_detail

def add_user(request):
    d1 = Department.objects.get(d_id=3) # 一个学院实例对象
    s1 = Student.objects.get(s_id=3)  # 一个学生实例对象
    print(s1.department.d_name)       # 学生所属学院的名称
    # 默认情况是student_set
    print(d1.student_set.all())        # 反向查询，学院的学生
    
    # 通过related_name重命名为students,为Student数据模型添加一个重命名related_name=students
    print(d1.students.all())          # 反向查询，学院的学生
    
    #为指定学生id插入一条学生详细信息
    Stu_detail.objects.create(age=18, gender=0, city='石家庄市', student_id=3)
    std = Stu_detail.objects.get(id=1) #实例化一个学生的详细信息
    print(std) #查询一个学生的详细信息
    return HttpResponse('数据添加成功')
```

## 一对一

**查询**

```py
from django.http import HttpResponse
from .models import Department,Student,Course,Stu_detail

def add_user(request): 
    s1 = Student.objects.get(s_id=3)  # 一个学生实例对象
    std = Stu_detail.objects.get(id=1) #实例化一个学生的详细信息
    print(std.student.s_name)    #正向查询一个学生的名字
    print(s1.stu_detail)   #反向查询，直接类名小写
    return HttpResponse('数据添加成功')
```

## 一对多

**数据添加 .add\(\) 添加已经存在的数据**

```py
from django.http import HttpResponse
from .models import Department,Student,Course,Stu_detail

def add_user(request):

    return HttpResponse('数据添加成功')
```

**新建数据 .create\(\)**

```py
from django.http import HttpResponse
from .models import Department,Student,Course,Stu_detail

def add_user(request):

    return HttpResponse('数据添加成功')
```

**.remove  一对多的删除，必须保证外键列允许为空**

```py
from django.http import HttpResponse
from .models import Department,Student,Course,Stu_detail

def add_user(request):

    return HttpResponse('数据添加成功')
```

## 多对多

**添加数据**

```py
from django.http import HttpResponse
from .models import Department,Student,Course,Stu_detail

def add_user(request):

    return HttpResponse('数据添加成功')
```

**多表查询**

```py
from django.http import HttpResponse
from .models import Department,Student,Course,Stu_detail

def add_user(request):

    return HttpResponse('数据添加成功')
```



