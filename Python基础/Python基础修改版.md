# 2020.4.14 Python 基础

> 作者邮箱：yangjuehui06@outlook.com
>
> 参考书目：《父与子的编程之旅》《笨方法学Python》
>
> git: https://github.com/weiyuchens/LearnNotes

## 0.更新日志

我决定搞一个更新日志，每天码字完都记录下，因为我都是在同一个文件里迭代 xixi

/**2020.4.14 更新了函数的前三个小节，补全了前面一点描述，哈哈*/ 







<u>基于Python3.6.8</u> 安装和部署环境不再赘述

IDE：<u>idle</u> 为什么不用Pycharm，因为前面用不上

//宇哥说要搞个分布式学习哈，正好俺也想系统的学下Python哈哈，所以就加进了  

//疫情下作为一个湖北人嘛，闲着也是闲着，干脆总结一下写成教程就好了^^

//说不定我儿子到时候能拿来启蒙（没有说各位是我儿子的意思）

//未来的儿子/女儿啊，写代码好累啊，以后千万学个艺术啥的啊[挥泪]

## 0.前言（大佬勿看请跳过）

​	学编程呢，按照我自己的理解哈，其实就是在指挥计算机进行计算，所谓的编程语言的语法、算法实际上都是人为（大佬们）设定的规则，这些规则是帮助一般人（你我）来和计算机进行对话的，计算机只能帮助你计算，帮助你完成复杂的过程，并不能从0直接到1。意思就是说，如果你所做的一切，你都需要先“输入”再经过处理“输出”。

​	学习编程最好你得现有一个宏观的概念，但是你的目标并不能定的太过于遥远，比如说你一开始学着赋值、变量、数据类型就想去写个微信、淘宝，那会非常让人崩溃。但是你可以先从最简单的小项目开始，就会很有趣。

​	比如需求是你想要做一个”猜数字“的游戏，功能是这样的：预先输入一个数字作为你心里的数字，然后让另一个人不停的猜，比如心里数字输入50，如果你输入60，那么程序会回复‘多了！’，如果输入40，那么程序会恢复'少了！'，直到猜到正确的数字为止。这个程序是我入门C时候的第一个程序，当然用Python实现更加简单。

​	我们现在假设这就是你需要独立制作的一个程序啦！我们来分析一下你应该做哪些工作.

```python
#你可以想象，程序其实就是一个盒子，你要设置好盒子里面的机关，然后输入然后通过机关再输出，emm，就像制作饼干的流水线，你得先放面团上去通过咔嚓咔嚓一顿操作，就变成饼干了
#首先，你需要想办法让程序能接受你输入信息对吧，那么你就会用到 input（）啦
#盒子里的内容咋设计呢，就像设置流水线一样要对你给的东西有反应把
#我说1，你说2，这就是编程要学的内容（盒子的内部设计）
#然后就要输出啊，一般来说，我们在IDE里面输出的内容，会在IDE里面直接展示对吧
#这好像和用户拿到手上的游戏还有点距离啊总不能直接发代码给用户把
#然后还要前端啦，设计点好看的界面啥的
#然后还要封装啦，把他变成EXE，这样不就能运行啦

```

所以一开始，学习的所有知识其实都是在为后面的盒子的内部设计做铺垫，学习编程（后端），很多时候说的就是做盒子内部的东西（个人理解，勿盲从），那么就从学好一点点开始吧。



## 1.赋值、输出与输入

### 1.1	赋值



```python
#赋值是基本了，将一个值赋给变量（他没有拒绝的权力），有时候人参就是这样唉
first=1			#这就是把1丢给变量‘first’了
second=2		#这里的‘first’‘second’都是自己命名的变量（按规则）
third=3
print(first+second-third) #print（）就是输出的意思啊啊!!
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

#### 4.1.2 数据变换（初级版）

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

所以怎么才能让他们的内容有条件的显示出来呢



## 5.逻辑判断与循环

### 5.1	if

if就是如果的意思，很明确。他可以让程序来自主判断输入是否满足条件，如果满足，那么执行下一步。反之如果不满足，那就会跳过。

```flow
st=>start: 开始框
cond=>condition: 条件判断框
op=>operation: 处理框
io=>inputoutput: 输出
eden=>end: 结束框
st->cond(yes)->op->io->eden
cond(no)->io
```

```python
if 条件:			#记住 条件后面的冒号:不能少，而且必须是英文符号
    执行语句
    	if 条件：	#如果句内还要套if，那就再缩进
```

​	**及其重要的一点：！！if内部的语句需要一个统一的缩进！！（就是指每行开头的空格，省去了C等语言中的大括号），一般来说 用4个空格和一个TAB，但是请务必记住！！！整个文件请统一选择用tab或者空格，不然又是tab又是空格，很容易莫名其妙的报错！！！**

eg：

```python
# coding: gbk
age=int(input())  #上面那个gbk是中文编码规范，代码里有中文就要注释一下
if age<=18:
    print("you are a adult，你已经是个成年人啦!")
======================== 
17
you are a adult, 你已经是个成年人啦！
>>> 
```

那如果大于18岁也要生成呢？(自己想下)

____fengexian____

现在我们回到4.1.6最后那个小程序（也就是前言那个），hhh现在可以实施了

```python
#	coding:	gbk
num=10
print("你这个小辣鸡能猜到我在想什么嘛！！！")
answer=int(input())
if answer<num:
    print("太小了吧蠢货！")
if answer>num:
    print("我能想这么大的数字吗？？")
if answer==num:
    print("运气而已，呵呵")
```

就这了，但是这个游戏只能玩一次啊喂，每次失败都要重新运行，能不能想个办法让他续上呢 [旺柴]

```python
#题外话一点，相信看到这里，应该算是入点小门了，由于本人最近Ddl严重，时间实在不允许这样写了，后面我就会写的简单些了，有啥不懂的群里直接问E哥哈^^
										#小杨 2：02/04/04
```

### 5.2 while

​	所以 为了解决只能玩一次的尴尬，可以试试while循环。

​	while是一种控制流语句 :kissing_smiling_eyes:

```flow
st=>start: kaishi
io=>inputoutput: shuchu
cond=>condition: tiaojian
op=>operation: xunhuan
e=>end: end

st->io->cond
cond(no)->e
cond(yes)->op->cond 
```

while的英文，翻译过来，就是“当...的时候”

程序执行到while的时候，当ture的时候，就去执行while的内部程序，当false的时候就跳过。

语法和if一样，也需要冒号

举个栗子

```python
#   coding: gbk
a=1
while a !=0:	# 回顾下 ‘！=’表示≠的意思
    print('input！')
    a=int(input())
print('over')

```

所以上个游戏可以改良成循环的了 :smile:

```python
num=10
print('input!')
bingo=False

while bingo==False:
    answer=int(input())

    if answer<num:
        print('small')
    if answer>num:
        print('biggggg')
    if answer==num:
        print('bingoooooo!')
        bingo=True

```

解释下哈，有人问我问题了我很开心T_T

在这个程序中，我们用了一个叫作bingo的变量，用于记录是否猜中了结果，请回顾while循环的初始概念：

> 程序执行到while的时候，当ture的时候，就去执行while的内部程序，当false的时候就跳过。

如果猜中了那就是True，如果没有猜中就是False，没有猜中就会执行循环体中的程序。

在每次循环中，我i们都会输入answer，判断它是大是小是相等，所以在最后一句，bingo=True时候，如果他们相等，那么bingo==False这个循环条件就不成立了，于是程序就结束了。

重点!这里的有双重循环， 所以千万要记得格式 空格！

### 5.3 逻辑判断

插播逻辑判断哈，上一章节 最后的代码里有啥子 False啥子很难懂的东西，这里要讲解下

一个逻辑表达式，其实代表一个bool值

```python
1<3  	#这就是一个bool值，值为True
2==3	#这就是False
```

把它们作为判断条件放在if 或者while的后面，就是根据他们的值来决定要不要执行。

相同的栗子：

```python
a=1
print(a>3) #false
print(a==2-1) #true
b=3
print(a+b==2+2)	#true

```

```python
#很容易混淆的两个概念
a= False
print(a)	#False
print(a==False) #True
```

```python
bingo=False #把bingo设置为一个False值
bingo==False  #判断bingo的值 是不是False，如果是，那么这句话就是True
```

while在判断条件为True的时候要执行循环

∵bingo==False	（看成两个未知数的等式）

∴当比较出来的值 是False的时候，等式成立（为True）

又∵等式为True的时候要执行循环

∴循环。//老千层饼了



### 5.4 random

顾名思义，这就是随机数模块，是python自带的模块。



引入模块的方法：写在开头,然后就可以用randint来生成随机数了

```python
from random import randint
#通用 from 模块名 import 方法名
```

```python
randint(5,10) #代表着5-10之间的随机数 包括5和10
```

还记得我们之前的弱智猜数字游戏吗，直接用随机数代替就好了。

```python
from random import randint
num= randint(1,100)
print('input!')
bingo=False

while bingo==False:
    answer=int(input())

    if answer<num:
        print('small')
    if answer>num:
        print('biggggg')
    if answer==num:
        print('bingoooooo!')
        bingo=True

```





### 5.5 变量的进阶思考

```python
#变量可以用来存储数据
eg:
num=10
answer=input()
#变量可以用来比较大小
answer<num
#变量还可以用来数学运算
a=5
b=a+3
c=a+b
```

注意！:在python中，变量的运算顺序是

1.先算等号右边的

2.再把等号右边的赋值给左边//在计算中，遵循正常的数学运算规律

```python
a=4
a=a+3
print(a)
```

发现了吗，运算出来是7，既然如此，我们就可以用此方法记录我们一共猜了多少次数字！

```python
from random import randint
num= randint(1,100)
print('input!')
bingo=False
count=0

while bingo==False:
    count=count+1	#也可以写成 count+= 1
    answer=int(input())

    if answer<num:
        print('small')
    if answer>num:
        print('biggggg')
    if answer==num:
        print('bingoooooo!')
        bingo=True
print('you have been used the piece of',count)

```

注意，一定要理解这个程序的结构，很重要

所以我们来试试，数学家高斯同学小时候做过的题目，1+2+3+...+100=？

```python
num=1
sum=0
while num<=100:
    sum=sum+num
    num=num+1
print(sum)

#这个程序同样重要！！！！
```



### 5.6 for

这是另外一种循环语句即

```python
for...in...
```



如果用for循环表示从1输出到100：

```python
for num in range(1,101):
    print(num)
```

注意，range（1，101）表示从一开始，到101为止（不包括101，注意这里和 randint 不一样），取其中所有的整数。

**for num range(1, 101)** 就是说，把这些数，依次赋值给变量num。

所以，当你需要一个循环10次的循环，你就只需要写：

```python
for num range(1,11)
#或者for num range(0,10)
#for num range(0,n) 一个循环n次的循环
```

for 循环的本质是对一个序列中的元素进行遍历。什么是序列，以后再说。先记住这个最简单的形式：

```python
for num in range(a,b)
```

就是从 a 循环至 b-1



### 5.7 循环的嵌套

设想一样，如果我们要输出5个SOS for 循环可以这么写：

```python
for num in range(0,5): #一定要记得 冒号，刚才忘记强调了
    print('*')
```

如果想让这5个*在同一行，需要加上 end 参数，使得 print 之后不换行：

```python
for num in range(0, 5):
    print('*', end=' ')
```

 

现在，如果我想要这样一个图形，怎么办？

```python
* * * * *
* * * * *
* * * * *
* * * * *
* * * * *
#或者如果我要这样的怎么办？
*
**
***
****
*****
```

除了你自己动手打好一个多行字符串外，也可以让程序帮我们解决这种问题，我们需要的是两个嵌套在一起的循环：

```python
for num in range(0, 3):
    for num1 in range(0, 3):
        print(num, num1)
#第二个 for 循环在第一个 for 循环的内部，表示每一次外层的循环中，都要进行一整遍内层的循环。

#print 里面用逗号分割，可以连续输出多个不同的值。
>>> 
 RESTART: C:/Users/yangj/AppData/Local/Programs/Python/Python36-32/test/test7.py 
0 0
0 1
0 2
1 0
1 1
1 2
2 0
2 1
2 2
>>> 
#内层循环中的 print 语句一共被执行了 9 次。

#num 从0到2循环了3次。对应于每一个 num 的值，num1 又做了从0到2三次循环。所以3*3一共9次。
```

所以如果要输出一个5*5的方阵图案，我们可以

```python
for num in range(0, 5):
    for num2 in range(0, 5):
        print('*', end=' ')
    print()
```

注意：第二个 print 的缩进和内层的 for 是一样的，这表明它是不是内层 for 循环中的语句，每次 num 的循环中，它只会在内循环执行完之后执行一次。

print 的括号里没有写任何东西，是起到换行的作用，这样，每输出5个*，就会换行。

要输出第二个三角图案时，我们需要根据当前外层循环的序数，设置内层循环应当执行的次数。

```python
for num in range(0, 5):
    for num2 in range(0, num+1):
        print('*', end=' ')
    print()
```

 

内层的j每次从0到 num+1 进行循环。

这样，当第一次 num=0 时，num2 就是 range(0,1)，只输出1个*。

而当最后一次 num=4 时，num2 就是 range(0,5)，输出5个*。



## 6.字符串

### 6.1 字符串基础

字符串就是一组字符的序列（坚定）

字符串 最基础的部分在前面变量那边有写过，这里不赘述了。

总所周知，字符串既可以单引号也可以双引号的

在字符串的内部，如果要使用引号，就可以使用外引号相异的引号

```python
'hellow "fking" world' #这就是内容带有引号的字符串
```

还有一种是 用\来表示引号，可以不受引号限

**\\'** 表示单引号，**\\"** 表示双引号

**\** 被称作**转义字符**，除了用来表示引号，还有比如用

- ***\*\n\** 表示字符串中的换行（相当于按一下回车键的效果）**
- ***\*\t\** 表示字符串中的制表符（相当于按一下tab键的效果）**
- ***\*\\*\* 表示字符串中的 \**\*\*** （因为单个斜杠被用来做转义了，所以真的要表示 \ 字符，就要两个斜杠）

\的用处很多，还有一种是在代码中来换行，而不影响效果：

```python
'this is the \
same line'
#这个字符串和 'this is the same line'是一模一样的,如果有天要写一行很长的代码，就可以用上了
```



### 6.2 字符串格式化

我们在输出字符串的时候，如果想对输出的内容进行一些整理，比如把几段字符拼接起来，或者把一段字符插入到另一段字符中间，就需要用到**字符串的格式化输出**。

如果你想要把三两个字符段连接起来

```python
str1='good'
str2='bye'
str3='baby!'
print(str1+str2+str3)
#或者甚至字符变量和字符串相加
print(str1+str2+'my'+str3)

```

```python
#或者是数字加文字？
num=18
print('my age is '+num)


#hahhahah 这样会报错了哈哈哈
#正确方式是用str（）把数字转换成字符串
print('my age is'+str(num))
```

```python
#另一种方法就是用 % 对字符串进行格式化
num=18
print('my age is %d' %num)

#输出的时候，原始字符串中的 %d 会被 % 后面的值替换。相当于替身玩偶，哈哈
#但是%d 只能用来替换整数。如果你想格式化的数值是小数，要用 %f,如果你想保留两位小数，需要在f前面加上条件：%.2f
print('num is %.2f' % 4.99)
```

```python
#可以用 %s 来替换一段字符串
item='course'
print('this %s is very good!'% item)
```

注意区分：有引号的表示一段字符，没有引号的就是一个变量，这个变量可能是字符，也可能是数字，但一定要和%所表示的格式相一致。



OK. 这时候 我们再试试把之前的沙雕小游戏改造一下

```python
from random import randint
num= randint(1,100)
print('input!')
bingo=False
count=0

while bingo==False:
    count=count+1	#也可以写成 count+= 1
    answer=int(input())

    if answer<num:
        print('%d is so small' % answer)
    if answer>num:
        print('%d is so biggggg' % answer)
    if answer==num:
        print('%d is real bingoooooo!' %answer)
        bingo=True
print('you have been used the piece of',count)

```



### 6.3 字符串格式化2

之前我们说到，可以用%来构造一个字符串，比如

```python
print ('%s is easy to learn' % 'Python')
```

 

有时候，仅仅代入一个值不能满足我们构造字符串的需要。假设你现在有一组学生成绩的数据，你要输出这些数据。在一行中，既要输出学生的姓名，又要输出他的成绩。例如

xiaoyang's score is 87

xiaoli's score is 59



那么在 python中，可以写成

```python
print("%s's score is %d" %('xiaoyang',87))
#or
name= 'xiaoli'
score= 59
print("%s's score is %d" %(name,score))
```

 

无论你有多少个值需要代入字符串中进行格式化，只需要在字符串中的合适位置用对应格式的%表示，然后在后面的括号中按顺序提供代入的值就可以了。占位的%和括号中的值在数量上必须相等，类型也要匹配。

 

**('xiaoyang', 87)** 这种用()表示的一组数据在python中被称为元组（tuple），是python的一种基本数据结构  **important!!!!**

 

这里有点需要留心的就是，括号和引号非常多!!!，一定注意括号该加到哪里。外层print的括号，要包含整个输出内容的语句，包括前面的字符串和后面的变量。内存的括号包含代入的值。如果 print 的括号加的不对，加在了 % 前面，那只能输出前半部分，导致报错了。

### 6.4 数据类型的转换（bool）

回顾第4.1章，数据类型的转换，现在要来 讲一下怎么转换BOOl值：

```python
bool('False')
```

print 一下结果，会发现是 True。

因为在python中，其他类型转成 bool 类型时，以下数值会被认为是False：

- **为0的数字**，包括0，0.0
- **空字符串**，包括''，""
- 表示空值的 **None**
- **空集合**，包括()，[]，{}

其他的值都认为是True。

 

**None** 是 python 中的一个特殊值，表示什么都没有，它和 0、空字符、False、空集合 都不一样。关于集合，我们后面的课程再说。

 

所以，'False' 是一个包含5个字符的字符串，不是空字符，当被转换成bool类型之后，就得到 True。

同样 bool(' ') 的结果是 True，一个空格也不能算作空字符串。

bool('') 才是False。

在 if、while 等条件判断语句里，判断条件会自动进行一次bool的转换。比如

```python
a = '123'
if a:
    print ('this is not a blank string')
```

 

这在编程中是很常见的一种写法。效果等同于

```python
if bool(a) == True:
```

或者

```python
if a != '':
```



## 7.函数

还记得数学上的函数是什么意思嘛，就是给定一个a，就会有唯一输出的一种对应关系F(a)。在Python以及其他编程语言中，函数也是这个意思，但是有部分有略微不同。

编程中所说的函数，就是一堆语句组成的语句块，这个语句块有个名字，你可以在需要时反复地使用这块语句。它**有可能**需要输入，**有可能**会返回输出。

> 举一个现实中的场景：我们去餐厅吃饭，跟服务员点了菜，过了一会儿，服务员把做好的菜端上来。
>
> 1. 餐厅的厨房就可以看作是一个函数
> 2. 我们点的菜单，就是给这个函数的参数（对函数来说就是输入）
> 3. 厨师在厨房里做菜的过程就是这个函数的执行过程
> 4. 做好的菜是返回结果，返回到我们的餐桌上（函数的返回值）

我们之前用的input和range就是python中的函数

打个比方，range()这是一个函数，range(1,10)中的1和10就是你输入的参数，而生成的结果就是这个函数的返回结果。

> 我发现我之前并没有很好的解释range函数，现在插播一下
>
> 1.它表示的是左闭右开区间
>
> 2.它接收的参数必须是整数，可以是负数，但不能是浮点数等其它类型；
>
> 3.它是不可变的序列类型，可以进行判断元素、查找元素、切片等操作，但不能修改元素；
>
> 4.它是可迭代对象，却不是迭代器  #这条可以不用理解，难解释

这里相当于range()就是厨房，1和10就是你点的菜，出来的结果就是返回到你桌上的菜

```Python
for num in range (1,10):
    print(num)
1
2
3
4
5
6
7
8
9
>>> 
```

除了python自带的函数以外，我们还可以自己定义函数，python定义一个函数的关键词是def，即define的缩写。

```python
def goodbye():
    print ("please donnot leave me！")
```

这时候就相当于你定义了一个名字叫goodbye的函数，后面的括号是需要输入的参数，而这里定义的时候并没有填写，是表示不需要参数。下面缩进的代码块就是函数的内容，也叫他函数体。

然后这时候我们去调用它：

```python
def goodbye():
    print ("please donnot leave me！")

goodbye()

 
please donnot leave me！
>>> 

```

### 7.1 函数的参数

​	在第7章里，我们讲了怎样定义一个自己的函数，但我们没有给他提供输入**参数**的功能。不能指定参数的函数就好比你去餐厅吃饭，服务员告诉你，不能点菜，有啥吃啥。这显然不能满足很多情况。

 所以，如果我们希望自己定义的函数里允许调用者提供一些参数，就把这些参数写在括号里，如果有多个参数，用逗号隔开，如：

```python
def cheat(victim):
   print(victim + ', please donnot leave me！')

```

或者

```python
def plus(num1, num2):
   print(num1+num2)
```



```python
#请注意!,在第一个例子里，victim是一个变量，他并不是字符串，例子如下：

def cheat(victim):
   print(victim + ', please donnot leave me！')

cheat("xiaoyang")

#也就是说，这里的victim，是要求你输入一个名字！，而不是让你傻傻的输入 victim 初学的时候我踩过的坑TVT
```



### 7.2 函数应用细节

我发现我上一段写的不怎么好，所以我准备举个例子讲讲：

还记得我们之前的 那个弱鸡小游戏嘛，hahah，拿来废物利用下

我希望我自己能定义一个函数，然后判断输入数值的大小

```python
def contrast(num1,num2):
    if num1<num2:
        print('num1 is too small!')
        return False
    if num1>num2:
        print('num1 is too big！')
        return False
    if num1==num2:
        print('bingo!')
        return True
contrast(8798692659,84092774534)

```

这里说一下，**return** 是函数的结束语句，return 后面的值被作为这个函数的**返回值**。函数中任何地方的 return 被执行到的时候，这个函数就会立刻结束并跳出。

注意：函数的 **返回值** 和我们前面说的 输出 是两回事。print 输出是将结果显示在控制台中，最终一定是转成字符类型；而 返回值，是将结果返回到调用函数的地方，可以是任何类型。

那我们把那个沙雕游戏拿出来溜溜吧：

```python
def contrast(num1,num2):
    if num1<num2:
        print('is too small!')
        return False
    if num1>num2:
        print('is too big！')
        return False
    if num1==num2:
        print('bingo!')
        return True

from random import randint
num=randint(1,100)
print('Guess what i think?')
bingo=False
while bingo==False:   #这里就是 ，当bingo的值是False的时候，就会一直循环，反之则输出
    answer = int(input())
    bingo = contrast(answer,num)
```

当然，函数只要定义了。是可以重复使用滴！



### 7.3 循环的进阶应用

我之前，不太想写，一是因为那天懒病发作，二是因为确实内容太多估计记不住，今天就拿着一起讲哈

可以回顾下，5.1那章节，除了我们讲过的用法，他还可以配合elif和else来使用

if，如果条件满足，就做xxx，否则就不做。

else就是“否则”，就xxx

```flow
st=>start: 开始框
cond=>condition: if
op1=>operation: 处理程序1号
op2=>operation: 处理程序2号
io=>inputoutput: 输出
eden=>end: 结束框
st->cond
cond(true)->op1->io
cond(false)-else->op2->io
```

当if后面的条件语句不满足时，与之相对应的 else 中的代码块将被执行。

```python
if a == 1:
   print('right')
else:
   print('wrong')
```

 elif 意为 else if，含义就是：“否则如果”条件满足，就做yyy。elif 后面需要有一个逻辑判断语句。

```flow
st=>start: 开始框
cond=>condition: if
cond2=>condition: elif
op1=>operation: 处理程序1号
op2=>operation: 处理程序2号
io=>inputoutput: 输出
ed=>end: 结束框
st->cond
cond(true)->op1->io
cond(false)->cond2(true)->op2->io
cond2(false)->io
```

当if条件不满足时，再去判断 elif 的条件，如果满足则执行其中的代码块：

```python
if a == 1:
   print ('one')
elif a == 2:
   print ('two')
```

 

if, elif, else 可组成一个整体的条件语句。

1. if 是**必须有**的；
2. elif **可以没有，也可以有很多个**，每个elif条件不满足时会进入下一个elif判断；一旦满足，执行完就结束整个条件语句；
3. else **可以没有，如果有的话只能有一个**，**必须在条件语句的最后。**

```python
if a ==1:
   print('one')
elif a==2:
   print('two')
elif a == 3:
   print ('three')
else:
   print ('too many')
```

我们昨天刚改写的小游戏中的函数contrast，用了三个条件判断，我们可以再改写成一个包含 if...elif...else 的结构：

```python
def contrast(num1, num2):
   if num1<num2:			
       print ('too small')	#如果满足，那么输入too small，并且返回False值
       return False;
   elif num1>num2:			#如果if不满足，那么来判断这里
       print ('too big')	#如果满足，则输出too big，并且返回False
       return False;
   else:					#如果上面这两个都不满足，那么输出bingo，返回True值
       print ('bingo')
       return True

from random import randint
num=randint(1,100)
print('Guess what i think?')
bingo=False
while bingo==False:   #这里就是 ，当bingo的值是False的时候，就会一直循环，反之则输出
    answer = int(input())
    bingo = contrast(answer,num)
```

