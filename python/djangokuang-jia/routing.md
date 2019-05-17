# url路由基模板渲染

* **url基本概念及格式**
* **path和re\_path**
* **模板路径配置**
* **渲染模板方式**

---

## URL概念

URL（Uniform Resoure Locator）统一资源定位符是对可以从互联网上得到的资源和访问方法的一种简洁的表示，是互联网上标准资源的地址。互联网上的每个文件都是一个唯一的URL，它包含的信息指出文件的位置及浏览器应该怎么处理它。

## URL格式

* [http://127.0.0.1:8000/hello/](http://127.0.0.1:8000/hello/)
* **URL解释：**
* **schema://host\[:port\#\]/path/..\[?query-string\]\[\#anchor\]**
* **schema:指定使用的协议（例如：http，https，ftp）**
* **host：Http服务器的IP地址或者域名**
* **port：端口，http默认是80端口**
* **path：访问资源的路径**
* **query-string：发送给http服务器的数据**
* **anchor：锚点**

## urls.py的作用

URL配置（RULconf）就像是Django所支撑网站的目录。它的本质是URL模式以及要为该URL模式调用的视图函数之间的映射表。以这样的方式告诉Django，对于那个URL调用那段代码。url的加载就是从配置文件中开始。

**url例子：**

1.在项目目录下ruls.py文件

```py
from django.contrib import admin
from django.urls import path
from . import views

urlpatterns = [
    path('admin/', admin,site.urls),
    path('test/django/', views.test1),
    path('test/<xx>/', views.test2),
]
```

1. 在项目目录创建了一个views.py文件

```
from django.http import HttpResponse

def test(request):
    return HttpResponse('hello django!!!')

def test2(request):
    return HttpResponse('hello python')
```

## path基本规则

```
使用尖括号（<>）从url中捕获值。
包含一个转化器类型（converter type）没有转化器，将匹配任何字符串，当然也包括了/字符。
            ↓
path('test/<xx>/',views.test)
                      ↑　
当前面的url匹配成功后就会调用后面的是视图函数。
```



