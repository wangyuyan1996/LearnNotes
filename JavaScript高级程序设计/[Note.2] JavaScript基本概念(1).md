## 2. JavaScript基本概念(1)
#### 2.1 语法
- **区分大小写<br/>**
    所有的变量、函数名和操作符都区分大小写，但函数名不能使用typeOf，因为这是一个关键字
- **标识符<br/>**
    标识符，其实就是指变量、函数、属性的名字，或者函数的参数。标识符命名规则：
    ⑴ 第一个字符必须是字母，下划线或者一个美元符号
    ⑵ 其他字符可以是字母、下划线、美元符号或数字

    >   其实也可以包含ASCII和Unicode字符，但不推荐这样做

    推荐使用驼峰大小的格式命名，及第一个字母小写，剩下每个有意义的单词的首字母大写：
    > firstSecond<br/>
    > myCar<br/>
    > doSomethingImportant


```
不能把关键字、保留字、true、false和null用作标识符
```

- **注释<br/>**
    ⑴ 单行注释<br/>
    
    ```
    // 这是一个单行注释
    ```
     ⑵ 多行（块级）注释
     
    ```
    /*
     *  这是一个多行      // 第二行第三行的*号是非必须的
     *  (块级)注释
     */
    ```

- **严格模式<br/>**
    ECMAScript(下称ES) 5当中引入了严格模式（strict mode），该模式是为JavaScript定义一种不同的解析与执行模型。在严格模式下，ES3的一些不确定行为会得到处理，而且对某些不安全操作会抛出错误。
    
    ```
    // 整个脚本启用严格模式，文件顶部添加
    "use strict";
    ```
    
    ```
    // 只在函数内部启用严格模式
    function doSomething () {
      "use strict";
    }
    ```

    >    支持严格模式的浏览器包括IE 10+、Firefox 4+、Safari5.1+、Opera 12+和Chrome
    

- **语句<br/>**
    ES中的语句一般以分号结尾，但不是必需的，如未添加则由解析器确定语句的结尾


```
    var sum = a + b  // 虽然没有分号有效，但是不推荐
    var diff = a - b;  //推荐
```

我们也可以使用C语言风格把语句组合到一个代码块中：

```
    if (test)
        alert("test");   // 有效但是容易出错，不推荐
    
    if (test) {
        alert("test");   // 推荐
    }
```


#### 2.2 关键字和保留字
关键字是语言保留的，不能用作标识符

```
// 截至第五版的关键字：
break do instanceof typeof case else new
var catch finally return void continue
for switch while debugger function this
with defalt if throw delete in try
```

```
// ECMA-262还描述了一组可能在未来会被作为关键字的保留字，这些也不能作为标识符：
abstract enum int short boolean export
interface static byte extends long super
char final native synchronized class
float package throws const goto private
transient implements protected volatile
double import public
```

```
// 严格模式下第五版还对以下保留字加了限制：
implements package public interface private
static let protected yield
```

#### 2.3 变量
ES变量是松散型的，即可以用来保存任何类型的数据。也就是，每个变量只是一个用于保存值的占位符而已。定义变量时可以使用操作符var，在ES6中引入了let。

```
// 定义变量
var message // ES5 使用方法，不推荐，会导致变量提升
let message // ES6 推荐使用方法，不会产生变量提升，最好不要两者混用

// 以上的代码定了一个名为message的变量，像这样未被初始化赋值的变量，会被保存一个特殊的值——undefined，也可以直接在定义时对变量进行初始化：
var message = "Hi"
let message = "Hi"

// 在这里变量message在初始化时被定义为了字符串类型，虽然再将message赋值为其他类型的值完全是有效的，但是并不推荐这么做，如：
message = 100
```

使用var/let定义的变量为局部变量，是在其所在的作用域中有效，退出其所在的作用域后变量就会被销毁

```
function test () {
    var message = "Hi";
}
test ();
alert(message);  // 会报错, message is not defined

// 但如果不使用var/let关键字，变量就会变成全局变量, 这里只要调用了test函数，message就定义成了全局变量

function test () {
    message = "Hi";  // 不推荐不使用关键字定义变量，对变量的维护不友好，而且严格模式下这样会报错
}
test ();
alert(message);  // "Hi"
```
可以使用一条语句定义多个变量，初始化/不初始化均可，使用逗号分隔：<br />
let message = "Hi", name = "Zhang San", age;

> 严格模式下不可以使用eval或arguments的变量

<br />

> **小知识补充——"变量提升"**： <br />
使用关键字var定义变量会使得其定义的函数或者变量总是被解析器提升到其作用域的顶部声明
<br />
<br />
举个栗子：

```
    (function (){
        console.log(foo);
        var foo = "Javascript";
    })();
// 控制台输出 undefined
```

> 为什么这里输出的是undefined而不是报错呢，是因为javascript是函数作用域，解析器会在函数开头处自动去声明局部变量，局部变量都会被放在函数的入口处定义，所以上面的代码实际会被解释成：

```
(function (){
 	var foo;
    console.log(foo);
    foo = "Javascript";
})();
```
> 这里有一个关于函数声明的**小坑**:

```
// function fn(){}  函数声明式
// var fn = function(){}  函数表达式

(function(){
    fn();
    function fn() {
        console.log("This is from function fn.");
    }
})();
// 控制台输出 "This is from function fn."


(function(){
    fn();
    var fn = function() {
        console.log("This is from function fn.");
    }
})();
// 控制台报错，fn is not a function

```
> 上述例子表明使用函数声明式的情况下，可以将调用语句写在函数声明之前，但是后者使用函数表达式的方式声明的话，则会出现报错。<br />
在JavaScript中，**变量的声明会被提升，而变量的赋值则不会**。但函数的声明与变量的声明不一样，**函数的函数体也会被一起提升，所以使用函数声明的形式才会发生提升**。
<br />
<br />