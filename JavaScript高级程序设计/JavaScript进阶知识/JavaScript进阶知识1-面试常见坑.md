## JavaScript常见面试坑之代码题

1. var/let在循环中声明变量，调用setTimeout

```
for (var i = 0; i < 3; i++) {  //用var关键字，变量是全局的
  setTimeout(() => console.log(i), 1);
}
//output: 3 3 3

for (let i = 0; i < 3; i++) {  //用let关键字，每次循环结束之后会生成一个新的变量，作用域之局限在循环中
  setTimeout(() => console.log(i), 1);
}
//output: 0 1 2

由于JS的事件队列机制（event queue），setTimeout的回调函数会在循环执行完之后去调用。
```



2. 对象中的普通函数和箭头函数this指向

```
const shape = {
  radius: 10,
  diameter() {
    return this.radius * 2; //output: 20
  },
  perimeter: () => 2 * Math.PI * this.radius  //output:NaN 这里的this还是指向的window
};

shape.diameter();
shape.perimeter();
```



3. 一元运算符类型转换

```
+true  // output: 1 一元运算符会将左右两侧变为数字，true则表示1
!"Lydia"  // output: false  "Lydia"true值取反

```


4. function是一种特殊的object

```
//What happens when we do this?
function bark() {
  console.log("Woof!");
}

bark.animal = "dog";
//It will be totally fine. Everything besides primitive types are objects.
```



5. 构造器添加的方法不能直接被实例调用，需要添加到其原型中
```
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const member = new Person("Lydia", "Hallie");
Person.getFullName = function() {
  return `${this.firstName} ${this.lastName}`;
};

console.log(member.getFullName());  //TypeError
//在一个构造函数里的方法是无法被其实例调用的。因为函数会在内存中占用空间，每个实例不一定都会用得到该方法，如果实例都创建一个相同的方法，
//则会占用很多不必要的空间。因此如果要实现这个功能，需要把方法添加到类的原型上

Person.prototype.getFullName = function() {  //原型上的方法可以被实例所共享，且只会占用一份空间
  return `${this.firstName} ${this.lastName}`;
};
```


6. 事件捕获顺序

```
//What are the three phases of event propagation?
A: Target -> Capturing -> Bubbling
B: Bubbling -> Target -> Capturing
C: Target -> Bubbling -> Capturing
D: Capturing -> Target -> Bubbling  //correct
```



7. 函数使用字符串模版传参时，第一个参数总是字符串模版本身，而后是按顺序传入的变量

```
function getPersonInfo(one, two, three) {
  console.log(one);
  console.log(two);
  console.log(three);
}

const person = "Lydia";
const age = 21;

getPersonInfo`${person} is ${age} years old`;   //output: ["", " is ", " years old"] "Lydia"  21

//If you use tagged template literals, the value of the first argument is always an array of the string values. The remaining arguments get the values of the passed expressions!
```

8. sessionStorage设置存储时长

```
sessionStorage.setItem("cool_secret", 123); //session storage would be removed after closing the tab

//while localStorage would have been there forever unless localStorage.clear() is invoked
```



9. 在内置构造器内添加原型方法

```
String.prototype.giveLydiaPizza = () => {
  return "Just give Lydia pizza already!";
};

const name = "Lydia";

name.giveLydiaPizza();  //output: "Just give Lydia pizza already!"

//String是一个内置的构造函数，是可以添加额外的属性的。在构造器的原型链里添加的方法，所有string变量都是共享调用
```

10. 给对象添加属性

```
const a = {};
const b = { key: "b" };
const c = { key: "c" };

//Object keys are automatically converted into strings
a[b] = 123;  //{"[Object object]": 123}
a[c] = 456;  //{"[Object object]": 456}

console.log(a[b]);  //output: 456
```



11. setTimeout执行顺序

```
const foo = () => console.log("First");
const bar = () => setTimeout(() => console.log("Second"));
const baz = () => console.log("Third");

bar();
foo();
baz();
//output: First Third Second
//setTimeout回调里的内容会在最后被打印；在浏览器中不光只有运行引擎，还有一个WebAPI
//setTimeout先调用，进入栈，其本身执行完之后会将回调函数传给WebAPI,然后出栈；接着调用foo,foo()进栈，打印First，出栈；调用baz，打印Third，出栈；
//此时栈是空的，WebAPI只能将事务放到Queue当中等待，等Stact空闲之后会去取Queue里面的事务执行
```


12. 类型判断

```
function sayHi() {
  return (() => 0)();  //executed immediately
}

typeof sayHi();  //output: 'number'
```



13. 添加数组元素

```
const numbers = [1, 2, 3];
numbers[10] = 11;
console.log(numbers); // output: [1, 2, 3, 7 x empty, 11]

//When you set a value to an element in an array that exceeds the length of the array, JavaScript creates something called "empty slots". These actually have the value of undefined, but you will see something like:
//[1, 2, 3, 7 x empty, 11]
//depending on where you run it (it's different for every browser, node, etc.)

```


14. 作用域

```
(() => {
  let x, y;
  try {
    throw new Error();
  } catch (x) {
    (x = 1), (y = 2); // 对传入catch作用的参数x赋值为1，而不是之前定义的x；而y则是针对外层定义的变量赋值
    console.log(x);  // output: 1
  }
  console.log(x);  // output: undefined  在catch作用域之外仍为undefined
  console.log(y); // output: 2
})();
```



15. setInterval 返回值

```
setInterval(() => console.log("Hi"), 1000);  //返回一个unique id，用于clearInterval()时使用
```
<br/>