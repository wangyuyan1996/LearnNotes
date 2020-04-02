# 2020.4.1 Python 基础

<u>基于Python3.6.8</u>

<u>idle</u>

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



### 2.2	数据类型

```python
a=10		#int 			整数
a=1.3		#float			浮点数
a=Ture		#Ture/False		真值
a='hello'	#字符串（可以用双引号）			
```

### 2.3	第一个程序进化版

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

