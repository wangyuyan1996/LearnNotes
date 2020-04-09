### 数组反转

```c
#include<stdio.h>
int main()
{
    int a[] = {1,2,3,4,5,6,7,8,9};
    int n =sizeof(a)/sizeof(a[0]);//sizeof 计算这个数组大小 数组九个元素 全为int int一个占据四个字节 故大小三十六
    int i = 0;//首元素下表
    int j = n - 1;//尾元素下标
    int tmp;
    
    while(i < j)
    {
        //交换a[i]和a[j]
        tmp = a[i];
        a[i] = a[j];
        a[j] = tmp;
        i++;//从左往右
        j--;//从右往左
        
    }
    for(i=0;i<n;i++)
    {
        printf("%d",a[i]);
    }
         return 0;       
}
```

***

### 冒泡排序

相邻连个元素比较，如果a[i]>a[i+1]，交换

```c
比如：a[4]={-1,7,3,4}
1.比较第一个和第二个元素，-1<7 不需交换
2.比较第二个和第三个元素，7>3 需要交换 数组变为{-1,3,7,4}
3.比较第三个和第四个元素，7>4 需要交换 数组变为{-1,3,4,7}
第一轮结束，此时可以确定最大的数已经放到最后
1.比较第一个和第二个元素，-1<3 不需交换
2.比较第二个和第三个元素，3<4 不需交换
第二轮结束，此时可以确定二大的数已经放到最后
1.比较第一个和第二个元素，-1<3 不需交换
第三轮结束，冒泡排序完成                            

```

写成代码：

```c
#include<stdio.h>
int main()
{
    int a[] = {1,-1,2,-2,3,-3,4,-4};
    int n =sizeof(a)/sizeof(a[0]);
    
    int i = 0;
    int j = 0;
    int tmp;
    printf("排序前\n");
    for(i=0;i<n;i++)
    {
        printf("%d, ",a[i]);
    }
    printf("\n");
    for(i=0;i<n-1;i++)
    {
        for(j=0;j<n-i-1;j++)
        {
            if(a[j]>a[j+1])//比较相邻两个元素，大于交换
            {
                tmp = a[j];
                a[j] = a[j+1];
                a[j+1] = tmp;
            }
        }
    }
    printf("排序后\n");
    for(i=0;i<n;i++)
    {
        printf("%d, ",a[i]);
    }
    printf("\n");
    return 0;
    
}
```



















