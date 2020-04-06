## C语言学习笔记-day5

### 万能指针

​        在定义指针的时候我们有一种很独特的定义法，定义一种万能指针，即void * 法。void *指针可以指向任意类型（前提是定义合法），但是在使用指针所指向的内存时，最好转换为它本身的指针类型。

例如：

```c
#include<stdio.h>
int main()
{ 
    void *p = NULL;
   int a = 10;
    p = &a;//指针保存的都是变量首地址哦
    
    *((int*)p) = 222;//在p前增加（int*）强制将p转化int*类型 否则编译器不认识 无法确定步长
    printf("*p = %d\n",*((int*)p));
    return 0；
}
```

这个程序在我这里输出结果：

```
*p = 222
```

***

### 指针步长

```c
#include<stdio.h>
int main()
{
    int a;
    int *p = &a;
    
    printf("p: %d, p+1: %d\n",p,p+1);
    
    char b;
    char *q = &b;
    printf("q: %d, q + 1: %d\n", q,q+1);
    
    return 0;
}
```

运行结果：

```c
p: 6356724, p+1: 6356728
q: 6356723, q + 1: 6356724
```

这个例子告诉我们：1.指针的加减法和我们常规认识的加减法含义不同；

​								   2.加减的数字取决于指针所指向的数据类型      int 定义参数存储为四字节 所以指针加一的时候，地址会加四，char定义参数存储为一字节，所以指针加一时候，地址将会加一

***

### const定义指针

在前面我们也学习过前缀const 定义过的变量，那个变量被定义就不可修改，在指针这里，也是类似的，

例如：

```c
include<stdio.h>
int main()
{//我们反复强调必须明确两个概念，第一个是指针变量，第二个是指针所指向的空间
    
    int a = 10;
    int * p1 = &a;
    *p1 = 100;//等价于操作a，*p1操作指针所指向的空间
    p1 = NULL;//操作指针变量
    
    //const修饰*，代表指针所指向的內存是只读
    const int*p2 = &a;
    //*p2 = 100;//err
    p2 = NULL;//ok
    
    //const修饰* 代表指针所指向的内存是只读
    int const  *p3 = &a;
    //*p3 = 100;err
    p3 = NULL;
    
    //const修饰指针变量，代表指针变量的值为只读
    int * const p4 = &a;
    *p4 = 100;// ok
    //p4 = NULL;//err
    
    //const修饰所有 只能读取 不可修改
    const int *const p4 = &a;
    *p4 = 100;//err
    p4 = NELL;//err
    
    //建议反复阅读
    
    
}
```

***

### 指针和数组

```c
#include<stdio.h>
int main()
{
    int a[10];
    //1.数组名是数组首元素地址
    printf("a = %p, &a[0] = %p\n",a, &a[0]);
    
    //2.数组名是常量，不允许修改，有点类似int *const p;

    return 0;
}
```

在我计算机上运行：

```
a = 0060FED8, &a[0] = 0060FED8
```

有一说一，确实数组名是数组首元素地址。

```c
#include<stdio.h>
int main()
{
    int a[10] = {1,2,3,4,5,6,7,8,9,10};
  	
    int *p = NULL;
    //p指针变量指向首个元素
    p = &a[0];
    p = a ;
    int i = 0;
    for(i=0;i<10;i++){
        printf("%d",*(p+i));// p[i]等价于*(p+1)操作都是指针所指向的内存
    }
    return 0;
}


```

打印结果是遍历a[10]中所有元素了，除此之外还有方法

```c
#include<stdio.h>
int main()
{
    int a[10] = {1,2,3,4,5,6,7,8,9,10};
    
    int *p = a;
    p = &a[0];
    int n = sizeof(a)/sizeof(*a);
    int  i = 0;
    
    for(i = 0; i < n; i++)//指针自增从而实现
    {
        printf("%d,",*p);
        p++;
    }
    printf("\n");
    
    //定义一个指针，指向尾元素
    int *q = &a[n-1];
    q = a+n-1;
    
    for(i = 0;i<n;i++)//指针自减从而实现
    {
        printf("%d,",*q);
        q--;
    }
    
    return 0;
}
```

***

### 指针数组

指针数组，首先它是一个数组，每个元素都是指针。

```c
#include<stdio.h>
int main()
{
    int a[3] = {0,1,2};
    //指针数组，它是一个数组，每个元素都是指针
    //方法1
    int *p[3];
    p[0] = &a[0];
    p[0] = a;
    
    p[1] = &a[1];
    p[1] = &a+1;
    
    p[2] = &a[2];
    p[2] = a+2;
    //方法2
     int n = sizeof(p)/sizeof(p[0]);
    int i = 0;
    for(i=0;i<n;i++)
    {
        p[i] = &a[i];
    }
    //打印内容
    for(i = 0;i<n;i++)
    {
        printf("%d\n",*p[i]);
    }
        return 0;
    
}
```























































