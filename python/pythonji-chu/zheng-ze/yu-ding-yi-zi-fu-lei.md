|  |
| :--- |


| 预定义字符类 | 说明 | 对等字符类 |
| :--- | :--- | :--- |
| \d | 任一数字字符 | \[0-9\] |
| \D | 任一非数字字符 | \[^0-9\] |
| \s | 任一空白符 | \[\t\n\xOB\f\r\] |
| \S | 任一非空白符 | \[^\t\n\xOB\f\r\] |
| \w | 任一字母数字字符 | \[a-zA-Z0-9\] |
| \W | 任一非字母数字字符 | \[^a-zA-Z0-9\] |

```py
import re

my_str ='ab3bc abb4d abbe'
res = re.findall(r'\d',my_str)
print(res)#返回['3', '4']
```



