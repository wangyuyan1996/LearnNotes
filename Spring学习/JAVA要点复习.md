# JAVA要点复习

> 作者：DZF  
>
> 邮箱：872573678@qq.com

***说明***

> 本文档主要用于记录DZF在学习spring过程中复习的JAVA遗忘的各种杂七杂八的知识点，  
>
> 同时本文档也会为未来的面试做准备，会涉及部分面试问题。



* **JDK、JVM、JRE是什么？**

  * **JVM**：英文名称（Java Virtual Machine），就是我们耳熟能详的 Java 虚拟机。它只认识 xxx.class 这种类型的文件，它能够将 class 文件中的字节码指令进行识别并调用操作系统向上的 API 完成动作。所以说，jvm 是 Java 能够跨平台的核心。
  * **JRE**：英文名称（Java Runtime Environment），Java 运行环境。它主要包含两个部分，jvm 的标准实现和 Java 的一些基本类库。它相对于 jvm 来说，多出来的是一部分的 Java 类库。也就是我们说的JAVA平台，所有的Java程序都要在JRE下才能运行。包括JVM和JAVA核心类库和支持文件。与JDK相比，它不包含开发工具——编译器、调试器和其它工具。
  * **JDK**：英文名称（Java Development Kit），Java 开发工具包。jdk 是整个 Java 开发的核心，它集成了 jre 和一些好用的小工具。例如：javac.exe，java.exe，jar.exe 等。

  这三者的关系是：一层层的嵌套关系。**在JDK的安装目录下有一个jre目录**，里面有两个文件夹bin和lib，在这里可以认为**bin里的就是jvm，lib中则是jvm工作所需要的类库，而jvm和 lib合起来就称为jre。**  

  **Java 能够跨平台运行的核心在于 JVM** 。Java 引入了字节码的概念，jvm 只能认识字节码，并将它们解释到系统的 API 调用。针对不同的系统有不同的 jvm 实现，有 Linux 版本的 jvm 实现，也有 Windows 版本的 jvm 实现，但是同一段代码在编译后的字节码是一样的。

* **堆与栈**
  * **堆**：虚拟机启动时创建，被所有线程共享 ，存放对象实例以及数组，垃圾回收机制主要管理堆。堆的**优势**是可以动态地分配内存空间，需要多少内存空间不必事先告诉编译器，因为它是在运行时动态分配的。但**缺点**是，由于需要在运行时动态分配内存，所以存取速度较慢。
  * **栈**：栈中主要存放一些**基本数据类型的变量**（byte，short，int，long，float，double，boolean，char）和对象的**引用**。栈的**优势**是，存取速度比堆快，栈数据可以共享。但**缺点**是，存放在栈中的数据占用多少内存空间需要在编译时确定下来，缺乏灵活性。

* **栈数据可以共享**

  String 可以用以下两种方式来创建：

  ```java
  String str1 = new String("abc");
  String str2 = "abc";
  ```

  * 第一种使用new来创建的对象，它存放在堆中。每调用一次就创建一个新的对象。
  * 第二种是先在栈中创建对象的引用str2，然后查找栈中有没有存放“abc”，如果没有，则将“abc”存放进栈，并将str2指向“abc”，如果已经有“abc”， 则直接将str2指向“abc”。

  ```java
     public static void main(String[] args) {
          String str1 = new String("abc");
          String str2 = new String("abc");
          System.out.println(str1 == str2);
      }
  ```

  * 输出false

  ```java
     public static void main(String[] args) {
          String str1 = "abc";
          String str2 = "abc";
          System.out.println(str1 == str2);
      }
  ```

  * 输出true
  * 用第二种方式创建多个“abc”字符串，在内存中其实只存在一个对象而已。 这种写法有利于节省内存空间。 同时还可以提高程序的运行速度，因为JVM会自动根据栈中数据的实际情况来决定是否创建新对象。