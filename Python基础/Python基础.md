



# 2020.4.2 Python 基础

> 作者邮箱：yangjuehui06@outlook.com
>
> 参考书目：《父与子的编程之旅》《笨方法学Python》

<u>基于Python3.6.8</u> 安装和部署环境不再赘述

IDE：<u>idle</u> 为什么不用Pycharm，因为前面用不上（我也不会）

## 1.赋值、输出与输入

### 1.1	赋值

```python
//赋值
first=1
second=2
third=3
print(first+second-third)
——
-1

```

* 将1赋值给first 最后将他们相加

* <u>输出格式print()输出数值，print("")输出字符</u>

  //给变量赋值的时候，字符串需要引号，而数值不需要

  //eg. '4'≠4

  ```python
  print'first'+'second'
  ——#这个线下面表示输出结果
  first+second
  ```

  

  ```python
  #字符输出 (在python中，#表示单行注释)
  first=1
  secon=2
  third=3
  print('first+second+third')
  ——
  first+second+third 
  ```

### 1.2 输入

python和其余的大多数编程语言一样，需要通过输入才能做到信息交互

```python
input()	#和print一样 必须有！英文版本的括号
		#他只能记录用户输入的字符串！！
```

### 1.3 第一个小程序

```python
print('who do you think i am?')
input()
print('oh!yes!')
```

当然，可以对他进行无限的插入：

```python
print('who do you think i am?')
input()
print('how old are you?')
input()
print('wow!awesome!')
```

注意！在python3中，input()所键入的都是字符串。就算输入数字，得到的也是含有数字的字符串而不是数值。

> 当然，这个程序有点蠢，他只会回答这三句

## 2.变量

### 2.1	基础部分

所谓变量，就是可变化的量，在python中命名一个变量非常简单，给他一个名字，然后赋值给他

栗子：

```python
theacher='Mr.Yang' #等号的作用就是右边赋值给左边
print(teacher)
——
Mr.Yang
```

```python
score=1
score=score+1
print(score)
——
2
```

* 变量大小写是有区别的 //SCORE、score、Score是完全不同的变量
* python中变量以字母开头

```python
#test
DayPerHour=7
HoursPerDay=24
MinutePerHour=60
MinutePerWeek=(DayPerHour*HoursPerDay*MinutePerHour)
print(MinutePerWeek)
--
10080

```

//遇到的错误

![image-20200401123854500](C:\Users\use\AppData\Roaming\Typora\typora-user-images\image-20200401123854500.png)

！一定要注意变量名是否一致

```python
#当然，我们还能这么做
name=input()
print(name)
```

### 2.2	变量的命名方式

> 本来在之前细碎的写了，但是后面写东西的时候犯了这样的错误，遂过来补一下//2020.4.2
>
> 变量的名字不是想起就能起滴~~~

命名规则：

1.第一个字符必须是字母或者下划线

2.剩下的部分可以是字母、下划线或者是数字0-9

3.变量名称是对大小写非常敏感的，大小写不同变量不同

### 2.3	数据类型（初级）

```python
a=10		#int 			整数
a=1.3		#float			浮点数
a=Ture		#Ture/False		真值
a='hello'	#字符串（可以用双引号）			
```

### 2.4	数据类型（bool）



**逻辑判断**在编程中是非常重要的，日后基本上大量的程序都建立在“真”与“假”的基本逻辑之上，bool所表示的就是这种最本质的**True/False**

举个栗子：

```python
a=1<3
print(a)
b=1
c=3
print(b>c)
======================== 
True	#a=1<3	的结果
False	#B>C	的结果
>>> 
```

通过大于号和小于号来比较两个数值，我们就得到了一个bool值。

“<”和“>”在编程语言中被称之为比较运算符/关系运算符

```python
#常见的比较运算符/关系运算符
#	">"				大于
#	"<"				小于
#	">="			大于等于	
#	"<="			小于等于
#	"=="			等于（是为了区别赋值符号）
#	"!="			不等于
#	not				非	//若x为Ture，则not x为False
#	and				与	//若x为Ture，且y为Ture，则x and y 为Ture
#	or				或	//若x、y中至少有一个为Ture，则x or y为Ture
```





### 2.5	第一个程序进化版

```python
#所以，在第一章里的小程序可以做一个简要变化
print('who do you think i am?')
you=input()
print('wow,awesome! i am a')
print(you)

```



## 3.基本的数学运算

### 3.1	操作符

#### 3.1.1	加减乘除

+、-、*和/都被成为操作符，是因为他们都会操作符号两边的数字。=号也是一个操作符，也称作赋值操作符（assignment operator）

```python
onenum+twonum
#onenum 与twonum 被称为操作数
```

* Python中的数学运算会遵循正常的数学运算顺序

* 相同的，可以使用（）来改变顺序

  ```python
  print(2+2*3)
  --
  8
  ```

  ```python
  print((2+2)*3)
  --
  12
  ```

#### 3.1.2    指数与取余



```python
#幂运算
print(2**2)
--
4
```

> 在很多其他语言中幂运算使用‘^’符号，但在Python中，‘^’符号是别的意思

```python
#正常除法
print(7/3)
--
2.333333333333333()

#取余
print(7%3)
--
1

```

#### 3.1.3	自增与自减

在之前//变量里有过

```python
score=1
score=score+1
print(score)
```

在Python中自增自减也有自己的表达方式

```python
score=1
score+=1
#score-=1
print (score)
```

#### 3.1.4	极大与极小

在计算的时候有时候会产生一些非常大的数字

```python
print 381761747874091.2*3136128481.1
--
1.1972538905024548e+24
```

这里的e是指e计数法（E-notation），处理很大的数有时候全显示出来会很不方便，所会用e来表示中间的位数。

同样的，相对于E计数法，还有指数计数法。两者要区分开

```
3**5表示3^5,或3的5次幂，也就是3*3*3*3*3，等于243
3e5表示3*10**5或者3乘以10的5次幂，也就是3*10*10*10*10*10，结果等于300000
```

**可以用Python来将数字转化为E计数法**

```python
a=17000000
print("%E"%a)
```

### 3.2 小练习

1. 三个人在餐厅吃饭，想要AA。总共花费35.27美元，他们想要保留15%作为消费，每个人需要支付多少？
2. 计算一个12.5m*16.7m的举行房间的面积和周长
3. 设计一个能转换华氏度和摄氏度的小程序。tips：C=5/9*（F-32）
4. 编写一个程序，计算以80km/h的速度行驶200km需要多长时间

```python
#只写下第一题哈，还是蛮简单的
print(35.27*(1-0.15)/3)
```

## 4.数据类型（进阶）

### 4.1数据类型的变换

#### 4.1.1 思考

首先，思考下上面3.2的小练习的第一题。

若将题目改为”3个人在餐厅吃饭，想要AA。总共花费X美元，他们想要保留15%作为消费，每个人需要支付多少？“

那么需要如何操作？

```python
#这是我第一次写的
totaldollar=input()
people=3
perdollar=(totaldollar*(1-0.15)/people)
print(perdollar)
#当然，最后报错了

```

这是为啥呢？（恐龙问号）

#### 4.1.2 数据变换

因为在Python中，input（）函数，只能记录用户输入的字符串，那么在后面perdollar的运算中，由于字符串不能运算，所以会报错，在这里就要先把他的键入类型由字符串改变为数值，才能继续运算。

```python
#在python中，实际上不能称之为转换，而是直接用原有的东西创建出了一个你所想要的新东西。
#在他们的后面，一定要有（），因为他们不是Python的关键字（比如print），而是内置函数
float()	#从一个字符串或者整数创建一个新的浮点数
int()	#从...创建一个新的整数
str()	#从一个数（任何类型）创建出一个新的字符串
```

那么先简单操作一下，栗子：

```python
a=12
b=float(a)
print(a)
print(b)
--
a=12
b=12.0	#这里可以看到，改变数据类型不会改变数据，他只是创建了一个新的值
```

```python
#当然反过来也一样
a=12.0
b=int(a)
print(a)
print(b)
--
a=12.0
b=12
```

将字符串转化为浮点数呢

```python
a='99.99'
c=float(a)
print(c)
```

* 浮点数转化为整数：

  ```python
  a=999.9
  print(int(a))
  ======================== 
  999	#可以看到浮点型数据在向整数转化的过程中，向下取整了
  >>> 
  
  ```

  

#### 4.1.3 查看数据类型

Python可以快捷查询一个数据是什么数据类型

```python
a=99.99
b=99
c='99'
print(type(a))
print(type(b))
print(type(c))
--
<class 'float'>
<class 'int'>
<class 'str'>
>>> 
```

#### 4.1.4 数据转换错误

```python
a='freedom！'
print(float(a))
--
Traceback (most recent call last):
  File "C:/Python/test3.py", line 2, in <module>
    print(float(a))
ValueError: could not convert string to float: 'freedom！'
>>> 
```

这是为啥呢，是因为Python无法从”freedom！“这个字符串上建立一个新的浮点型数据（整数同理）

#### 4.1.5 思考（进阶版本）

之前在4.1.1里面，提到的那个问题，现在知道是咋回事了吧hh，其实就是因为数据类型不对，需要转换

```python
#正确版本
totaldollar=input()
a1=float(totaldollar)
people=input()
b1=int(people)
perdollar=(a1*(1-0.15)/b1)
print(perdollar)
======================== 
99.99
3
28.330499999999997
>>> 
```

这样就可以输入数字，然后计算出结果了hhh

但是这样的话，最后的输出页面太不美观了，我们可以稍微改进一下



```python
#改进版
print("please input totaldollar:  ")
totaldollar=float(input())		#这里要注意，float(input())是一种简化的写法
print("how many people?")
people=int(input())
perdollar=(totaldollar*(1-0.15)/people)
print("oh，god！so crazy! it's:")
print(perdollar)
======================== 
please input totaldollar:  
99.99
how many people?
3
oh，god！so crazy! it's:
28.330499999999997
>>> 
```

#### 4.1.6 简单的逻辑判断

这里需要用到之前关系运算符的知识（2.3数据类型）可以回顾一下。

```python
num=10
print('guess what i think?')
answer=int(input())

result=answer<num
print('too small!')
print(result)

result=answer>num
print('too big')
print(result)

result=num==answer
print('equal!')
print(result)
======================== 
guess what i think?
99
too small!
False
too big
True
equal!
False
>>> 

#看看他们，都是好样的！（误）
#这就是简单的逻辑判断，但是发现了嘛，他们所有的结果一起出来了！
```

