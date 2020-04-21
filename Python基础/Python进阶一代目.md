# Python 进阶学习，一代目版本

> 作者：小杨；yangjuehui06@outlook.com
>
> 分布式学习git: https://github.com/weiyuchens/LearnNotes

## 0.前言

阅读本文档之前，请阅读基础篇

之前讲了很多很多Python最基础的语法，实际上很简单

本来我是准备一直在一个文件里进行迭代，但是目录太长了

而且后面的内容会有变化，所以想了想还是另外开一个文档写

进阶学习方面我尽量多写代码



## 1.如何用文件保存游戏？

之前我们在基础篇玩过一个叫猜数字的小游戏，那我们还是从这个入手

给他新增一个成绩记录的功能



从头开始写吧

首先我们要想好，我们是为了什么开发，想要实现什么功能，需要什么解决方案

ok

那我们现在先需要三个数据

假设是

3 5 31 # 他们分别是 总的游戏次数；最快猜出的论数；猜过的总轮数

ok

欧克，我们现在先创建一个数据为0 0 0的txt文件，作为存档



不分步骤了，看代码注释了

```python
f = open('game.txt') 			#老套路了，先读取
score = f.read().split()
f.close()						#记得close
# 分别存入变量
game_times = int(score[0])
min_times = int(score[1])
total_times = int(score[2])
#计算游戏的平均轮数，注意，由于除数不能有0，所以我们加入一个if来判断

if game_times > 0:
    avg_times = total_times /game_times
else:
    avg_times = 0
#输出成绩信息，%.2f这个格式之前有讲过，表示float数据保留两位小数
print('你已经晚了%d次，最少%d轮猜出答案，平均%.2f轮猜出答案' %(game_times, min_times, avg_times))
#别忘了声明
from random import randint
num = randint(1,100)
print ('please guess what i think?')
bingo = False
while bingo == False:
    answer = int(input())
    if answer<num:
        print('god tooo small!')
    if answer>num:
        print('toooo big wodema!')
    if answer == num:
        print('bingo !')
        bingo = True


```



## 2.如何用文件保存游戏？（2）

现在我们知道如何读取文件中的数据了，现在来kk如何保存结果进去呢

当然，只用加写入功能进去就可以了

```python
from random import randint

f = open('game.txt') 			#老套路了，先读取
score = f.read().split()
f.close()						#记得close
# 分别存入变量
game_times = int(score[0])
min_times = int(score[1])
total_times = int(score[2])
#计算游戏的平均轮数，注意，由于除数不能有0，所以我们加入一个if来判断

if game_times > 0:
    avg_times = total_times /game_times
else:
    avg_times = 0
#输出成绩信息，%.2f这个格式之前有讲过，表示float数据保留两位小数
print('你已经van了%d次，最少%d轮猜出答案，平均%.2f轮猜出答案' %(game_times, min_times, avg_times))


num = randint(1,100)
times = 0
print ('please guess what i think?')
bingo = False
while bingo == False:
    times += 1
    answer = int(input())
    if answer<num:
        print('god tooo small!')
    if answer>num:
        print('toooo big wodema!')
    if answer == num:
        print('bingo !')
        bingo = True
#判断游戏是不是第一次玩
if game_times == 0 or times < min_times: 
    min_times = times
total_times += times
game_times += 1
result = '%d %d %d ' % (game_times, min_times,total_times)
f = open('game.txt','w')
f.write(result)
f.close()

```



## 3.如何用文件保存游戏（3）

现在游戏可以保存成绩啦，但是只能存一组啊！，比如我和我~~女朋友~~ 一起玩，但是她太菜了，我不想和她的成绩记在一起咋办。



所以想办法发搞个新功能，就是存储多组成绩

那我们可以设计，再游戏开始之前，玩家需要输入自己的名字，然后根据不同名字记录不同的成绩。

同样的，就不搞分步骤了，应该很好理解

```python
from random import randint

name = input('请输入你的id:')

f = open('game.txt',encoding='gbk') 			#老套路了，先读取
lines = f.readlines()

f.close()						#记得close
# 分别存入变量
scores = {}						#初始化一个空字典
for l in lines:
    s = l.split()				#把每一行的数据拆分成list
    scores[s[0]] = s[1:]		#第一项数据就是kEY,把他切出来

score = scores.get(name)		#找数据
if score is None:			#如果没找到这个key，就从新新建
    score = [0, 0, 0]

game_times = int(score[0])
min_times = int(score[1])
total_times = int(score[2])
#计算游戏的平均轮数，注意，由于除数不能有0，所以我们加入一个if来判断

if game_times > 0:
    avg_times = total_times /game_times
else:
    avg_times = 0
#输出成绩信息，%.2f这个格式之前有讲过，表示float数据保留两位小数
print('%s,你已经van了%d次，最少%d轮猜出答案，平均%.2f轮猜出答案' %(name,game_times, min_times, avg_times))


num = randint(1,100)
times = 0
print ('please guess what i think?')
bingo = False
while bingo == False:
    times += 1
    answer = int(input())
    if answer<num:
        print('god tooo small!')
    if answer>num:
        print('toooo big wodema!')
    if answer == num:
        print('bingo !')
        bingo = True
#判断游戏是不是第一次玩
if game_times == 0 or times < min_times: 
    min_times = times
total_times += times
game_times += 1

#把成绩更新到对应的玩家数据中
#加傻瓜str转换成字符串，为后面的格式化做准备
scores[name] =[str(game_times),str(min_times),str(total_times)]
result=''

for n in scores:
    #数据按照“name game_times,min_times,total_times”的格式进行转化
    #结尾加上\n换行
    line = n+''+''+''.join(scores[n])+'\n'
    result += line  #加到result中
    
f = open('game.txt','w',encoding='gbk')
f.write(result)
f.close()

```



## 4.函数的默认参数

我们之前好像说过函数的吧，我今天在某神秘网站看到一点进阶内容，就搬过来看看



之前说定义函数的格式应该还记得吧

```python
def hellow(name):	#不要忘记冒号
    print('hellow' +name)
    
hellow('world')
```



但是很多时候，我们都是用world来调用，在少数时候才回去改参数，时候打这么多代码，就有点多，怎么给他改短一点呢：



```python
def hellow(name = 'world'):
    print('hellow'+name)
```

这样是不是简单很多啦！当你没有提供参数的时候，他就会一直使用默认参数，如果你提供了，他就用你的，这样的情况下，就可以更简便的调用：

```python
hellow()
```

直接运行，这样输出的仍然是hellow world

同样，你可以指定参数：

```python
hellow(' python')
>>>
hellowworld
hellow python
>>> 
```



注意事项:

当函数有多个参数的时候，如果你想给部分参数提供默认参数，那么这些参数必须在参数的末尾

栗子：

```python
def func(a,b=5)		#True
def func(a=5,b)		#False
```



## 5.面向对象（1）

说这个之前，先姜维一下，啥叫面向对象编程。

之前我们写的这么多小程序，都是按照功能-需求的顺序设计程序。

**这种就被称为“面向过程编程”**



还有另外一种设计方式，就是把数据和对数据的操作用一种叫“对象（object）”的东西打包起来，这种被称为面向对象开发，更加适合大型的程序开发。

向对象编程最主要的两个概念就是：类（class）和对象（object）

 

类是一种抽象的类型，而对象是这种类型的实例。

 

举个现实的例子：

“笔”作为一个抽象的概念，可以被看成是一个类。而一支实实在在的笔，则是“笔”这种类型的对象。

 

一个类可以有属于它的函数，这种函数被称为类的“方法”。

一个类/对象可以有属于它的变量，这种变量被称作“域”。

域根据所属不同，又分别被称作“类变量”和“实例变量”。

 

继续笔的例子。一个笔有书写的功能，所以“书写”就是笔这个类的一种方法。

每支笔有自己的颜色，“颜色”就是某支笔的域，也是这支笔的实例变量。

 

而关于“类变量”，我们假设有一种限量版钢笔，我们为这种笔创建一种类。而这种笔的“产量”就可以看做这种笔的类变量。因为这个域不属于某一支笔，而是这种类型的笔的共有属性。

 

域和方法被合称为类的属性。


python是一种高度面向对象的语言，它其中的所有东西其实都是对象。所以我们之前也一直在使用着对象。看如下的例子：

```python
s = 'how are you'
#s被赋值后就是一个字符串类型的对象
l = s.split()
#split是字符串的方法，这个方法返回一个list类型的对象
#l是一个list类型的对象
```

 

通过dir()方法可以查看一个类/变量的所有属性：

```python
dir(s)
dir(list)
```

