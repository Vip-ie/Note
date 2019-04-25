### 什么是正则表达式

* **正则表达式是一个工具，用来匹配或者提取字符串**

### 正则表达式主要解决什么问题

判断一个字符串**是否匹配给定的格式**

* 判断用户注册账号是否满足格式

```py
判断用户提交的邮箱的格式是否正确
一个或多个字母或数字@一个或多个字母或数字.com
r'^[a-zA-Z0-0]+@[a-zA-Z0-9]+\.com$'
------------------------------------------------------------
import re
my_str ='3002881567@qq.com'
res = re.findall(r'^[a-zA-Z0-0]+@[a-zA-Z0-9]+\.com$',my_str)
print(res)
```

从一个字符串中**按指定格式提取信息**

* 抓取页面中的连接

### 抓取页面中特定部分数据

```py
import re

my_str ='''
<div class="menu_le">
<a href="/flash_fl/2_1.htm">动作</a>
<a href="/flash_fl/3_1.htm">体育</a>
<a href="/flash_fl/5_1.htm">益智</a>
<a href="/flash_fl/4_1.htm">射击</a>
<a href="/flash_fl/6_1.htm">冒险</a>
<a href="/flash_fl/7_1.htm">棋牌</a>
<a href="/flash_fl/8_1.htm">策略</a>
<a href="/flash_fl/12_1.htm">休闲</a>
<a href="/special/195.htm">女生</a>
<a href="/flash_fl/16_1.htm">装扮</a>
<a href="/flash_fl/13_1.htm">儿童</a>
<a href="/special/90.htm">过关</a>
<a href="/special/1.htm">双人</a>

</div>
'''
res =re.findall(r'href="(.*?),my_str')#只会提取括号里面的内容
for i in res:
    print(i)
返回
/flash_fl/2_1.htm
/flash_fl/3_1.htm
/flash_fl/5_1.htm
/flash_fl/4_1.htm
/flash_fl/6_1.htm
/flash_fl/7_1.htm
/flash_fl/8_1.htm
/flash_fl/12_1.htm
/special/195.htm
/flash_fl/16_1.htm
/flash_fl/13_1.htm
/special/90.htm
/special/1.htm
```



