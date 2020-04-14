## C语言学习笔记-day11

### 指针指向栈区空间

话不多说，直接上程序：

```c
#include<stdio.h>
int main()
{
    int *p;
    int a;//定义一个栈区变量  普通局部变量定义完毕全部保存在栈区 我们之前提到过的
    p = &a;//指针指向栈区空间
    
    *p = 10;
    printf("*p = %d\n",*p);
    
    return 0;
}
```

打印内容：

```c
*p = 10
```

***

### 指针指向堆区空间

这里需要一个malloc函数，保存在头文件<stdlib.h>之中 我们需要注意：

1.动态分配的空间，如果程序没有结束，不会自动释放

2.一般使用完，需要人为释放free(p)

3.free(p);不是释放p变量，释放p所指向的内存

4.同一块堆区内存只能释放一次

5.所谓的释放不是指内存消失，指这块内存用户不能再使用了，系统回收了，如果用户再用，就是操作非法内存

```c
//参数是指定堆区分配多大的空间
//返回值：成功就是堆区空间首元素地址
//失败返回NULL
malloc(sizeof(int));
```

例如：



```c
#include<stdio.h>
#include<stdlib.h>


int main()
{
    int *p = NULL;
    
    p = (int *)malloc(sizeof(int));//在堆区申请一块内存
    if(p == NULL)
    {
        printf("分配失败\n");
        return -1;//如果失败就提前结束程序了
    }
    
    *p = 10;
    printf("*p = %d\n",*p);
    
    if(NULL != p)
    {
        free(p);
        p = NULL;
    }
    
    return 0;
}
```

这样一来程序就可以运行啦

我们来聊一个很有意思的问题--堆区空间越界：

```c
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
int main()
{
    char *p = NULL;
    
    p = (char*)malloc(0);
    if(p == NULL)
    {
        printf("分配失败\n");
        return 0;
    }
    
    strcpy(p,"mikejiang");
    printf("%s\n",p);
    
    free(p);
    
    return 0;
}
```

按道理来说，这个程序是编译不通过的，但是很多编译器检测不了这个错误，还会继续运行，至于错误原因，我们慢慢分析：

```c
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
int main()
{
    char *p = NULL;
    
    p = (char*)malloc(0);//给p变量分配内存0；按道理是无法运行的，但是检测不了
    if(p == NULL)
    {
        printf("分配失败\n");
        return 0;
    }
    
    strcpy(p,"mikejiang");//复制字符，居然可以正常显示
    printf("%s\n",p);
    
    free(p);
    
    return 0;
}
```

这就涉及一个堆区空间越界，即使用空间大于分配，在有些奇特的情况，系统检测不了，但是随着程序运行会产生一些不可控bug，难以消除，令人头痛。

***

### 结构体

有时候我们需要将几个数据结合成一个有机的整体，显然单独定义变量比较繁琐，数据不便于管理；

C语言中给出了另一种构造数据类型------结构体。

```c
int num;
char name[20];
char sex;
int age;
int char addr[30];
学生信息的一般表达法
struct stu
{
    int num;
char name[20];
char sex;
int age;
int char addr[30];
}student;
学生信息的结构体表示法
```



```c
#include<stdio.h>
#include<string.h>
//1.struct 是关键字
//2.struct Student合起来才是结构体类型
//3.结构体内部定义的变量不能直接赋值
//4.结构体只是一个类型，没有定义变量前，是没有分配空间，没有空间，就不能赋值

struct Student
{
	int age;
    char name[50];
    int score;
};//有分号

int main()
{
    //定义结构体变量
    //1.类型名 变量名
    struct Student stu;//别忘了struct关键字
    //结构体变量初始化，和数组一样，要使用大括号
    //只有在定义时才能初始化
    struct Student stu2 {18,"mike",59};
    
    //使用结构体成员，不能直接使用，需要借助结构体变量来引用
    struct Student tmp;
    //如果是普通变量，使用.运算符
    tmp.age = 18;
    strcpy(tmp.name,"mike");//name成员是数组名，数组名是常量，不能修改
    tmp.score = 59;
    
    //如果是指针变量，使用->
    //如果是指针，指针有合法指向，才能操作结构体成员
    struct Student *p;
    p = &tmp;
    p->age = 18;
    strcpy(p->name,"mike");
    p->score = 59;
    
    //任何结构体变量都以用.或->操作成员
    (&tmp)->age = 18;
    
    (*p).age = 18;
    
    
    
    
    return 0;
}
```















