## C语言学习笔记-day10

### 内存区介绍

在程序没有执行前，有几个内存分区已经确定，虽然分区确定，但是没有加载内存，程序只有运行时才加载内存：

text（代码区）：只读，函数

data：初始化的数据，全局变量，static变量，文字常量区（只读）

bss：没有初始化的数据，全局变量，static变量



当运行程序，加载内存，首先根据前面确定的内存分区（text，data，bss）加载，然后额外加载2个区

text（代码区）：只读，函数

data：初始化的数据，全局变量，static变量，文字常量区（只读）

bss：没有初始化的数据，全局变量，static变量

stack（栈区）：普通局部变量，自动管理内存

heap（堆区）：手动申请空间，手动释放，整个程序结束，系统也会自动回收，如果没有手动释放，程序也没有结束，这个堆区空间不会自顶释放

|      类型      |            存储位置             |
| :------------: | :-----------------------------: |
|    auto变量    |              栈区               |
| static局部变量 | 初始化在data段，末初始化在BSS段 |
|   extern变量   | 初始化在data段，末初始化在BSS段 |
| static全局变量 | 初始化在data段，末初始化在BSS段 |
|   extern函数   |             代码区              |
|   static函数   |             代码区              |
|  register变量  |      运行时存储在CPU寄存器      |
|   字符串常量   |             data段              |

### memset的使用

使用时必须包含头文件<string.h>

```c
#include<string.h>
void *memset(void*s,int c,size_t n);
//功能：将s的内存区域的前n个字节以参数c填入
//参数：
//    s：需要操作内存s的首地址
//	  c：填充的字符，c虽然参数为int，但必须是unsigned char，范围为0-255
//	  n：指定需要设置的大小
//返回值：s的首地址
```

具体用法例如：

```c
#include<stdio.h>
#include<string.h>

int main()
{
    int a;
    memset(&a,0,sizeof(a));//常用做法，确保a这个参数已经清零
    printf("a=%d\n",a);

    int a1;
    memset(&a1,97,sizeof(a1));//很多人觉得这里应该输出a1=97，其实不然，中间参数虽然是整型，但是却是按照字符串处理，也就是读取ASCII值
    printf("a1=%c\n",a1);

    int a2;
    memset(&a2,'a',sizeof(a2));
    printf("a2=%c\n",a2);//和a1输出结果一样

    int b[10];
    memset(b,0,10*sizeof(int));//将b整个数组全部清零
    //为什么要引入memset函数来对数组进行清零？
    //因为如果不用这个函数，就必须使用for循环来一位一位清零，这样效率显然不高
    //而且这个函数主要针对的是字符操作哦

    //我们想让一个数组所有的值都是b，该怎么做？
    char c[10];
    int i;
    memset(c,'b',10*sizeof(char));
    for(i=0;i<10;i++)
    {
        printf("%c",c[i]);//这样可以把所有值都赋值成b
    }

    return 0;
}
```

***

### memcpy函数

memcpy函数也是一个把一个字符串的内容传递给另一个字符串的函数，保存<string.h>文件。但是他与我们之前学的strncpy有所不同，因为strncpy的标准是读取到“\0“结束，但是memcpy函数可以避免这点，例如：

```c
#include<stdio.h>
#include<string.h>

int main()
{
    
    char p[] = "hello\0mike";//以字符串初始化，自动在默认隐藏一个结束符'\0'
    char buf[100];
    printf("sizeof(p)=%d\n",sizeof(p));
    strncpy(buf,p,sizeof(p));//使用strcpy函数
    printf("buf1 = %s\n",buf);
    printf("buf2 = %s\n",buf + strlen("hello")+1);//检测hello之后mike这个字符串是否已经复制到位
    
    memset(buf,0,sizeof(buf));//清零
    memcpy(buf,p,sizeof(buf));//赋值
    printf("buf3 = %s\n",buf);
    printf("buf4 = %s\n",buf + strlen("hello")+1);
    
    return 0;
}
```

输出结果：

```c
sizeof(p)=11
buf1 = hello
buf2 =
buf3 = hello
buf4 = mike
```

所以memcpy()不受限制，可以把所有内容拷贝

再举一个例子：

```c
#include<stdio>
#include<string.h>

int main()
{
    int a[10] = {1,2,3,4,5,6,7,8,9,10};
    int b[10];
    //第3个参数是拷贝内存的总大小
    memcpy(b,a,10*sizeof(int));
    memcpy(b,a,sizeof(a));
    
    //使用memcpy()最好别出现内存重叠
    //如果出现内存重叠，最好使用memmove
    memcpy(&a[2],a,5*sizeof(int));//这样编译虽然没有问题，但是最好还是别这么操作吧
    memmove(&a[2],a,5*sizeof(int));
    
    return 0;
}
```

***

### memcmp函数

memcmp函数比较两个变量，比较他们内部值的大小，这个函数保存在<string.h>文件，使用前需调用

使用格式：

```C
memcmp(&a,&b,sizeof(b));//这个程序比较a和b变量，比较数量是b的长度 注意是挨个比较啊
```

再来举个例子：

```c
#include<stdio.h>
#include<string.h>
int main()
{
    int a[10] = {1,2,3,4,5,6,7,8,9,10};
    int b[10] = {1,2,3,4,5,6,7,8,9,11};
    int flag = memcmp(a,b,10*sizeof(int));//比较十个数据大小，这里显然a的最后一个元素比b的最后一个元素小
    if(flag<0)
    {
        printf("a<b\n");
    }
    else if(flag>0)
    {
        printf("a>b\n");
    }
    else
    {
        printf("a==b\n");
    }
    
    return 0;
}
```

这个程序的输出结果为：

```c
a<b
```







