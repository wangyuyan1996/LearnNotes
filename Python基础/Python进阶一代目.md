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

