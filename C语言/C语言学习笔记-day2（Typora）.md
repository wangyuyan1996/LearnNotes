# C语言学习笔记-day2

### 判断语句（重点）

#### 1.if 语句

​	一个 if 语句由一个布尔表达式后跟一个或者多个语句组成

例如：

```c
#include <stdio.h>
int main()
{
    int i = 500;//定义局部变量
   if (i > 3)//使用if语句检查布尔条件
   {
       printf("王建都是大帅比\n");//如果结果是真 执行命令
   }// 程序里的每一个大括号和小括号都必不可少 如果编译错误 首先检查是否输入错误 例如漏掉分号 用 中文打字法输入 "，" 
    return 0;
}
```

​		显然**i**的值大于3，输出结果王建都是大帅比

***

#### 2.if...else语句

​		一个 if 语句 后可跟一个可选的 else 语句，else 语句在布尔表达式为 false 时执行。

例如：

```c
#include<stdio.h>
int main()
{
    int i = 500;//定义局部变量
   if (i >800)//使用if语句检查布尔条件
   {
       printf("王建都是大帅比\n");//如果结果是真 执行命令 但是这里没有满足 所以程序执行else 后方指令
   }
    else{
        printf("王建都是超级大帅比\n");
         }
    return 0;
}
```

输出结果：王建都是超级大帅比

***

#### 3.嵌套if语句

​		在c语言中，嵌套if-else语句是合法的，即能在一个if或if-else语句内使用另一个if或else if 语句。

例如：

```c
#include<stdio.h>
int main()
{
    int i = 500;//定义局部变量
    float x = 10.00;
   if (i ==500)//使用if语句检查布尔条件 注意这里判断必须要用两个= 表示判定
   {  if(x>5)
       {printf("王建都是大帅比\n");//如果结果是真 执行命令 但是这里没有满足 所以程序执行else后方指令
   }
       }
    else{
        printf("王建都是超级大帅比\n");
    }
    return 0;
}
```

 这里的输出结果依然是：王建都是大帅比

这里建议实际操作多更换几次数字和数据类型 体会一下复杂的应用哦

***

#### 4.switch语句

一个 switch 语句允许测试一个变量等于多个值时的情况。

例如：

```c
#include<stdio.h>
int main()
{
    int i = 0;//先定义一个变量i 它的类型被定义为整型
   scanf("%d",&i);//操作人员手动输入一个值，i 等于输入的这个值
   switch(i)//对i的不同的几种状态进行判定
   {
     case(1)://当i = 1 的时候
        printf("hello faker\n");
        break;//break语句跳出当前循环
     case(2)://当i = 2 的时候
        printf("hello doinb\n");
        break;
     case(3):// 当i = 3的时候
        printf("hello uzi");
        break;
   }
    return 0;
}

```

这里根据输入的i值的变化分别确定三个不同的输入结果

***

#### 5.嵌套switch语句

​        在C语言中，switch语句可以在另一个switch语句中间使用，即使内部和外部switch和case包含相同的值，也并不会冲突。

例如：

```c
#include<stdio.h>
int main()
{
    int i = 100;
    int j = 200;
    switch(i)
    {
    case 100:
        printf("i的值是%d\n",i);
        switch(j)
        {
        case 200:
            printf("j的值是%d\n",j);
        }
    }
    return 0;
}

```

这里输出的是：

```
i的值是100
j的值是200
```

***

#### 6.三元运算符

​		三元运算符可以替代if...else语句，它的使用格式如下：

```c
Exp ? Exp2 : Exp3;
```

例如：

```c
#include<stdio.h>
int main()
{
    int num ;
    printf("请输入一个数：");
    scanf("%d",&num);
     (num%2==0)?printf("偶数"):printf("奇数");// 先判断num是否被二整除 如果能够整除 执行 中间程序  显示 “偶数” 如果为否 显示“奇数”
    return 0;
}
```

这是一个判断输入数字是否是偶数的程序

***

### 循环类型

​		在有的程序当中我们可能需要对一些模块反复使用，所以循环环节必不可少，循环的执行顺序是从上到下，依次运行。如果遇到循环的嵌套，则先执行内部循环，再执行外部循环。

#### while循环

​		while后面跟着一个判定条件，如果条件为真，则循环会一直执行下去，如果为稼，则跳出内部的循环。

例如：

```c
#include<stdio.h>
int main()
{
    int num = 10;
    while(num<20)//while判断num的值 当num<20 内部循环进行
    {
        printf("hello world\n");
        num++;// 等于 num = num + 1 num自己不断增加
    }
    return 0;
}

```

这个程序的结果是产生十行“hello world”

---

#### for循环

​		for 循环允许您编写一个执行指定次数的循环控制结构。

例如：

```c
#include<stdio.h>
int main()
{   int i;// 定义一个整型变量i
    for(i=10;i<20;i=i+1)//for循环语句第一个部分 是起始变量大小 中间是执行循环条件 最后条件是变量变化规律 三个之间用;隔开
{
    printf("此时i的值是：%d\n",i);
}
    return 0;
}
```

​		这个程序最终会打印10行，每一行会显示此时i的数字

***

#### do...while循环

​		不像 for 和 while 循环，它们是在循环头部测试循环条件。在 C 语言中，do...while 循环是在循环的尾部检查它的条件。do...while 循环与 while 循环类似，但是 do...while 循环会确保至少执行一次循环。

例如：

```c
#include<stdio.h>
int main()
{   int i = 10;
    do{
        printf("此时i的值为%d\n",i);
        i = i + 1;
    }while(i<20);// do...while形式下的判断条件会在这里给出
    return 0;
}
```

这个程序最终会打印10行，每一行会显示此时i的数字

***

#### 嵌套循环

​		多个循环语句可以在同一个程序中嵌套使用

例如：

```c
#include<stdio.h>
int main()
{   int i = 0;
    int j = 0;
    for(i=0;i<10;i++)
    {
       for(j=0;j<10;j++)
       {
           printf("hello hello\n");
       }
    }
    return 0;
}

```

这里内外循环一共显示10*10次数“hello world”

***

### 循环控制语句

循环语句可以被一些特殊语句打断

|   控制语句   |                             描述                             |
| :----------: | :----------------------------------------------------------: |
|  break语句   | 终止循环或 switch** 语句，程序流将继续执行紧接着循环或 switch 的下一条语句 |
| continue语句 |             告诉循环结构结束本次循环开始下次循环             |
|   goto语句   |           将控制转移到被标记的语句然而并不推鉴使用           |

