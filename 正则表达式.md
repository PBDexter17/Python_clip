
基本urllib用法


```python
import urllib.request
file = urllib.request.urlopen("http://www.baidu.com")

data = file.read()
dataline = file.readline()

fhandle = open("E:/Python_workspace/spider/1.html", "wb")
fhandle.write(data)
fhandle.close()
```


```python
import urllib.request
#url = "https://blog.csdn.net/zm714981790/article/details/51304506"
url = "https://blog.csdn.net/weiwei_pig/article/details/51178226"
file = urllib.request.urlopen(url)
```

### 正则表达式
- 普通字符作为原子


```python
import re
pattern = "yue"
string = "http://yum,iqianyue.com"
result1 = re.search(pattern, string)
print(result1)
```

    <_sre.SRE_Match object; span=(16, 19), match='yue'>
    

- 非打印字符作为原子

字符串中用于格式控制的符号，比如换行符。


```python
import re
pattern = "\n"
string = '''http://yum.iqianyue.com
http://baidu.com'''
result2 = re.search(pattern, string)
print(result2)
```

    <_sre.SRE_Match object; span=(23, 24), match='\n'>
    

- 通用字符作为原子

一个原子用来匹配一类字符。\w匹配任意字母数字下划线，\d匹配任意一个十进制数


```python
import re
pattern = "\w\dpython\w"
string = "abcdfphp345pythony_py"
result3 = re.search(pattern, string)
print(result3)
```

    <_sre.SRE_Match object; span=(9, 18), match='45pythony'>
    

- 原子表


```python
import re
pattern1 = "\w\dpython[xyz]\w"
pattern2 = "\w\dpython[^xyz]\w"
pattern3 = "\w\dpython[xyz]\W"
string = "adcdfphp345pythony_py"
result1 = re.search(pattern1, string)
result2 = re.search(pattern2, string)
result3 = re.search(pattern3, string)
print(result1)
print(result2)
print(result3)
```

    <_sre.SRE_Match object; span=(9, 19), match='45pythony_'>
    None
    None
    

- 元字符

. 可以用来匹配除换行符以外的任意字符。


```python
import re
pattern = ".python..."
string = "abcdfphp345pythony_py"
result1 = re.search(pattern, string)
print(result1)
```

    <_sre.SRE_Match object; span=(10, 20), match='5pythony_p'>
    

边界限制元字符


```python
import re
pattern1 = "^abd"
pattern2 = "^abc"
pattern3 = "py$"
pattern4 = "ay$"
string = "abcdfphp345pythony_py"
result1 = re.search(pattern1, string)
result2 = re.search(pattern2, string)
result3 = re.search(pattern3, string)
result4 = re.search(pattern4, string)

print(result1)
print(result2)
print(result3)
print(result4)
```

    None
    <_sre.SRE_Match object; span=(0, 3), match='abc'>
    <_sre.SRE_Match object; span=(19, 21), match='py'>
    None
    

限定符


```python
import re
pattern1 = "py.*n"
pattern2 = "cd{2}"
pattern3 = "cd{3}"
pattern4 = "cd{2, }"
string = "abcdddfphp345pythony_py"
result1 = re.search(pattern1, string)
result2 = re.search(pattern2, string)
result3 = re.search(pattern3, string)
result4 = re.search(pattern4, string)

print(result1)
print(result2)
print(result3)
print(result4)
```

    <_sre.SRE_Match object; span=(13, 19), match='python'>
    <_sre.SRE_Match object; span=(2, 5), match='cdd'>
    <_sre.SRE_Match object; span=(2, 6), match='cddd'>
    None
    

模式选择符


```python
import re
pattern = "python|php"
string = "abcdfphp345pythony_py"
result1 = re.search(pattern, string)
print(result1)
```

    <_sre.SRE_Match object; span=(5, 8), match='php'>
    

匹配.com 或 .cn的后缀的url网址


```python
import re
pattern = "[a-zA-Z]+://[^\s]*[.com|.cn]" #表达式不能有空格
string = "<a href = 'http://www.baidu.com'>百度首页</a>"
result = re.search(pattern, string)
print(result)
```

    <_sre.SRE_Match object; span=(11, 31), match='http://www.baidu.com'>
    

匹配电话号码


```python
import re
pattern = "\d{4}-\d{7}|\d{3}-\d{8}"
string = "021-6728263653682382265236"
result = re.search(pattern, string)
print(result)
```

    <_sre.SRE_Match object; span=(0, 12), match='021-67282636'>
    

匹配电子邮件地址


```python
import re
pattern = "\w+([.+-]\w+)*@\w+([.-]\w+)*\.\w+([.-]\w+)*"
```
