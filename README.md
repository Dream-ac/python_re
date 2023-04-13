#re
# 一、 限定符

#### （1）*

```python
xy*g
匹配 'y' 0次或多次
```

#### （2）+

```python
xy+g 
匹配 'y' 多次
```

#### （3）{}

```python
xy{5}g
匹配 'y' 出现5次

xy{2,5}g
匹配 'y' 2-5次

xy{2,}g
匹配 'y' 2次以上
```

#### （4）?

```python
likes?
匹配 's' 0|1次
```

#### （5）()

```python
(xy)+
匹配 'xy' 多次
```

#### （6）|

```python
play the (pinao|guitar)
匹配 pinao或guitar
```

#### （7）[]+

```python
[xyg]+
匹配的字符只能取自xyg
[a-z]+
匹配a-z的小写字母
[A-Z]+
匹配A-Z的大写字母
[a-zA-Z]+
匹配所有字母
[a-zA-Z0-9]+
匹配所有字母数字
[^a-zA-Z0-9]+
匹配除'^'后面列出的字符之外的字符
```

# 二、元字符

```python
\d
匹配数字字符
\D
非数字字符
\w
单词字符(包含所有的英文字符、数字、下划线)
\W
非单词字符
\s
空白字符(包括空格、制表符和换行符)
\S
非空白字符
.
任意字符不包括换行符
^
匹配行首(与[]中的'^'不同)
$
匹配行尾
```

# 三、贪婪匹配和懒惰匹配

```python
示例：
<div>
    <span>小飞的西瓜频:https://v.ixigua.com/2asfSbf</span>
</div>

贪婪匹配：<.+> 匹配尽可能多的字符
匹配结果：
<div>
    <span>小飞的西瓜频:https://v.ixigua.com/2asfSbf</span>
</div>

懒惰匹配：<.+?> 匹配尽可能少的字符
匹配结果：
<div><span>             </span></div>

```

# 四、手机号匹配

```python
^(13[0-9]|14[5-9]|15[0-35-9])\d{8}$
以13、14、15开头 以11位数字结尾

exp:
13880689999      15591888888
ab13430826666
15591558888
1339737977777
14763111111

匹配结果：
15591558888
14763111111


```

## （1）\b 

单词字符的边界

11位号码之后为空白字符或边界 

边界：后面没有任何内容

```python
^(13[0-9]|14[5-9]|15[0-35-9])\d{8}\b
匹配结果：
13880689999
15591558888
14763111111

\b(13[0-9]|14[5-9]|15[0-35-9])\d{8}\b
匹配结果：
13880689999      15591888888
15591558888
14763111111
原因 '^' 匹配一行行首
```

# 五、正则表达式

```python
import re
```

## re.findall()

```python
print(re.findall('.+', 'abc\ndef\ng'))
打印结果：
['abc', 'def', 'g']

匹配换行
import re
print(re.findall('.+', 'abc\ndef\ng', flags=re.DOTALL))
打印结果：
['abc\ndef\ng']


```

### re.flags

```python
re.I(re.IGNORECASE)
不区分大小写

re.M(re.MULTLINE)
^x
匹配多行以x开头的字符串，否则只匹配第一行以'x'开头的字符串

re.S(re.DOTALL)
可以匹配换行符
具体参考官方文档：
https://docs.python.org/3/library/re.html#flags
```

### 手机号匹配2

```python
print(re.findall(r'\b(13[0-9]|14[5-9]|15[0-35-9])\d{8}\b'),phonenum)
匹配结果：
['138', '155', '155', '147']
原因编程语言将'()'视为匹配边界
解决方法
print(re.findall(r'\b(?:13[0-9]|14[5-9]|15[0-35-9])\d{8}\b'),phonenum)
```

## re.serach()

```python
res = re.search('\d{3,4}-\d{7,8}', 'Tel:028-7654321')
print(res)
results：
	<re.Match object; span(4,15), match='028-7654321'>
获取索引:
print(res.span())

res = re.search('(\d{3,4})-(\d{7,8})', 'Tel:028-7654321')

print(res.group(1))
results: 028

print(res.group(2))
results: 7654321
    

```



