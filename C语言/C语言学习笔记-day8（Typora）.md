## C语言学习笔记-day8（今天是做练习的快乐一天）

### 查找匹配字符串出现的次数（练习）

```c
#include<stdio.h>
#include<string.h>//strstr(str1,str2)函数被包含在 string.h 文件 strstr(str1,str2) 函数用于判断字符串str2是否是str1的子串。如果是，则该函数返回str2在str1中首次出现的地址；否则，返回NULL。

    int main()
{
    char *p = "11abcd222222abcd333333abcd4444444444abcd33dd";
    int i = 0;
    char *tmp = NULL;
    while(1)//一直循环
    {
        //查找匹配字符，如果找到，返回匹配字符串的地址，没有找到返回空
        tmp = strstr(p,"abcd");
        if (tmp == NULL)//没有找到
        {
            break;//跳出循环
        }
        else//找到
        {
            i++;//累加
            //重新寻找起点
            p = tmp + strlen("abcd");
        }
    }
    printf("abcd出现的次数为：%d",i); 
    return 0;
}
```

***

输入数组，最大的与第一个元素交换，最小的与最后一个元素交换，输出数组。

```c
#include<stdio.h>
    int main()
{
    int a[] = {2,3,6,1,8,4,9,11,16};//定义一个数组
    int *p  = a;//定义指针p指向a数组的首元素地址
    int l,i,n,m,tmp;
    int max = *p;
    int min = *p;
    l = sizeof(a)/sizeof(a[0]);//确定数组长度
	//循环10次寻找最大数max记录最大数下标n
    for(i=0;i<l;i++)
    {
        if(*p<(*(p+i)))
            {
                max = *(p+i);
                n = i;
            }
    }
    //循环10次寻找最小数min记录下最小数下标m
    for(i=0;i<10;i++)
    {
        if(*p>(*(p+i)))
            {
                min = *(p+i);
                m = i;
            }
    }
    //定义一个中间变量tmp 交换最大元素和第一个元素
    tmp = *p;
    *p = *(p+n);
    *(p+n)=tmp;
    //定义一个中间变量tmp 交换最小元素和最后一个元素
    tmp = *(p+l);
    *(p+l) = *(p+m);
    *(p+m) = tmp;
	//循环打印数组每个元素
    for(i=0;i<l;i++)
    {
        printf("%d ",*(p+i));

    }
    return 0;
}

```

我的输出结果：

```c
16 3 6 1 8 4 9 11 2
Process returned 0 (0x0)   execution time : 0.075 s
Press any key to continue.
```

程序运行时间也是衡量程序质量的重要标准，兄弟们要注意啊，这是我自己写的，大家有更好的欢迎讨论

***

输入一个整数，并将其反转后输出

```c
#include<stdio.h>

    int main()
{
    int old;
    int new_number = 0;
    int n;
    printf("请输入一个数\n");
    scanf("%d",&old);
    while(old!=0)
    {
        n=old%10;
        old = old / 10;
        new_number = new_number * 10 + n;
    }
    printf("%d\n",new_number);



    return 0;

}
```









