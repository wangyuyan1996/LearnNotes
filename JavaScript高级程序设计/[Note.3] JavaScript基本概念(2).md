## JavaScript基本概念(2)

#### 2.4 数据类型
ES中有5种简单类型
- undefined
- Null
- Boolean
- Number
- String

还有一种复杂类型
- Object // 本质是由一组无序键值对组成

> ES不支持创建自定义类型机制，由于ES数据类型具有动态性，所以没有再定义其他数据类型对必要

##### 1）typeof操作符
typeof是用来检测给定变量的数据类型的，调用它返回的是一个字符串
返回值可能如下：
- "undefined"  // 这个值未定义
- "boolean"  // 这个值是布尔值
- "string"  //这个值是字符串
- "number"  //这个值是数值
- "object"  //这个值是对象或null, null被认为是一个空的对象引用
- "function"  //这个值是函数


```
// example

console.log(typeof "message");  // "string"
console.log(typeof 100); // number

let a = [];
console.log(typeof a); // "object"
```

##### 2）Undefined类型
Undefined类型只有一个值就是undefined, 在声明变量时未对其赋值则这个变量就是undefined。
<br/>
不过，等于undefined的变量和尚未定义的变量是不一样的。

```
// example

let message;  // 这个变量声明了但是没有初始化赋值所以获得了undefined值

console.log(message);  // undefined
console.log(name);  // 报错 “name is not defined”
```

> 有个tricky的地方，对未初始化和未声明对变量执行typeof都会返回undefined, 两种变量从技术角度上说虽然有本质区别，但实际上无论对哪一种都不能执行真正都操作

```
console.log(typeof message);  // "undefined"
console.log(typeof name);  // "undefined"
```

##### 3）Null类型
Null类型也只有一个值，也就是null。它表示一个空对象指针，这也是使用typeof操作符检测null时返回"object"的原因。

```
console.log(typeof null);  // "object"
```

如果定义的变量想用于保存对象，可以在初始化时赋为null，这样只要直接检查null就知道对应的变量是否已经存在一个对象的引用了。

> 实际上，undefined值派生自null, 所以在比较两者的值时，它们是相等的

```
console.log(null == undefined);  // == 双等号相等操作符只比较值不比较类型（后面会有详细说明），此处为true
```
尽管它们之间有这样的联系，但两者用途完全不同。无论什么情况下都无需把一个变量显式地赋值成为undefined，而如果定义变量想用于存放对象，则建议显式地将变量赋值为null

```
let message = null;

// 这样不仅可以体现null作为空对象指针的惯例，也有助于进一步区分null和undefined
```

##### 4）Boolean类型
Boolean是用的最多的类型之一。只有两个字面值true和false。
> 注意：true和false是区分大小写的，也就是说True和False不属于Boolean值，其他大小写形式也一样。它们只是标识符

如果要将一个值转换成其对应的Boolean值，可以调用转型函数Boolean():

```
let message = "Hello world!";
let messageBoolean = Boolean(message);  // true
```
任何数据类型的值调用Boolean()都会返回一个Boolean的值，以下为转换规则：

数据类型 | 转换为true的值 | 转换为false的值
---|---|---
Boolean | true | false
String | 任何非空字符串 | "" （空字符串）
Number | 任何非零数字值（包括无穷大） | 0和NaN
Object | 任何对象 | null
Undefined | - | undefined

```
// example

let message = "Error";
if (message) {  // if语句会自动对判断值做Boolean转换
    console.log(message);  // 会执行到这里并打印出"Error"
}

```

##### 5）Number类型
Number类型可以用来表示**整数和浮点数值**。除了常见对十进制外，整数还可以通过八进制、十六进制的字面值来表示。<br>
八进制第一位必须是0，然后是0-7的数字序列。如果字面中的数字超出了范围，前导0将被忽略当做十进制解析。

```
let octalNum1 = 070  // 八进制数值，转化成十进制为56
let octalNum2 = 08   // 无效八进制数值，按十进制解析为8
```

十六进制前两位必须是0x, 然后跟着（0-9，A-F）字母大小写均可。

```
let hexNum1 = 0xA  // 10
let hexNum2 = 0x1f // 31
```
> 算数计算中，八进制和十六进制都会被转换成十进制计算
> JavaScript中可以保存+0和-0，正零和负零被认为相等


// 未完待续...