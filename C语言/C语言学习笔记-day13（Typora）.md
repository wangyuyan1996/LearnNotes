## C语言学习笔记-day13

### 成员指针指向data区或者栈区

在赋值字符串之时，有一种使用指针将它指向文字常量区的方法，和之前方法颇为得类似。

```c
#include<stdio.h>
#include<stdlib.h>

struct Student 
{
    int age;
    char *name;//此处定义一个指针
    int score;
};//必须分号

int main()
{
    struct Student s;
    s.age = 18;
    s.name = "mike";//指针变量保存字符串常量的首地址
    s.score = 59;
    printf("%s",s.name);
    return 0;
}
```

还有一种方法

```c
#include<stdio.h>
#include<stdlib.h>

struct Student 
{
    int age;
    char *name;//此处定义一个指针
    int score;
};//必须分号
//指针指向栈区空间
int main()
{
    struct Student s;
    s.age = 18;
    
    char buf[100];
    s.name = buf;//指向栈区空间
    strcpy(s.name,"mike");
    s.score = 59;
    
    return 0;
}
```

还有一种方法

```c
#include<stdio.h>
#include<stdlib.h>
#include<stdlib.h>

struct Student 
{
    int age;
    char *name;//此处定义一个指针
    int score;
};//必须分号
//变量指针指向堆区空间
int main()
{
    struct Student s;
    s.age = 18;
    
 	s.name = (char*)malloc((strlen("mikejiang")+1)*sizeof(char));//增加一个放置“\0” 这样写是最准确 每个字符都是char
    s.name = buf;//指向栈区空间
    strcpy(s.name,"mike");
    s.score = 59;
    
    if (s.name!=NULL)
    {
       free(s.name);
        s,name = NULL;
    }
    
    return 0;
}
```

