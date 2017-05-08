#### 4-1 拆分含有多个分隔符的字符串

方法一：对于单个分隔符，直接使用s.split() 方法进行分割

~~~python
s = "abc def ghi jkl"
>>> s.split()    # 默认以空白字符(空格，回车，Tab等)进行分割
['abc', 'def', 'ghi', 'jkl']
~~~

方法二：使用re.split() 对多种分隔符的字符串进行切割

~~~python
>>> import re
>>> s = "abc dfg&ghi$jkl"
>>> re.split("[ &$]", s)
['abc', 'dfg', 'ghi', 'jkl']
~~~

#### 4-2 判断字符串a是否以字符串b开头或者结尾

方法：可以直接使用str.startswith()和str.endswith() 进行判断

~~~python
>>> [name for name in s if name.endswith('.py')]
['a.py', 'f.py']
>>> #当有多项匹配时使用元组
>>> [name for name in s if name.endswith(('.py', '.c'))]
['a.py', 'e.c', 'f.py’]
~~~



#### 4-4 将多个小字符串拼接成长字符串：

方法一： 使用 ‘+’ 连接符将其连接起来：

~~~python
>>> str = ['abc','def','ghi','gkl']
>>> s = ''
>>> for i in str:
...     s += i
>>> s
'abcdefghigkl'
~~~

方法二： 使用 join 方法，对其进行连接(推荐)

~~~python
>>> str = ['abc','def','ghi','gkl']
>>> '.'.join(str)
'abc.def.ghi.gkl'
>>> ''.join(str)
‘abcdefghigkl'
~~~

当连接混有数字和字符串的列表时，列表生成式比列表解析式效率要高：

~~~python
>>> str_l = ['abc', 123, 45, 'efg']
>>> ''.join([str(i) for i in str_l])Out[3]:
'abc12345efg'
>>> ''.join((str(i) for i in str_l))Out[4]: ‘abc12345efg'
~~~

#### 4-5 对字符串进行左中右对齐

方法一：使用str.ljust(), str.rjust() 和str.center()进行左中右对齐

~~~python
>>>d = {"abcdedfg":1, "hijklmn":2, "opq":3,"rst":4, "uvw":5, "xyz":6}
>>>str = "abdgd"
>>> str.ljust(20) #默认的填充为空格
'abdgd               '
>>>str.rjust(20, "+")Out[8]:
'+++++++++++++++abdgd'
>>>str.center(20,'=')Out[9]:
'=======abdgd========'
~~~

方法二: 使用 format 方法， 传递类似于’<20’, ‘>20’,’^20’等参数，完成同样的任务。

~~~
>>>format(str, '<20') # 等价于str.ljust(20)
'abdgd               '
>>>format(str, '>20') Out[12]:
'               abdgd'
>>>format(str, '^20') Out[13]:
'       abdgd        ‘
~~~

\# 对字典对齐打印输出

~~~python
>>>w = max(map(len, d.keys()))
>>>for k in d:
...:     print k.ljust(w),':', d[k]    
...:
opq      : 3
xyz      : 6
uvw      : 5
hijklmn  : 2
rst      : 4
abcdedfg : 1
~~~

#### 4-6 字符串的删除和替换：

方法一: 使用strip(),lstrip(),rstrip()去除字符串两端的字符

~~~python
>>> s = "    zhaozhichao@gmail.com    "
>>> s.strip() # 默认是去除两端的空格,等价于 s.strip(" “)
'zhaozhichao@gmail.com'
>>> s.lstrip()  # 去除左端空格
'zhaozhichao@gmail.com    '
>>> s.rstrip()  # 去除右端空格
'    zhaozhichao@gmail.com’
~~~

方法二：去除中间固定位置的字符，可以使用切片+拼接方式

~~~python
>>> s = "abc\t123"
>>> s[:3] + s[4:]
‘abc123'
~~~

方法三：使用字符串的replace()函数 或者正则表达式re.sub()删除任意位置的字符

~~~python
>>> s = "abcd\tefg\nhijk\t"
>>> s.replace("\t", “")
'abcdefg\nhijk'
>>> # replace()只能替换单个字符，需要替换多个字符的时候，可以使用re.sub方法
>>> import re
>>> re.sub("[\r\n]", "", s)
'abcdefghijk'
~~~

方法四： 使用字符串的translate() 方法，来实现字符之间的映射

~~~python
>>> s = xyz124214abc # 替换为abc124214xyz
>>> import string 
>>> string.maketrans('abcxyz','xyzabc')
'\x00\x01\x02\x03\x04\x05\x06\x07\x08\t\n\x0b\x0c\r\x0e\x0f\x10\x11\x12\x13\x14\x15\x16\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f !"#$%&\'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`xyzdefghijklmnopqrstuvwabc{|}~\x7f\x80\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x8d\x8e\x8f\x90\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f\xa0\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb\xbc\xbd\xbe\xbf\xc0\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf\xe0\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xeb\xec\xed\xee\xef\xf0\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff'
>>> s.translate(string.maketrans('abcxyz','xyzabc'))
‘xyz124214abc'
~~~

