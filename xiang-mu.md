## 项目目录说明

```
├── app.py                       项目总入口
├── handlers                     项目路由逻辑业务目录
│   ├── __init__.py
│   └── main.py                  项目业务逻辑
├── utils                        项目辅助函数
│   ├── __init__.py
│   └── photo.py                 项目图片路径方法
├── models
│   ├── account.py
│   ├── db.py
│   └── __init__.py
├── static                       项目总静态文件目录
└── templates                    项目总模板目录
        ├── base.html            项目总模板文件
        ├── expolore.html        项目功能模块模板文件
        └──index.html           项目功能模块模板文件
```





项目目录

```
Module
    ├── alembic              #数据库版本控制
    ├── app.py 
    ├── deploy               #维护文件
    ├── handlers             #总路由函数入口
    │   └── __init__.py
    ├── Modules              #数据库相关函数建模
    │   └── __init__.py
    ├── requirements.txt
    ├── templates            #模板相关
    │   └── static
    └── utils                #辅助函数
        └── __init__.py

```



