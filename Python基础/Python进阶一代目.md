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





