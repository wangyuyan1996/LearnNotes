# Spring 学习笔记3

> 作者：DZF  
> 邮箱：872573678@qq.com

本节笔记将使用上一次的笔记所建立的Spring工程基础上，问候世界。

## 创建package

* 在scr目录下建立一个package
* 将package名字命名为Demo

<img src=".\image\image-20200405164135916.png" alt="image-20200405164135916" style="zoom:33%;" />

## 创建xml文件

* 在scr目录下创建一个xml文件
* 将xml文件命名为application.xml

<img src=".\image\image-20200405164357139.png" alt="image-20200405164357139" style="zoom:33%;" />

## 编写代码

* 在Demo中创建问候世界类`HelloWorld.java`

```java
package Demo;

public class HelloWorld {
	   private String message;
	   public void setMessage(String message){
	      this.message  = message;
	   }
	   public void getMessage(){
	      System.out.println("Your Message : " + message);
	   }
}
```

* 在Demo中创建问候世界主函数`Main.java`

```java
package Demo;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Main {
   public static void main(String[] args) {
      ApplicationContext context = 
             new ClassPathXmlApplicationContext("application.xml");
      HelloWorld obj = (HelloWorld) context.getBean("helloWorld");
      obj.getMessage();
   }
}
```

* 编写`application.xml`文件

```xml
<?xml version="1.0" encoding="UTF-8"?>

<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">

   <bean id="helloWorld" class="Demo.HelloWorld">
       <property name="message" value="Hello World!"/>
   </bean>

</beans>
```

## 来问候一下世界吧

* run一下，即可问候世界

<img src=".\image\image-20200405164901551.png" alt="image-20200405164901551" style="zoom: 50%;" />
