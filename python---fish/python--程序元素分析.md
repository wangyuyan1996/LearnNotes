#1.python程序元素分
##1.1温度转换程序讲解
【缩进】

1个缩进=4个空格



1. 缩进是用在python中标明代码之间的层次关系；

1.  缩进是python语言中表明程序框架的唯一手段；

【注释】



1. 注释是程序员在代码中加入的辅助说明信息，它不能被计算机执行，也不受语法约束，可以在里面写入任何内容。
2. 一般来说，注释用来帮助程序员记录程序设计方法，辅助程序阅读；
3. 注释的两种方法：①单行注释以#开头；②多行注释以"开头和结尾;


【变量】

1. val/c/f等

【命名】

1. 命名指给程序中自定义元素关联名字的过程，命名需要保证在程序中，名字具有唯一性；
2. 命名需要符合如下规则：①命名规则使用大小写字母、数字和下划线的组合，但首字母只能是大小写字母或者下划线，不能使用空格；②中文等非字母符号也可以作为符号。

【表达式】

1. 表达式指程序中产生或计算新数据值的一行代码；
2. python语言的33个保留字或者操作符可以产生符合语法的表达式；

【空格的使用】

1. 表示缩进关系的空格不能改变；
2. 空格不能将一个命名分割；
3. 除上述两条外，程序中可以任意使用空格增加程序可读性。

【输入函数】

1. input（）函数从控制台获得用户输入；使用方法如下：<变量>=input（<提示性文字>);
2. 获得的用户输入以字符串形式保存在<变量>中。

【表达式】

1. 如果val="28C"
2. 则val[-1]是最后一个字符"C"
3. 前两个字符组成的字串可以用val[0:2]表示，它表示一个从[0，2）的区间；
4. 由于约定用户输入的最后一个字符是C或者F，之前是数字，所以通过val[0:-1]来获取除最后一个字符外的字符串。

【分支语句基本过程】

if <条件1成立>:

  <表达式组1>

elif<条件2成立>:
 
  <表达式组2>

......

elif<条件N-1成立>:
    
   <表达式组N-1>

else:

   <表达式组N>

【赋值语句】

1. 同步赋值指同时给多个变量赋值，即先运算右侧N个表达式，然后同时将表达式结果赋值给左侧；
 
[例]将变量x和y交换
1. 采用单个赋值，需要3行语句：即通过一个临时变量t缓存x的原始值，然后将y值赋给x，再将x的原始值通过t赋值给y；

【输出函数】

1. print（）函数用来输出字符信息，或者以字符形式输出变量的值。


【循环语句】

1. 循环语句是控制程序循环运行的语句。这类语句一般根据判断条件或者计数条件确定一段程序的运行次数；
2. 计数循环基本过程
for in range(<技术值>):<表达式组>

【例】：使某一段程序连续运行10次
for i in range(10):<表达式组>





