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

**python是一种高度面向对象的语言**，它其中的所有东西其实都是对象。所以我们之前也一直在使用着对象。看如下的例子：

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



## 6.面向对象（2）

我知道上一章听起来很痛苦，我一开始也非常痛苦，等我先写完后面的具体例子，然后会把上面几章节细化一下的。



先来试试创建一个类：

```python
class MyClass:	#记得冒号
    pass

mc = MyClass()
print(mc)
```

关键词是class，然后加上类的名称，创建了一下叫MyClass的类。

后面缩进的pass是这个类的内部内容，pass表示的是这个内部是空的。

类名加上圆括号的形式可以创建一个关于这个类的实例，也就是所谓的被称之为‘对象’的东西。

我们可以把这个对象赋值给变量mc。

所以，现在变量mc就是一个名叫MyClass的类的对象。

来看看输出结果：

```python
>>> 
 RESTART: C:/Users/yangj/AppData/Local/Programs/Python/Python36-32/test/test.py 
<__main__.MyClass object at 0x03C842D0>
>>> 
```

这里就可以解释一下了

mc是__ main __这个模块中MyClass这个类的一个实例

也就是这个英文的字面意思(object)，后面的这个16进制代码是说这个对象在内存中的内存地址。



现在我们给这个类加上一点“域”

```python
class MyClass:	#记得冒号
    name = 'ash'

    def sayhellow(self):
        print ('hellow %s' % self.name)
        
mc = MyClass()
print(mc.name)
mc.name = 'lily'
mc.sayhellow()

```



运行一下，看看结果：

```python
>>> 
 RESTART: C:/Users/yangj/AppData/Local/Programs/Python/Python36-32/test/test.py 
ash
hellow lily
>>> 
```



在这里，我给MyClass这个类增加了一个变量name，并且把它的值设定为了’ash‘

然后定义了一个新方法 sayhellow

下面这个mc.name是调用类变量的方法，

也就是说，调用一个类的方法就是“对象.变量名”。

这样你就可以获得他的值，当然也就可以改变它的值



但是要注意到，类方法和之前说到的定义函数是有区别的，他们的区别在于，类方法的第一个参数必须为self，并且通过 对象.方法名（）的方式进行调用。

**但是并不需要额外提供self这个参数的值！！！**

self在这个类方法中的值，就是你调用的这个对象本身额



## 7.面向对象（3）-具象理解

是不是还是看不懂，没关系，你一次性肯定是看不懂的，我也看不懂，这很正常。

面向对象本身就是复杂抽象的概念，我们可以先不管对象和类的抽象概念，试着从代码中去理解



在刚开始编程的时候，从上到下一行行执行的简单程序容易被理解，即使加上if、while、for之类的语句以及函数调用，也还是不算困难。有了面向对象之后，程序的执行路径就变得复杂，很容易让人混乱。不过当你熟悉之后会发现，面向对象是比面向过程更合理的程序设计方式。



这里举个例子



我现在有一辆小汽车

已知武汉到宜昌有100km（误）

想要算出开着汽车60kmh的速度（大误），从武汉到宜昌要多久。

面向过程的方法：

```python
speed = 60.0
distance = 100.0
time = distance/ speed
print (time)
```



面向对象的方法：

```python
class Car:
    speed = 0
    def drive(self,distance):
        time = distance /self.speed
        print(time)
        
car = Car()
car.speed = 60.0
car.drive(100.0)

>>> 
 RESTART: C:/Users/yangj/AppData/Local/Programs/Python/Python36-32/test/test.py 
1.6666666666666667
>>> 
```



当然，看上去，似乎面向过程的工作量似乎更小？

实际上，如果我们让题目变得更加复杂

如我我有一辆兰博基尼（大雾），他的速度是150kmh

然后到了武汉，我还想去长沙。

那么我想知道，这两种车在这两段路上需要多长时间

面向过程：

```python
speed1 = 60.0
distance1 = 100.0
time1 = distance1 / speed1
print (time1)

distance2 = 200.0
time2 = distance2 / speed1
print (time2)

speed2 = 150.0
time3 = distance1 / speed2
print (time3)

time4 = distance2 / speed2
print (time4)

>>> 
 RESTART: C:/Users/yangj/AppData/Local/Programs/Python/Python36-32/test/test.py 
1.6666666666666667
3.3333333333333335
0.6666666666666666
1.3333333333333333
>>> 
```



面向对象：

```python
class Car:
    speed = 0
    def drive(self,distance):
        time = distance/self.speed
        print(time)

car1 = Car()
car1.speed = 60.0
car1.drive(100.0)
car1.drive(200.0)

car2 = Car()
car2.speed = 150.0
car2.drive(100.0)
car2.drive(200.0)

>>> 
 RESTART: C:/Users/yangj/AppData/Local/Programs/Python/Python36-32/test/test.py 
1.6666666666666667
3.3333333333333335
0.6666666666666666
1.3333333333333333
>>> 
```



对比两种方法，面向过程把数据和处理数据的计算全部放在一起，当功能复杂之后，就会显得很混乱，且容易产生很多重复的代码。而面向对象，把一类数据和处理这类数据的方法封装在一个类中，让程序的结构更清晰，不同的功能之间相互独立。这样更有利于进行模块化的开发方式。

 

当然，面向对象实在是太复杂了

这个例子相当的粗浅，他和之前的循环，变量不一样，没有那么直观，但是记住不要对他产生恐惧！加油！





## 8.面向对象（4）-继承

好像，上面那个并不能很好的展现面向对象的魅力啊（误）



加点难度吧

仍然是宜昌到武汉，但是这次除了奔驰兰博，我又给自己new了一辆自行车！（厉害吧）

自行车和汽车有着相同的属性：速度（speed）。还有一个相同的方法（drive），来输出行驶/骑行一段距离所花的时间。但这次我们要给汽车增加一个属性：每公里油耗（fuel）。而在汽车行驶一段距离的方法中，除了要输出所花的时间外，还要输出所需的油量。



这个用面向过程的思路，可能很要掉电头发hehae。

你可能需要写两个函数，然后把数据作为参数传递进去，在调用的时候要搞清应该使用哪个函数和哪些数据。

面向过程的方法，你可能需要写两个函数，然后把数据作为参数传递进去，在调用的时候要搞清应该使用哪个函数和哪些数据。有了面向对象，你可以把相关的数据和方法封装在一起，并且可以把不同类中的相同功能整合起来。这就需要用到面向对象中的另一个重要概念：**继承。**

 

我们要使用的方法是，创建一个叫做Vehicle的类，表示某种车，它包含了汽车和自行车所共有的东西：速度，行驶的方法。然后让Car类和Bike类都继承这个Vehicle类，即作为它的子类。在每个子类中，可以分别添加各自独有的属性。

**Vehicle类被称为基本类或超类，Car类和Bike类被成为导出类或子类。**



```python
class Vehicle:
    def __init__(self,speed):		
        self.speed=speed

    def drive(self,distance):
        print('need %f hour(s)' %(distance / self.speed))

class Bike(Vehicle):
    pass

class Car(Vehicle):
    def __init__(self,speed,fuel):
        Vehicle.__init__(self,speed)
        self.fuel = fuel


    def drive(self,distance):
        Vehicle.drive(self,distance)
        print('need %f fuels' %(distance / self.speed))


b = Bike(15.0)
c = Car(80.0,0.012)
b.drive(100.0)
c.drive(100.0)

```



来解释一下代码哈，

```python
#用代码块写，是因为有很多语法和md冲突了
__init__ 这个函数在类被创建的时候自动调用，用来初始化类。它的参数，要在创建类的时候提供。于是我们通过提供一个数值来初始化speed的值。

注意：__init__是python的内置方法，类似的函数名前后是两个下英文划线，如果写错了，则不会起到原本应有的作用。

#class定义后面的括号里表示这个类继承于哪个类。Bike(Vehicle)就是说Bike是继承自Vehicle中的子类。Vehicle中的属性和方法，Bike都会有。因为Bike不需要有额外的功能，所以用pass在类中保留空块，什么都不用写。

#Car类中，我们又重新定义了__init__和drive函数，这样会覆盖掉它继承自Vehicle的同名函数。但我们依然可以通过“Vehicle.函数名”来调用它的超类方法。以此来获得它作为Vehicle所具有的功能。注意，因为是通过类名调用方法，而不是像之前一样通过对象来调用，所以这里必须提供self的参数值。在调用超类的方法之后，我们又给Car增加了一个fuel属性，并且在drive中多输出一行信息。

 
```

最后，我们分别创建一个速度为15的自行车对象，和一个速度为80、耗油量为0.012的汽车，然后让它们去行驶100的距离。





放上结果：

```python
>>> 
 RESTART: C:/Users/yangj/AppData/Local/Programs/Python/Python36-32/test/test.py 
need 6.666667 hour(s)
need 1.250000 hour(s)
need 1.250000 fuels
>>> 
```





有没有点感觉了？

我的理解哈

> 面向对象就像是，设计一个角色模型
>
> 比如说，我要设计一个角色 叫ash，那么在Python中，这个类名字就叫ash
>
> 然后我要设计他的各种属性
>
> 比如三维 173 、145、18（×）
>
> 然后后面就可以直接在程序中很便捷的直接使用ash这个角色，包括了他的各项数据
>
> 面向过程和面向对象哪个好用，是根据复杂度来的
>
> 比如说，如果你要拿ash和Eden来比较长度（误）
>
> 那就直接面向过程，对比两个数据
>
> 那如果你要计算ash和Eden两个角色根据各个方面进行综合pk
>
> pk结果要根据各种数据包括体力，身高，体重，力量多数据综合比对
>
> 那这个时候面向过程就会特别繁琐
>
> 因为你需要定义 ash的体力、eden的体力、ash的身高...各种变量，工作量非常大
>
> 但是如果是面向对象，那就会简单很多，你只需要定义 身高，体重，体力这样的数据
>
> 就像游戏中的各种属性，不同的角色都在用
>
> 这样的情况下，很明显，面向对象更加简单