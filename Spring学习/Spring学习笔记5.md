# Spring学习笔记5

> 作者：DZF  
>
> 邮箱：872573678@qq.com

## IoC容器

* `Spring`容器时`Spring`框架的核心。
* 容器创建对象、连接对象、配置对象，管理整个创建至销毁的全生命周期
* 容器使用依赖注入（DI）管理应用程序组件
* 被管理的对象成为Beans

**容器如何工作？**

* 阅读配置元数据的指令，了解对哪些对象进行实例化、配置与组装
* 元数据可通过XML，Java注释或Java代码表示
* Spring IoC容器利用Java的POJO类与配置元数据生成完全配置可执行的系统或应用程序

![Spring IoC 容器](https://atts.w3cschool.cn/attachments/image/wk/wkspring/ioc1.jpg)

**两种容器**

*  ***Spring BeanFactory 容器***

  它是最简单的容器，给 DI 提供了基本的支持，它用 org.springframework.beans.factory.BeanFactory 接口来定义。BeanFactory 或者相关的接口，如 BeanFactoryAware，InitializingBean，DisposableBean，在 Spring 中仍然存在具有大量的与 Spring 整合的第三方框架的反向兼容性的目的

* ***Spring ApplicationContext 容器***

  该容器添加了更多的企业特定的功能，例如从一个属性文件中解析文本信息的能力，发布应用程序事件给感兴趣的事件监听器的能力。该容器是由 org.springframework.context.ApplicationContext 接口定义。

## BeanFactory容器

* 最简单的容器，为依赖注入提供支持
* BeanFactory类最为常用的接口实现是XmlBeanFactory类
* XmlBeanFactory容器从XML文件读取配置元数据，生成配置系统或应用
* 一般不选择使用BeanFactory，但在移动设备（资源宝贵）或基于applet的应用中会被优先选择

### 简单案例

> 一个CD player可以简单视为三部分组成，分别为电源、碟片、耳机，播放player需要依次检查电源、碟片、耳机是否就位，请用代码表示检查是否可以播放的流程。

* maven文件

```XML
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.sgg</groupId>
  <artifactId>test_bean_factory</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <packaging>jar</packaging>

  <name>test_bean_factory</name>
  <url>http://maven.apache.org</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>

  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>

	<dependency>
	    <groupId>org.springframework</groupId>
	    <artifactId>spring-context</artifactId>
	    <version>4.1.6.RELEASE</version>
	</dependency>
	
  </dependencies>
</project>

```



* 创建一个`Power`类

```java
package com.sgg.test_bean_factory;

/**
 * @author zmddzf
 *
 */
public class Power {
	// 供电状态
	private boolean state;
	
	// set方法
	public void setState(boolean state) {
		this.state = state;
	}
	
	// get方法
	public boolean getState() {
		return state;
	}
}

```

* 创建一个`Disk`类

```java
package com.sgg.test_bean_factory;

/**
 * @author zmddzf
 *
 */
public class Disk {
	// 碟片状态
	private boolean state;
	
	//set方法
	public void setState(boolean state) {
		this.state = state;
	}
	
	//get方法
	public boolean getState() {
		return state;
	}

}
```

* 创建一个`HeadPhone`类

```java
package com.sgg.test_bean_factory;
/**
 * @author zmddzf
 *
 */
public class HeadPhone {
	// 耳机状态
	private boolean state;
	
	//set方法
	public void setState(boolean state) {
		this.state = state;
	}
	
	//get方法
	public boolean getState() {
		return state;
	}
}
```

* 创建`player`类

```java
package com.sgg.test_bean_factory;

public class Player {
	
	// CD播放机的组成单位
	private Power pw;
	private Disk ds;
	private HeadPhone hp;
	
	public void setPw(Power pw) {
		this.pw = pw;
	}
	
	public void setDs(Disk ds) {
		this.ds = ds;
	}
	
	public void setHp(HeadPhone hp) {
		this.hp = hp;
	}
	
	public boolean checkReady() {
		if (pw.getState()) {
			if (ds.getState()) {
				if (hp.getState()) {
					return true;
				}
			}
		}
		return false;
	}

}
```

* 编写application.xml文件

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">
 
    <bean id="power" class="com.sgg.test_bean_factory.Power">
        <property name="state" value="true" />
    </bean>
    
    <bean id="disk" class="com.sgg.test_bean_factory.Disk">
       <property name="state" value="true"></property>
    </bean>
    
    <bean id="headphone" class="com.sgg.test_bean_factory.HeadPhone">
        <property name="state" value="true"></property>
    </bean>
    
    <bean id="player" class="com.sgg.test_bean_factory.Player">
        <property name="pw" ref="power"></property>
        <property name="ds" ref="disk"></property>
        <property name="hp" ref="headphone"></property>
    </bean>
 
</beans>
```

> 这里我们可以看到，Player依赖于Power、Disk、HeadPhone，于是我们在这里写上了`ref` 字段，这其实就是一个典型的依赖注入。

* 编写`App.java`

```java
package com.sgg.test_bean_factory;

import org.springframework.beans.factory.BeanFactory;
import org.springframework.beans.factory.xml.XmlBeanFactory;
import org.springframework.core.io.ClassPathResource;

/**
 * Hello world!
 *
 */
public class App 
{
    public static void main( String[] args )
    {
    	BeanFactory factory = new XmlBeanFactory(new ClassPathResource("application.xml"));
    	Player player = (Player) factory.getBean("player");
    	System.out.println("The state of this player is: " + player.checkReady());
    }
}
```

![image-20200413163441483](.\image\image-20200413163441483.png)

## ApplicationContext容器

* Application Context （Spring 上下文）是 BeanFactory 的子接口
* 增加了企业所需要的功能，如从属性文件中解析文本信息和将时间传递给指定的监听器
* 在org.springframework.context.ApplicationContext interface 接口中定义
* 常用的ApplicationContex接口实现：
  - **FileSystemXmlApplicationContext**：该容器从 XML 文件中加载已被定义的 bean。在这里，你需要提供给构造器 XML 文件的完整路径。
  - **ClassPathXmlApplicationContext**：该容器从 XML 文件中加载已被定义的 bean。在这里，你不需要提供 XML 文件的完整路径，只需正确配置 CLASSPATH 环境变量即可，因为，容器会从 CLASSPATH 中搜索 bean 配置文件。
  - **WebXmlApplicationContext**：该容器会在一个 web 应用程序的范围内加载在 XML 文件中已被定义的 bean。

### 简单案例

> 接上一部分案例，这里使用FileSystemXmlApplicationContext接口实现

* 只需要修改App.java文件即可

```java
package com.sgg.test_bean_factory;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.FileSystemXmlApplicationContext;

/**
 * Hello world!
 *
 */
public class App 
{
    public static void main( String[] args )
    {
    	ApplicationContext factory = new FileSystemXmlApplicationContext("C:\\Users\\zmddzf\\Desktop\\java_code\\test_bean_factory\\src\\main\\resources\\application.xml");  // 写完整路径
    	Player player = (Player) factory.getBean("player");
    	System.out.println("The state of this player is: " + player.checkReady());
    }
}

```

![image-20200413170738502](.\image\image-20200413170738502.png)

## Bean介绍

| 属性                     | 描述                                                         |
| ------------------------ | ------------------------------------------------------------ |
| class                    | 这个属性是强制性的，并且指定用来创建 bean 的 bean 类。       |
| name                     | 这个属性指定唯一的 bean 标识符。在基于 XML 的配置元数据中，可以使用 ID 和/或 name 属性来指定 bean 标识符。 |
| scope                    | 这个属性指定由特定的 bean 定义创建的对象的作用域。           |
| constructor-arg          | 用来注入依赖关系。                                           |
| properties               | 用来注入依赖关系。                                           |
| autowiring mode          | 用来注入依赖关系。                                           |
| lazy-initialization mode | 延迟初始化的 bean 告诉 IoC 容器在它第一次被请求时，而不是在启动时去创建一个 bean 实例。 |
| initialization 方法      | 在 bean 的所有必需的属性被容器设置之后，调用回调方法。       |
| destruction 方法         | 当包含该 bean 的容器被销毁时，使用回调方法。                 |

> `bean` 是一个被实例化，组装，并通过 `Spring IoC` 容器所管理的对象，`bean` 是由用容器提供的配置元数据创建的



### Spring Bean的作用域

| 作用域         | 描述                                                         |
| -------------- | ------------------------------------------------------------ |
| singleton      | 在spring IoC容器仅存在一个Bean实例，Bean以单例方式存在，默认值 |
| prototype      | 每次从容器中调用Bean时，都返回一个新的实例，即每次调用getBean()时，相当于执行newXxxBean() |
| request        | 每次HTTP请求都会创建一个新的Bean，该作用域仅适用于WebApplicationContext环境 |
| session        | 同一个HTTP Session共享一个Bean，不同Session使用不同的Bean，仅适用于WebApplicationContext环境 |
| global-session | 一般用于Portlet应用环境，该运用域仅适用于WebApplicationContext环境 |

* **singleton作用域**

> singleton 是默认的作用域。当一个bean的作用域为Singleton，那么Spring IoC容器中只会存在一个共享的bean实例，并且所有对bean的请求，只要id与该bean定义相匹配，则只会返回bean的同一实例。调用时创建，每次获取到的都是同一个bean对象。

```xml
<!-- A bean definition with singleton scope -->
<bean id="..." class="..." scope="singleton">
    <!-- collaborators and configuration for this bean go here -->
</bean>
```

> 按照上文的例子做一个测试，改变一下电源的状态，再将其传入`player`中，然后重新获取一个`player`的`bean`，检查一下是否接通

```java
package com.sgg.test_bean_factory;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.FileSystemXmlApplicationContext;

/**
 * Hello world!
 *
 */
public class App 
{
    public static void main( String[] args )
    {
    	// 获取配置文件
    	ApplicationContext factory = new FileSystemXmlApplicationContext("C:\\Users\\zmddzf\\Desktop\\java_code\\test_bean_factory\\src\\main\\resources\\application.xml");
    	// 获取player实例
    	Player playerA = (Player) factory.getBean("player");
    	// 检查是否ready
    	System.out.println("The state of this player is: " + playerA.checkReady());
    	// 获取Power实例
    	Power power = (Power) factory.getBean("power");
    	// 将Power状态设为关闭
    	power.setState(false);
    	// 检查是否ready
    	System.out.println("The state of this player is: " + playerA.checkReady());
    	// 将player的电源关闭
       	playerA.setPw(power);
    	// 重新获取一个player实例
    	Player playerB = (Player) factory.getBean("player");
    	// 检查是否ready
    	System.out.println("The state of this player is: " + playerB.checkReady());
    }
}
```

![image-20200416234617833](.\image\image-20200416234617833.png)

* **prototype作用域**

> 当一个bean的作用域为Prototype，表示一个bean定义对应多个对象实例。Prototype作用域的bean会导致在每次对该bean请求（将其注入到另一个bean中，或者以程序的方式调用容器的getBean()方法）时都会创建一个新的bean实例。  
>
> Prototype是原型类型，它在我们创建容器的时候并没有实例化，而是当我们获取bean的时候才会去创建一个对象，而且我们每次获取到的对象**都不是同一个对象**。

这里我们修改一下`application.xml`做一下测试，将`powe`r与`player`的`scope`都改为`prototype`

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">
 
    <bean id="power" class="com.sgg.test_bean_factory.Power" scope="prototype">
        <property name="state" value="true" />
    </bean>
    
    <bean id="disk" class="com.sgg.test_bean_factory.Disk">
       <property name="state" value="true"></property>
    </bean>
    
    <bean id="headphone" class="com.sgg.test_bean_factory.HeadPhone">
        <property name="state" value="true"></property>
    </bean>
    
    <bean id="player" class="com.sgg.test_bean_factory.Player" scope="prototype">
        <property name="pw" ref="power"></property>
        <property name="ds" ref="disk"></property>
        <property name="hp" ref="headphone"></property>
    </bean>
 
</beans>
```

![image-20200416234432144](.\image\image-20200416234432144.png)

对比两次结果，你发现了什么？

### Spring 生命周期

> 理解 Spring bean 的生命周期很容易。当一个 bean 被实例化时，它可能需要执行一些初始化使它转换成可用状态。同样，当 bean 不再需要，并且从容器中移除时，可能需要做一些清除工作。

> 尽管还有一些在 Bean 实例化和销毁之间发生的活动，但是本章将只讨论两个重要的生命周期回调方法，它们在 bean 的初始化和销毁的时候是必需的。

> 为了定义安装和拆卸一个 bean，我们只要声明带有 **init-method** 和/或 **destroy-method** 参数的 。init-method 属性指定一个方法，在实例化 bean 时，立即调用该方法。同样，destroy-method 指定一个方法，只有从容器中移除 bean 之后，才能调用该方法。

> Bean的生命周期可以表达为：Bean的定义——Bean的初始化——Bean的使用——Bean的销毁

* **初始化回调**

*org.springframework.beans.factory.InitializingBean* 接口指定一个单一的方法：

```java
void afterPropertiesSet() throws Exception;
```

因此，你可以简单地实现上述接口和初始化工作可以在 afterPropertiesSet() 方法中执行，如下所示：

```java
public class ExampleBean implements InitializingBean {
   public void afterPropertiesSet() {
      // do some initialization work
   }
}
```

> 在基于 XML 的配置元数据的情况下，你可以使用 **init-method** 属性来指定带有 void 无参数方法的名称。例如：

```xml
<bean id="exampleBean" 
         class="examples.ExampleBean" init-method="init"/>
```

> 下面是类的定义：

```java
public class ExampleBean {
   public void init() {
      // do some initialization work
   }
}
```

* **销毁回调**

*org.springframework.beans.factory.DisposableBean* 接口指定一个单一的方法：

```java
void destroy() throws Exception;
```

> 因此，可以简单地实现上述接口并且结束工作可以在 destroy() 方法中执行，如下所示：

```java
public class ExampleBean implements DisposableBean {
   public void destroy() {
      // do some destruction work
   }
}
```

> 在基于 XML 的配置元数据的情况下，你可以使用 **destroy-method** 属性来指定带有 void 无参数方法的名称。例如：

```xml
<bean id="exampleBean"
         class="examples.ExampleBean" destroy-method="destroy"/>
```

> 下面是类的定义：

```java
public class ExampleBean {
   public void destroy() {
      // do some destruction work
   }
}
```

> 如果你在非 web 应用程序环境中使用 Spring 的 IoC 容器；例如在丰富的客户端桌面环境中；那么在 JVM 中你要注册关闭 hook。这样做可以确保正常关闭，为了让所有的资源都被释放，可以在单个 beans 上调用 destroy 方法。

> 建议你不要使用 InitializingBean 或者 DisposableBean 的回调方法，因为 XML 配置在命名方法上提供了极大的灵活性。

* **默认初始化和销毁方法**

> 如果具有相同名称的初始化或者销毁方法的 Bean，那么不需要在每一个 bean 上声明**初始化方法**和**销毁方法**。框架使用 元素中的 **default-init-method** 和 **default-destroy-method** 属性提供了灵活地配置这种情况，如下所示：

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans-3.0.xsd"
    default-init-method="init" 
    default-destroy-method="destroy">

   <bean id="..." class="...">
       <!-- collaborators and configuration for this bean go here -->
   </bean>

</beans>
```

### Bean 后置处理器

> Bean 后置处理器允许在调用初始化方法前后对 Bean 进行额外的处理。
>
> **BeanPostProcessor** 接口定义回调方法，可以实现该方法来提供自己的实例化逻辑，依赖解析逻辑等。也可以在 Spring 容器通过插入一个或多个 BeanPostProcessor 的实现来完成实例化，配置和初始化一个bean之后实现一些自定义逻辑回调方法。
>
> 可以配置多个 BeanPostProcessor 接口，通过设置 BeanPostProcessor 实现的 **Ordered** 接口提供的 **order** 属性来控制这些 BeanPostProcessor 接口的执行顺序。
>
> BeanPostProcessor 可以对 bean（或对象）实例进行操作，这意味着 Spring IoC 容器实例化一个 bean 实例，然后 BeanPostProcessor 接口进行它们的工作。
>
> **ApplicationContext** 会自动检测由 **BeanPostProcessor** 接口的实现定义的 bean，注册这些 bean 为后置处理器，然后通过在容器中创建 bean，在适当的时候调用它。

* `HelloWorld.java`

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
	
	public void init() {
		System.out.println("The Object is Created!");
	}
	
	public void destroy() {
		System.out.println("The Object is Destroyed!");
	}
}
```

* `initHelloWorld.java`

```java
package com.sgg.demo;

import org.springframework.beans.BeansException;
import org.springframework.beans.factory.config.BeanPostProcessor;

public class InitHelloWorld implements BeanPostProcessor {
	public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
	      System.out.println("BeforeInitialization : " + beanName);
	      return bean;  // you can return any other object as well
	}
	
   public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
	      System.out.println("AfterInitialization : " + beanName);
	      return bean;  // you can return any other object as well
	   }
}
```

* `SpringBeans.java`

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">
 
    <bean id="helloBean" class="com.sgg.demo.HelloWorld" 
    	init-method="init" destroy-method="destroy">
        <property name="name" value="dzf415" />
    </bean>
    <bean class="com.sgg.demo.InitHelloWorld" />

</beans>
```

* `App.java`

```java
package com.sgg.demo;

import org.springframework.context.support.AbstractApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class App {
 
	public static void main(String[] args) {
		AbstractApplicationContext context = new ClassPathXmlApplicationContext("SpringBeans.xml");
 
		HelloWorld obj = (HelloWorld) context.getBean("helloBean");
		obj.printHello();
		context.registerShutdownHook();		
	}
}
```

![image-20200417012231724](.\image\image-20200417012231724.png)

### Bean 定义继承

> 子 bean 的定义继承父定义的配置数据。子定义可以根据需要重写一些值，或者添加其他值。
>
> Spring Bean 定义的继承与 Java 类的继承无关，但是继承的概念是一样的。你可以定义一个父 bean 的定义作为模板和其他子 bean 就可以从父 bean 中继承所需的配置。
>
> 当你使用基于 XML 的配置元数据时，通过使用父属性，指定父 bean 作为该属性的值来表明子 bean 的定义。

> 下面是配置文件 **Beans.xml**，在该配置文件中我们定义有两个属性 *message1* 和 *message2* 的 “helloWorld” bean。然后，使用 **parent** 属性把 “helloIndia” bean 定义为 “helloWorld” bean 的孩子。这个子 bean 继承 *message2* 的属性，重写 *message1* 的属性，并且引入一个属性 *message3*。

```xml
<?xml version="1.0" encoding="UTF-8"?>

<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">

   <bean id="helloWorld" class="com.tutorialspoint.HelloWorld">
      <property name="message1" value="Hello World!"/>
      <property name="message2" value="Hello Second World!"/>
   </bean>

   <bean id="helloIndia" class="com.tutorialspoint.HelloIndia" parent="helloWorld">
      <property name="message1" value="Hello India!"/>
      <property name="message3" value="Namaste India!"/>
   </bean>

</beans>
```

这里是 **HelloWorld.java** 文件的内容：

```java
package com.tutorialspoint;
public class HelloWorld {
   private String message1;
   private String message2;
   public void setMessage1(String message){
      this.message1  = message;
   }
   public void setMessage2(String message){
      this.message2  = message;
   }
   public void getMessage1(){
      System.out.println("World Message1 : " + message1);
   }
   public void getMessage2(){
      System.out.println("World Message2 : " + message2);
   }
}
```

这里是 **HelloIndia.java** 文件的内容：

```java
package com.tutorialspoint;

public class HelloIndia {
   private String message1;
   private String message2;
   private String message3;

   public void setMessage1(String message){
      this.message1  = message;
   }

   public void setMessage2(String message){
      this.message2  = message;
   }

   public void setMessage3(String message){
      this.message3  = message;
   }

   public void getMessage1(){
      System.out.println("India Message1 : " + message1);
   }

   public void getMessage2(){
      System.out.println("India Message2 : " + message2);
   }

   public void getMessage3(){
      System.out.println("India Message3 : " + message3);
   }
}
```

下面是 **MainApp.java** 文件的内容：

```java
package com.tutorialspoint;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class MainApp {
   public static void main(String[] args) {
      ApplicationContext context = new ClassPathXmlApplicationContext("Beans.xml");

      HelloWorld objA = (HelloWorld) context.getBean("helloWorld");

      objA.getMessage1();
      objA.getMessage2();

      HelloIndia objB = (HelloIndia) context.getBean("helloIndia");
      objB.getMessage1();
      objB.getMessage2();
      objB.getMessage3();
   }
}
```

一旦你创建源代码和 bean 配置文件完成后，我们就可以运行该应用程序。如果你的应用程序一切都正常，将输出以下信息：

```
World Message1 : Hello World!
World Message2 : Hello Second World!
India Message1 : Hello India!
India Message2 : Hello Second World!
India Message3 : Namaste India!
```

在这里你可以观察到，我们创建 “helloIndia” bean 的同时并没有传递 message2，但是由于 Bean 定义的继承，所以它传递了 message2。

## Bean 定义模板

你可以创建一个 Bean 定义模板，不需要花太多功夫它就可以被其他子 bean 定义使用。在定义一个 Bean 定义模板时，你不应该指定**类**的属性，而应该指定带 **true** 值的**抽象**属性，如下所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>

<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">

   <bean id="beanTeamplate" abstract="true">
      <property name="message1" value="Hello World!"/>
      <property name="message2" value="Hello Second World!"/>
      <property name="message3" value="Namaste India!"/>
   </bean>

   <bean id="helloIndia" class="com.tutorialspoint.HelloIndia" parent="beanTeamplate">
      <property name="message1" value="Hello India!"/>
      <property name="message3" value="Namaste India!"/>
   </bean>

</beans>
```

父 bean 自身不能被实例化，因为它是不完整的，而且它也被明确地标记为抽象的。当一个定义是抽象的，它仅仅作为一个纯粹的模板 bean 定义来使用的，充当子定义的父定义使用。