### 什么是元字符

本身具有特殊含义的字符

### 常用元字符有那些

`. ^ $ {} * + ? | []`**都叫通配元字符**

```py
通配元字符.代表任意一个字符
锚点元字符 ^锁定首行 $锁定行尾 
单词边界\b(不属于元字符) 单词之间以空格隔开，在单词两边加上\b匹配单词
{}控制次数{2，6}表示2到6之间任意个数都可以匹配
-------------------------------------------------
控制次数，修饰的是前面的规则
* 任意多个字符，匹配*前面的字符
+ 至少要有一个到N个
? 大于一个就匹配不到
-------------------------------------------------
| 选择元字符 类似python中的or
[...] 字符组，中括号代表一个字符
[^...]反向字符类
每个元字符都可以结合使用
-------------------------------------------------
.实例
import re

my_str ='华美小同学正在玩泥巴，哈哈 华美小同学的'
res = re.findall(r'华美小同学...',my_str)   #不加点匹配的是写入文字内容，每增加一个点多匹配一个字符
print(res) #返回['华美小同学正在玩']
-------------------------------------------------
^实例

my_str ='华美小同学正在玩泥巴，哈哈 华美小同学的'
res = re.findall(r'^华美小同学',my_str) #匹配华美小同学开头字符，如果没有华美小同学开头匹配不到
print(res) #返回['华美小同学正在玩']
$实例 

my_str ='华美小同学正在玩泥巴，哈哈 华美小同学'
res = re.findall(r'华美小同学$',my_str)#匹配华美小同学结尾字符，如果没有华美小同学匹配不到
print(res) #返回['华美小同学']
-------------------------------------------------

\b实例
my_str ='hello python adfahello python'
res = re.findall(r'\bhello\b',my_str) #默认识别单词
print(res) #返回 ['hello']
-------------------------------------------------

{}实例
my_str ='abbbbbbc'

res = re.findall(r'ab{2,6}c',my_str) #{2,6}表示2到6之间的个数，
{2,}表示从2到无限大，{,6}表示最多匹配6个
print(res)#返回['abbbbbbc']
-------------------------------------------------

[]实例
my_str ='abb12bb33b4444bc'
res = re.findall(r'[0-9]{2,6}',my_str) #匹配数字
print(res)#返回['12', '33', '4444']
-------------------------------------------------

*实例
my_str ='abbbbbbc'
res = re.findall(r'ab*c',my_str) #*匹配任意多个字符
print(res)#返回['abbbbbbc']
-------------------------------------------------
+实例
my_str ='abbbbbbc'

res = re.findall(r'ab+c',my_str) #*匹配至少要有一个到N个
print(res)#返回['abbbbbbc']
-------------------------------------------------
?实例
my_str ='ac'
res = re.findall(r'ab?c',my_str) #*匹配大于一个就匹配不到了
print(res)#返回['ac']
-------------------------------------------------

|实例
my_str ='hello world python world'
res = re.findall(r'hello|python|world',my_str) 
print(res)#返回['hello', 'world', 'python', 'world']
-------------------------------------------------

[]实例
my_str ='hello world python world hello hello python world python'
res = re.findall(r'[he]',my_str) #匹配出所有中括号内的字符
print(res)#返回['h', 'e', 'h', 'h', 'e', 'h', 'e', 'h', 'h']

my_str ='abbc abbd abbe'
res = re.findall(r'abb[abc]',my_str) #匹配出所有中括号内的字符
print(res)#返回['abbc']

my_str ='ab3bc abb4d abbe'
res = re.findall(r'[a-zA-Z0-9]{4}',my_str)  #匹配4个任意字符
print(res)#返回['ab3b', 'abb4', 'abbe']
-------------------------------------------------

反向字符类
my_str ='#ab3bc a4bb$d abb%e'
res = re.findall(r'[^a-zA-Z0-9]',my_str) #匹配反向字符类
print(res) #返回['#', ' ', '$', ' ', '%']
```

### ![](/assets/yuanzufu.png)

### 转义元字符\

```py
import re

my_str ='abc.cs'
res =re.findall(r'ab|\.',my_str) #
print(res)
```

### 



