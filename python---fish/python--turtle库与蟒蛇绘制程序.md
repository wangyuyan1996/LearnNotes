#1.程序编写目标
【inital-print模板】


1. 初始变量：运算需要的初始值；
2. 运算部分：根据算法实现；
3. 结果输出：print（）输出结果。
#2.turtle库与蟒蛇绘制程序
【def定义函数】
 

1. 函数是一组代码的集合，用于表达一个功能，或者说函数表示一组代码的归属，函数名称是这段代码的名字。
2. def所定义的函数在程序中未经调用不能直接执行，需要通过函数名调用才能够执行。
 
 
【作业】（纪念一下我成功的小蟒蛇吧）

![image](images/1586788676(1).png)

【函数讲解】

【1】turtle.circle（）函数功能

1. 参数rad描述圆形轨迹半径的位置；
2. 参数angle表示小乌龟沿着圆形爬行的弧度值；

【2】turtle.fd()函数功能

1. turtle.fd()函数也可称为turtle.forward（）函数；
2. 表示小乌龟向前直线爬行移动，它有一个参数表示爬行的距离；

#3.函数库的引用
python对库函数引用的方式

1. 第一种方式在程序头部增加：import<库名>

例如：import turtle

     >>>import turtle
     >>>turtle.fd(100)
     
1. 第二种引用方式：

from<库名>import<函数名>

from<库名>import*

例

     >>>from turtle import*
     >>>fd(100)