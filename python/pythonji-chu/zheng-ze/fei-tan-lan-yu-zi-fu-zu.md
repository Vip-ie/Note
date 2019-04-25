**贪婪模式：**尽量多的提取/匹配出来

```py
import re

my_str ='abbbbbbc'
res = re.findall(r'ab*',my_str)
```

**非贪婪模式：**只要能满足，刚达到标就可以

```py
import re

my_str ='abbbbbbc'
res = re.findall(r'ab*?',my_str)
```



