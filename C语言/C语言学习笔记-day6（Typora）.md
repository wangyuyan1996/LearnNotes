## C语言学习笔记-day6

### 值传递和地址传递

在前面我们定义过函数，但是在不借助指针的情况下，我们如果想调用，可能会存在一定困难，例如：

```c
#include<stdio.h>

void swap(int m, int n)
{
    int temp;
    temp = m;
    m = n;
    n = temp;
    printf("m = %d, n = %d\n",m ,n);
}  
    int main()
    {
        int a = 11;
        int b = 22;
        
        swap(a,b);//值传递，形参的修改不会影响到实参 变量本身传递 不管这个变量什么类型 
        printf("a = %d, b = %d\n", a,b);
    
    	return 0;
    }

```

在我们的理解，a和b值应该已经互换，但是其实结果并不是这样哦：

```c
m = 22, n = 11
a = 11, b = 22
```

​		我们可以发现其实结果并不是我们想的那样，因为我们单纯对函数的值进行变换其实是改变不了输出结果，这个时候我们必须借助指针：

```c
#include<stdio.h>

void swap(int *m, int *n)
{
    int temp;
    temp = *m;
    *m = *n;
    *n = temp;

}  
    int main()
    {
        int a = 11;
        int b = 22;
        
        swap(&a,&b);//地址传递，变量的地址
        printf("a = %d, b = %d\n", a,b);
    
    	return 0;
    }

```

这种情况下，输出改变哦：

```
a = 22, b = 11
```

记住一个重要结论：

**如果想通过函数改变实参，必须地址传递**

***

### 形参中的数组

```c
#include<stdio.h>

//1.形参中的数组，不是数组，它是普通指针变量
//2.形参数组：int a[100000],int a[],int *a对编译器而言，没有任何区别
//3.编译器都是当做int *处理
//4，形参中的数组和非形参数组区别：型参中的数组是指针变量，非形参的数组就是数组
void print_array(int a[]) //定义第一个的函数 形参int a[]这里不是数组而是指针
{
    int i = 0;
    //64位系统，sizeof(a)，a是指针变量，结果为8
    //sizeof(a[0])第0个元素，是int类型的，结果为4呢
    int n = sizeof(a)/sizeof(a[0]);//8/4=2
    printf("sizeof(a)=%d\n",sizeof(a));
    printf("sizeof(a[0]) = %d\n",sizeof(a[0]));
    
    for(i=0;i<n;i++)
    {
        printf("%d,",a[i]);//等价*(a+i)
    }
    printf("\n");
}

void print_array2(int a*,int n)
{
    int i = 0;
    for(i =0; i< n;i++)
    {
        printf("%d,a[i]");
    }
    printf("\n");
}
int main()
{
    int a[] = {1,-2,3,-4,5,-6,7,-8,9};
    int n = sizeof(a)/sizeof(a[0]);
    print_array(a,n);//应该把数组元素个数传递进去
}

int main()
{
    int  a[] = {1,-2,3,-4,5,-6,7,-8,9};
    int i = 0;
    int n = sizeof(a)/sizeof(*a);
    
    printf("排序前\n");
    for(i=0;i<n;i++)
    {
        printf("%d",a[i]);
    }
    //冒泡排序 这前面没有提及冒泡排序的问题，我后面会做补充
    int j = 0;
    int tmp;
    for(i = 0;i< n -1;i++)
    {
        for(j=0;j<n-1-j;j++)
        {
            if  (a[j]>a[j+1])
            {
                tmp = a[j];
                a[j]=a[j+1];
                a[j+1]=tem;
            }
        }
    }
    printf("排序后\n");
    for(i = 0;i<n;i++)
    {
        printf("%d",a[i]);
        
    }
    printf("\n");
    return 0;
}
```

























