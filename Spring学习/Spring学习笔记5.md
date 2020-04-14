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

