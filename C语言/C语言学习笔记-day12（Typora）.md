## C语言学习笔记-day12

### 结构体数组

结构体中也有数组，称为结构体数组。它与前面讲的数值型数组几乎是一模一样的，只不过需要注意的是，结构体数组的每一个元素都是一个结构体类型的变量，都包含结构体中所有的成员项。

```c
#include<stdio.h>
#include<string.h>

struct Student
{
    int age;
    char name[50];
    int score;
};

int main()
{
    struct Student s;
    
    struct Student a[5];//结构体数组 有五个变量啊
    //操作元素
    a[0].age = 18;
    strcpy(a[0].name,"mike");
    a[0].score = 59;
    //操作某个元素地址
    (a+1)->age = 19;
    strcpy((a+1)->name,"jiang");
    (a+1)->score = 60;
    
    (*(a+2)).age = 20;
    strcpy((*(a+2)).name,"jie");
    (*(a+2)).score = 61;
    
    struct Student *p = a;
    p = &a[0];
    
    p[3].age = 21;
    strcpy(p[3].name,"zed");
    p[3].score = 62;
    
    (p+4)->age = 22;
    strcpy((p+4))->name,"ali";
    (p+4)->score = 63;
    
    
    int i = 0;//结构体数组的引用与引用一个结构体变量在原理上是一样的。只不过结构体数组中有多个结构体变量，我们只需利用 for 循 环一个一个地使用结构体数组中的元素。
    int n = sizeof(a)/sizeof(a[0]);
    for(i=0;i<nli++)
    {
        printf("%d,%s,%d",a[i].age,a[i].name,a[i].score);
    }
    
    return 0;
}
```

定义的时候初始化：

```c
struct Student
{
    int age;
    char name[50];
    int score;
};

int main()
{
    struct Student a[5] = 
    {
        {18,"faker",59},
        {19,"the_shy",60},
        {20,"lwx",61},
        {21,"mata",62},
        {22,"uzi",63}
    };
   
   return 0;
}
```

***

### 结构体嵌套

```c
#include<stdio.h>
#include<string.h>

struct Info
{
	int age;
    char name[50];
};

struct Student
{
    struct Info info;
    int score;
};

int main()
{
    struct Student s;
    s.info.age = 18;//记住这个用法非常关键
    strcpy((s.info.name),"mike");
    s.score = 100;
    
    struct Student *p =&s;
    p->info.age = 18;//记住这个用法非常关键
    strcpy((p->info.name),"mike");
    p->score = 100;
    
    //初始化
    struct Student tmp= {18,"mike",59};
    
    return 0;
}
```

###  结构体值传递和地址传递的区别

这个和之前指针那一块有点类似，话不多说，直接上代码：

```c
#include<stdio.h>
#include<string.h>

struct Student
{
    int age;
    char name[50];
    int score;
};

void  setStu(struct Student tmp)//当setStu调用完毕，tmp释放
{
    tmp.age = 22 ;
    strcpy(tmp.name,"jiang");
    tmp.score = 77;
    printf("setStu %d,%s,%d\n",tmp.age,tmp.name,tmp.score);
}

int main()
{
    struct Student s1 = {18,"mike",59};
    
    setStu(s1);
    printf(" %d,%s,%d\n",s1.age,s1.name,s1.score);
    
    return 0;
}
```

这个程序输出结果：

```c
setStu 22,jiang,77
 18,mike,59
```

这个道理和我们之前提到类似，因为局部变量tmp在使用完毕就释放掉，无论怎么修改也不会改变主函数的值，所以要想修改，必须采用地址传递

```c
#include<stdio.h>
#include<string.h>

struct Student
{
    int age;
    char name[50];
    int score;
};

void fun2(struct Student *p)
{
    printf("%d,%s,%d",p->age,p->name,p->score);
}

int main()
{
    struct Student s1 ={18,"mike",59};
    fun2(&s1);
    
    return 0;
}

```

输出结果：

```c
18,mike,59
```

仔细体会一下，和之前提到的有很大的相似，反复阅读，深刻体会。

***

### 指针指向栈区空间

指向栈区空间就是指向临时变量

```c
#include<stdio.h>
#include<string.h>

struct Student
{
    int age;
    char name[50];
    int score;
};

int main()
{
    //定义一个结构体类型的指针
    struct Student tmp;
    struct Student *p;
    //指针指向栈区空间
    p = &tmp；
    
    p->age = 18;
    strcpy(p->name,"mike");
    p->score = 59;
    printf("%d,%s,%d\n",p->age,p->name,p->score);
    
    return 0;
}
```

***

###  指针指向堆区空间

```c
#include<stdio.h>
#include<string.h>
#include<stdlib.h>

struct Student
{
    int age;
    char name[50];
    int score;
};

int main()
{
//定义一个结构体类型的指针
struct Student *p;
//指针指向堆区空间
p = (struct Student*)malloc(sizeof(struct Student));
 p->age = 18;
    strcpy(p->name,"mike");
    p->score = 59;
 	 printf("%d,%s,%d\n",p->age,p->name,p->score);
    
    if (p!= NULL)
    {
        free(p);
        p = NULL;
    }
    
    return 0;
}
```

