### 字典

**字典特性**

**键（key）唯一性： **字典中的键\(key\)具有唯一性，不存在两个相同的键\(key\)

**无序性：**字典中的键也是无序的，所以不能通过索引取值

**可变性：**字典是可变对象，但是字典的键\(key\)必须是不可变对象

---

### 需求

现在有这样一个需求，要求集合中的每个元素都对应一个值，形成键值对的形式，就像字典一样，在Python中有办法定义这样的数据类型吗？

### 字典两种定义方法

```py
>>> dict = {'name':1,'sex':'男'}  
>>> di = dict(name='rave',age=18)
```

### 字典修改和添加

```py
修改和添加:
di['a'] = 2
di['b'] = 3
-----------------------------------------


修改
>>> di['name'] = 'leva'
>>> di
{'name': 'leva', 'age': 18}
-----------------------------------------

增加
>>> di['sex'] = '男'
>>> di
{'name': 'leva', 'age': 18, 'sex': '男'}
```

### 字典的增删改查

```py
增:
    copy
    setdefault 有则查，无则增
删:
    clear  清空所有键值
    pop    删除一个指定键值
    popitem  随机删除一个键值
改:
    update 更新一个键值
查:
    get 通过键获取值
    keys 通过keys获取所有键
    value 通过value获取所有值
    items 获取所有键与值
-------------------------------------------------------

增
>>> di = {'name': 'leva', 'age': 18, 'sex': '男'}
>>> c = di.copy()  通过copy拷贝获得一个新字典
>>> c
{'name': 'leva', 'age': 18, 'sex': '男'}

>>> c.setdefault('name',888) 有则查，无则增
'leva'
>>> c
{'name': 'leva', 'age': 18, 'sex': '男'}

>>> c.setdefault('addr','sun')  有则查，无则增
'sun'
>>> c
{'name': 'leva', 'age': 18, 'sex': '男', 'addr': 'sun'}
-------------------------------------------------------

改
>>> c.update({'name':'eva'})
>>> c
{'name': 'eva', 'age': 18, 'sex': '男', 'addr': 'sun'}
-------------------------------------------------------

删
>>> c
{'name': 'eva', 'age': 18, 'sex': '男', 'addr': 'sun'}
>>> c.pop('addr') 删除指定键值
'sun'
>>> c
{'name': 'eva', 'age': 18, 'sex': '男'}
>>> c.popitem()
('sex', '男')
>>> c
{'name': 'eva', 'age': 18}
>>> c.clear() 清空所有键值
>>> c
{}
-------------------------------------------------------

查
>>> c
{'name': 'eva', 'age': 18, 'sex': '男', 'addr': 'sun'}
>>> c.get('name')
'eva'

>>> c.keys()
dict_keys(['name', 'age', 'sex', 'addr'])

>>> c.values()
dict_values(['eva', 18, '男', 'sun'])

>>> c.items()
dict_items([('name', 'eva'), ('age', 18), ('sex', '男'), ('addr', 'sun')])
```



