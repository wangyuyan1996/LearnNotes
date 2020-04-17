# Spring学习笔记4

> 作者：dzf  
>
> 邮箱：872573678@qq.com

本节笔记将主要介绍如何在maven环境下使用spring问候这个美好的世界

* maven安装教程参见：https://blog.csdn.net/nicole_33/article/details/90739361
* mac下安装环境参阅e宝SpringMVC教程

### 新建maven项目

* File --> new --> other --> Maven --> Maven Project --> Next --> Next
* Group Id 填一个你的组织名称，Artifact Id 填你这个project的名称，这里简单填一个demo
* 新建完之后生成的目录如下所示

<img src=".\image\image-20200412001010222.png" alt="image-20200412001010222" style="zoom:50%;" />

<img src=".\image\image-20200412001548635.png" alt="image-20200412001548635" style="zoom:50%;" />



### 使用maven管理jar包

* 引入需要的`jar`包，如果你的`maven`本地库里没有，`maven`会自己下载
* 需要修改`pom.xml`文件来管理jar包
* 我们可以去中央库查我们需要的包怎么引入https://mvnrepository.com/

```xml
<!-- https://mvnrepository.com/artifact/org.springframework/spring-context -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.2.5.RELEASE</version>
</dependency>
```

* 我们的需要的依赖包，要写在`<dependencies></dependencies>`中 

> 对于`maven`中`pom.xml`，这里有详细的介绍https://www.cnblogs.com/xiaobaizhiqian/p/8214035.html



### 问候一下这个美好的世界吧

* 在`scr/main/java`下的`com.sgg.demo`中建立HelloWorld.java文件

```java
package com.sgg.demo;
 
public class HelloWorld {
 
	private String name;
 
	public void setName(String name) {
		this.name = name;
	}
 
	public void printHello() {
		System.out.println("Hello World Again! ");
        System.out.println("                  by " + name);
	}
}
```

* 在`scr/main/java`下的`com.sgg.demo`中编辑`App.java`文件

```java
package com.sgg.demo;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class App {
 
	public static void main(String[] args) {
		final ApplicationContext context = new ClassPathXmlApplicationContext("SpringBeans.xml");
 
		final HelloWorld obj = (HelloWorld) context.getBean("helloBean");
		obj.printHello();
	}
}
```

* 在`scr/main/`目录下建立文件夹resources，并新建SpringBeans.xml文件

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">
 
    <bean id="helloBean" class="com.sgg.demo.HelloWorld">
        <property name="name" value="dzf415" />
    </bean>
 
</beans>
```



![image-20200412004619826](.\image\image-20200412004619826.png)