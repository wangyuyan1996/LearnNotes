## JavaScript中容易被忽视的冷知识

#### 1. Null和undefined的本质区别
- 给一个全局变量赋值null, 相当于这个变量的指针对象以及值清空，如果是给对象的属性赋值null，或者局部变量赋值为null, 相当于给这个属性分配了一块空的内存然后值为null, JS会回收全局变量为null的对象。
- 给一个全局变量赋值为undefined，相当于将这个对象的值清空，但是这个对象依旧存在，如果是给对象的属性赋值undefined，说明这个值为空。
- 值null是一个字面量，undefined是全局对象的一个属性。null是表示缺少的标识，指示变量未指向任何对象
 
#### 2.

```
const foo = {}
Foo.prop = 123 //可以复制成功
Foo = {} //TypeError: 'foo' is read-only
```

const是保证变量指向的那个内存地址所保存的数据不得改动，对于简单类型的数据，值就保存在变量指向的那个内存地址，因此等同于常量。
<br/>
<br/>
但对于引用类型，变量指向内存地址，保存的 指示一个指向实际数据的指针，const只能保证这个指针是固定的，而指向的数据结构可以改变。

#### 3. BFC(Block formatting context) 块级格式化上下文
可以理解成为某个元素的一个css属性，只不过这个属性不能被开发者显示修改，拥有这个属性的元素对内部元素和外部元素会表现出一些特性。

**触发条件：**
根元素，及HTML元素
float的值不是none
overflow的值不是visible
display的值为inline-block、table-cell、table-caption
position的值为absolute或者fixed

#### 4. 函数创建原型
每个函数在创建时都会有它的prototype(原型)，指向一个object<br/>

为了多个实例共享方法
**Object.create**

```
// 该方法创建一个新的对象，使用传入的对象来提供所创建新对象的prototype，可以作为一种继承的方式
function Animal(name, energy) {
    let animal = Object.create(Animal.prototype)
    animal.name = name
    animal.energy = energy
    
    return animal
}

const leo = Animal('Leo', 5)

// if use 'new' keyword to create the instance of Animal, 'new' would help to do the above to the below

function Animal(name, energy) {
    this.name = name
    this.energy = energy
}

const leo = new Animal('leo', 5)

Object.getPrototypeOf() // 参数是一个实例，可以获取这个实例原型上的所有方法
```
ES8中有Object.values() / Object.keys() / Object.entries()
Object.getOwnPropertyDescriptors 获取自身所有属性的描述符，如果没有自身属性则返回空对象

> 箭头函数没有constructor，没有prototype，不能使用new来创建实例


#### 5. Array.reduce()
接受两个参数，第一个是一个**回调函数**，第二个是**赋初始值**

```
const numbers = [1, 2, 3, 4]
const sum = numbers.reduce((accumulator, currentValue) => {
    return accumulator + currentValue  //some process
}, 0)
```
<br/>

