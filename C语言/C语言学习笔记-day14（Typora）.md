## C语言学习笔记-day14

### 结构体套一级指针

```c
#include<stdio.h>
#include<string.h>
#include<stdlib.h>

struct Student
{
    int age;
    char *name;
    int score;
};

int main()
{
    struct Student *p;
    //需要给p分配内存
     p = (struct Student *)malloc(sizeof(struct Student));//如果单纯这么定义 不给一个name指针指向 编译会段错误 
    p ->name= (char*)malloc(strlen("mike")+1);//给name指向 等于定义堆区一个空间 存放name指向
    p->age = 18;
    strcpy(p->name,"mike");
    p->score = 59;
    printf("%d,%s,%d",p->age,p->name,p->score);
    //释放必须先释放name再释放p
    //释放name
    if(p->name!=NULL)
    {
        free(p->name);
        p->name = NULL;
    }
    //释放p
    if(p!=NULL);
    {
        free(p);
        p = NULL;
    }
    
    return 0;
}

```

***

### 共用体

通过前面的讲解，我们知道结构体（Struct）是一种构造类型或复杂类型，它可以包含多个类型不同的成员。在C语言中，还有另外一种和结构体非常类似的语法，叫做**共用体（Union）**，它的定义格式为：

```c
union 共用体名{
    成员列表
};
```

举个例子：

```c
#include<stdio.h>

union Test
{
    unsigned char a;//定义无符号char变量成a
    unsigned short b;
    unsigned int c;//C语言char1个字节 short2个字节 int4个字节
};

int main()
{
    //1.结构体的大小可以简单认为成员大小的累加
    //2.共用体的大小为最大成员的大小
    //3.共用体共用一块内存，所有成员的地址都一样
    union Test obj;
    printf("%p,%p,%p,%p",&obj,&obj.a,&obj.b,&obj.c);//输出结果没有差别 
    //4.当给某个成员赋值，会影响到其他成员
    //左边是高位，右边是低位
    //高位放搞地质，低位放低地址（小端）
    obj.c = 0x44332211;//从右往左输入内存
    printf("obj.c = %x",obj.c);
    printf("obj.b = %x",obj.b);
    printf("obj.a = %x",obj.a);
    //输出obj.c = 44332211
	//	   	 obj.b = 2211
    //         obj.a = 11    
    
    
    return 0;
}
    
```

***

### 枚举使用

在实际编程中，有些数据的取值往往是有限的，只能是非常少量的整数，并且最好为每个值都取一个名字，以方便在后续代码中使用，比如一个星期只有七天，一年只有十二个月，一个班每周有六门课程等。

`#define`命令虽然能解决问题，但也带来了不小的副作用，导致宏名过多，代码松散，看起来总有点不舒服。C语言提供了一种**枚举（Enum）类型**，能够列出所有可能的取值，并给它们取一个名字。

举个例子：

```c
#include<stdio.h>

//#define pink 0
//#define red 1
//#define green 2
//#define white 3
//#define blue 4
//#define yellow 5
//define宏定义很麻烦 容易导致错误
//enmu是关键字
//里面的成员是一个标示符，枚举变量
//第一个成员如果没有赋值，默认为0，下一个成员比上一个多1
//枚举类型
//成员：枚举成员，
enmu color
{
  pink,red,green,white,blue,yellow //从0开始递增数 pink = 0, red =1 以此类推 
};

int main()
{
    int flag = 1;
    if(flag == red)
    {
        printf("red\n");
    }
    //枚举变量flag2
    enmu Color flag2;
    
    //1.可以用枚举成员给flag2赋值
    flag2 = pink;//等价于pink = 0
    
    //2.也可以用常量给flag2赋值，不推荐 这样枚举就失去了本身意义
    flag2 = 3;
}
```

***

### typedef的使用

 typedef给一个已存在的类型起一个别名，typedef不能创建新类型

```c
#include<stdio.h>

//一个常用方法
struct Test
{
    int a;
};

//定义一个和结构体变量
struct struct Test2
{
    int a;
}Test2;

Test2 tmp;//这里定义一个tmp是结构体类型 等于省略一关键词struct 其它用法一致

int main()
{
    //给int起一个别名叫int64
    typedef int int64;//有分号
    
    int64 a;//等价int a; 
    //这个和define宏定义有点像 但是宏定义发生在预处理阶段 typedef是在编译阶段
    
    return 0;
}
```



























