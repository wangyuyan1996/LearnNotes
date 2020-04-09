### C语言学习笔记-day7

### 返回局部变量的地址

在我们编辑一些函数的时候，可能会因为一些地址的处理不当而导致段错误，下面是个例子;

(关于段错误的例子可以参考前面笔记)

```c
#include<stdio.h>
int *fun()
{
    int a;
    
    return &a;//返回局部变量地址 在一些编辑器里面例如 linux 64位 gcc 不允许返回局部变量的地址
}


int main()
{
    int *p = NULL;
    
    p = fun();//接受函数返回的地址
    *p = 100;//操作指针所指向的内存 当fun()函数执行完毕，fun()内部的a，自动释放 也就是说此时fun()之中所有参数地址都找不到 此时的p指针变成了一个不知道指向何处的野指针 所以*p这个操作编译器执行不了
    
    return 0;
    
}
```

----

### 返回全局变量的地址

```c
#include<stdio.h>
//1.在{}外面定义的变量，就是全局变量，全局变量在任何地方都可以使用
//2.全局变量只有在整个程序结束后，才释放
int a;
int *fun()
{
    return &a;//fun()调用完毕，a不释放
}
int main()
{
    int *p = NULL;
    p = fun();
    
    *p = 100;
    printf("*p = %d\n",*p);//第2种写法：printf("a= %d\n",a);
    //第3种写法：printf("a = %d\n",*(fun())); 
    return 0;
}
```

此时输出：

```c
*p = 100
```

***

### 字符串打印说明

关于字符串的打印原理，下面这个程序我给出解释，其实也和指针密不可分：

```c
#include<stdio.h>
int main()
{	
    char str[] = "hello faker";
    //1.%s，从首元素开始打印，直到结束符为止
    //2.%s，操作的是指针所指向的内容
    printf("str = %s\n",str);//%s在C语言中代表字符串类型格式符 经过前面学习 我们已经知道这样可以打印字符串了 它的原理是什么样的 如下：
    // str 是首元素地址 但是数组非常特别 在打印数组时不需要写*str 因为*str代表第0个元素 在这里是char
    int i = 0;
    
    //打印字符串的实现
    while(str[i]!='\0')//等价 while(*(str+i)!='\0')
    //所有字符串的最后都有隐藏"\0"作为结束  这个循环的意思其实是将str字符串每个字符打印出来 直到所有的字符都一一打印出来也不停留~
    {
        printf("%c",str[i]);// *(str+i)以及str[i]在本质上是一样的  %c在C语言中代表字符型格式符
        i++;
    }
    printf("\n");
    return 0;
}
```

---

### 字符指针

下面是一种最基础的修改字符串数组内部元素方法：

```c
#include<stdio.h>
int main()
{
    char str[] = "hello faker";
    str[0] = '1';
    *(str + 1) = '2';
    printf("str = %s\n",str);//此时输出结果 12llo faker
    return 0;
}
```

下面这个是个进阶版本：

```c
#include<stdio.h>
int main()
{
    char str[] = "hello faker";

    //定义一个指针 指向首个元素
    char *p = NULL;
    p = &str[0];
    p = str;//数组名字就是首元素的地址 牢牢记住这个个概念
    
    *p = 'a';
    p++;
    *p = 'b';
    printf("str = %s\n",str);//此时输出结果 abllo faker
    printf("p=%s\n",p);//bllo faker 此时p从第二个元素开始显示
    printf("p = %s\n",p-1);//abllo faker p-1 继续从第一个元素开始显示
    return 0;   
}
```

---

### 字符拷贝问题

在讲解字符拷贝问题之前，我们先简单介绍一下strcpy()函数

```c
#include<stdio.h>
#include<string.h>//头文件<string.h>内包含strcpy函数
int main()
{	
    char a[20], c[] = "I am faker";
	strcpy(a, c);//这是C语言里面复制字符串的库函数, 函数声明包括在专门处理字符串的头文件<string.h>中 括号内的参数意思为 将字符串c内容赋值给到a 按照之前知识 我们是这么理解的 但是真正原因 请继续往下看
	printf(" c=%s\n", c);
	printf(" a=%s\n", a);

    return 0;
}
```

这道题的输出结果：

```c
 c=I am faker
 a=I am faker
```

在掌握了基础知识之后，我们继续：

```c
#include<stdio.h>
#include<string.h>

int main()
{
    char buf[100];
    char *p = buf;
    //1.p指向buf的首元素
    //2.strcpy()是给p所指向的内存拷贝内容，字符串拷贝给了buf
    strcpy(p,"hello faker");
    
    printf("p = %s,buf = %s\n",p,buf);
    return 0;
}
//这是一个错误示范
int main01()
{
    char *p;
    //1.不是给p变量拷贝内容
    //2.给p所指向的内存拷贝内容
    //3.p是野指针，给野指针所指向的内存拷贝内容，结果导致错误
    strcpy("p,"hello faker")
    
    return 0;
}
```

如果我们自己编写一个函数来实现，那应该怎么写呢：

```c
#include<stdio.h>
void my_strcopy(char *dst, char*src)
{
    int i = 0;
    while(*(src+i) != '\0')//在终止符之前一直循环
    {
     	*(dst + i) = *(src + i);
        i++;
    }
    *(dst+i) = '\0';//因为这个拷贝不包含终止符 在系统最后的时候必须手动添加
}

int main()
{	
    char src[] = "hello faker";
    char dst[100];
    char *p = dst;//定义一个char *类型的变量 存放dst数组首字符的地址
    
    my_strcopy(p,src);
    printf("dst = %s",dst);
    
    return 0;
}
```

这里有一个关于前面字符串知识的补充，我们必须确认3个0的区别：

```c
0：数字0，但是等价于终止符'\0'
'\0':终止符 用在字符串最后表示已经结束
'0':字符0
```

​		一个字符串如果没有终止符，就无法正常使用，有些编译器会对终止符自动补充，但是有的不会，所以在编写代码的时候要自己有意识

---

### const修饰字符指针

const我们不是第一次碰到哦，这次是关于修饰字符指针，直接开始例子：

```c
#include<stdio.h>
int main()
{
    char buf[] = "hello";
    char *p1 = buf;
    *p1 = 'a';//改变指针所指向的内存
    p1 = NULL;//改变指针变量本身
    
    //const修饰*，指针所指向的内存不能修改
    const char *p2 = buf;
    //*p2 = 'a'; err
    p2 = NULL;//  ok
    return 0;
}
```

---

###   字符串常量

首先明白两个概念：

1.每个字符串都是一个地址，这个地址是指字符串首元素地址；

2.字符串常量放在data区，文字常量区

例如：

```c
#include<stdio.h>
int main()
{
    char *p = "hello faker";
    //1.字符串常量就是此字符串的首元素地址 定义指针 然后直接将字符串的地址赋给指针相当合理
    printf("s1 = %p\n","hello faker");
    printf("p = %p\n",p);//这3个printf打印值都是一样 全是字符串首元素地址
   
    char *p2 = "hello faker";
        printf("s2 = %p\n","hello faker");//这3个printf打印值都是一样 全是字符串首元素地址
	// 2.字符串常量，文字常量区的字符串，只读，不可修改
    printf("*p1 = %c\n",*p1);//读，ok
	//3.p1指向字符串常量，字符串常量只读，不可修改
    *p1 = 'a';//修改 err
    return 0;
}
```

data（文字常量区）生命周期和程序是一样哦，程序结束，data才会释放。

```c
char *p = "hello";
char buf[] = "hello"
```

这两个语法有区别吗 显然：

```c
//1.p指针保存了"hello"的地址
//2.指针指向的内存不能修改
char *p = "hello";
//1.把"hello"一个一个字符放在buf数组中
//2.数组的元素可以修改哦
char buf[] = "hello"
```





























