## C语言学习笔记-day15

### 文件指针

在C语言中使用一个指针变量指向一个文件，这个指针称为文件指针。

```c
typedef struct
{
    short	level;//缓冲区“满”或者“空”的程度
    unsigned flags;//文件状态标志
    char fd;//文件描述符
    unsigned char hold;//如无缓冲区不读取字符
    short  bsize;//缓冲区的大小
    unsigned char *buffer;//数据缓冲区的位置
    unsigned ar;//指针，当前的指向
    unsigned istemp;//临时文件，指示器
    short token;//用于有效性的检查
   
}FILE;
```

​		FILE是系统使用typedef定义出来的有关文件信息的一种结构体类型，结构中含有文件名、文件状态和文件当前位置等信息。

​		声明FILE结构体类型的信息包含在头文件“stdio.h”中，一般设置一个指向FILE类型变量的指针变量，然后通过它来引用这些FILE类型变量。通过文件指针就可以对它所指的文件进行各种操作。

值得注意的有以下几点：

1.FILE所有平台名字都一样，FILE是一个结构体类型，里面成员功能一样，不同平台成员名字不一样。

定义格式：

```c
FILE *fp
```

2.fp指针，只调用了fopen(),在堆区分配空间，把地址返回给fp；

3.fp指针不是指向文件，fp指针和文件关联，fp内部成员保存了文件的状态；

4.操作fp指针，不能直接操作，必须通过文件库函数来操作fp指针；

5.通过库函数操作fp指针，对文件的任何操作，fp成员里面成员会相应地变化（系统自动完成）。

***

### 文件分类

从用户或者操作系统的角度（逻辑上）把文件分为文本文件和二进制文件：

**文本文件：**基于字符编码的文件

**二进制文件：**基于值编码的文件



**文本文件:**

1.基于字符编码，常见编码有ASCII、UNICODE等

2.一般可以使用文本编辑器直接打开

3.数5678以ASCII存储形式（ASCII码）为：

00110101 00110110 00110111 00111000



**二进制文件：**
1.基于值编码，自己根据具体应用，指定某个值是什么意思

2.把内存中的数据按其在内存中的存储形式原样输出到磁盘上

3.数5678的存储形式（二进制码）为：00010110 00101110

***

### 标准文件设备指针

C语言中有三个特殊的文件指针由系统默认打开，用户无需定义即可直接使用：

**stdin:**  标准输入，默认为当前终端（键盘），我们使用的scanf、getchar函数默认从此终端获得数据。

**stdout:**  标准输出，默认为当前终端（屏幕），我们使用的printf、puts函数默认输出信息到此终端

**stderr:**  标准出错，默认为当前终端（屏幕），我们使用的perror函数默认输出信息到此终端。

举个例子：

```c
#include<stdio.h>

int main()
{
    printf("aaaaaaaa\n");
    fclose(stdout);//关闭标准输出文件指针
    printf("bbbbbbbb\n");

    
    return 0;
}
```

这里结果：

```c
aaaaaaaa
```

关闭标准输出文件指针，printf函数无法使用，寻找不到显示地方

***

perror函数

还是上面例子：

```c
#include<stdio.h>

int main()
{
    printf("aaaaaaaa\n");
    fclose(stdout);//关闭标准输出文件指针
    printf("bbbbbbbb\n");

	//打印库函数调用失败的原因
	perror("mike");
    
    return 0;
}
```

打印结果：

```c
aaaaaaaa
mike: Bad file descriptor
```

这个函数可以显示错误原因

如果稍稍修改：

```c
#include<stdio.h>

int main()
{
    printf("aaaaaaaa\n");
    //fclose(stdout);//关闭标准输出文件指针
    printf("bbbbbbbb\n");

	//打印库函数调用失败的原因
	perror("mike");
    
    return 0;
}
```

显示：

```c
aaaaaaaa
bbbbbbbb
mike: No error
```

没有错便显示No error

​                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               















