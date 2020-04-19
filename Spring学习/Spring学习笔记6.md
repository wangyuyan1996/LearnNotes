# Spring学习笔记6

> 作者：DZF  
>
> 邮箱：872573678@qq.com

-----

> **本次学习笔记主要介绍Spring的依赖注入**

## 基于构造函数的注入

> 使用有参构造器，在bean中使用`constructor-arg`实现依赖注入

```java
package com.sgg.ditest;

public class Student {
	
	private String std_no;
	private String std_name;
	private String std_school;
	
	public Student(String std_no, String std_name, String std_school) {
		this.std_no = std_no;
		this.std_name = std_name;
		this.std_school = std_school;
	}
	
	public String studentString() {
		String s;
		s = "{std_no:" + std_no + ",std_name:" + std_name + ",std_school:" +std_school + "}";
		return s;	
	}
}

```

```java
package com.sgg.ditest;

public class Printer {
	
	private Student std;
	
	public Printer(Student std) {
		this.std = std;
	}
	
	public void getStendentInfo() {
		System.out.println(std.studentString());
	}
}
```

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">

	<bean id="student" class="com.sgg.ditest.Student">
		<constructor-arg type="java.lang.String" value="12345678"/>
    	<constructor-arg type="java.lang.String" value="丁卓非"/>
    	<constructor-arg type="java.lang.String" value="经济与工商管理学院"/>
	</bean>
	
	<bean id="printer" class="com.sgg.ditest.Printer">
		<constructor-arg ref="student"/>
	</bean>

</beans>
```

```java
package com.sgg.ditest;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

/**
 * Hello world!
 *
 */
public class App 
{
    public static void main( String[] args )
    {
        ApplicationContext context = new ClassPathXmlApplicationContext("application.xml");
        Printer printer = (Printer) context.getBean("printer");
        printer.getStendentInfo();
    }
}
```

## 基于设值函数的依赖注入

> 使用`bean`中`property`的`ref`字段，配合setter实现依赖注入。此时需要无参构造器（Java默认存在无参构造器）。

```java
package com.sgg.ditest;

public class Printer {
	
	private Student std;

	public void setStd(Student std) {
		this.std = std;
	}
	
	public void getStendentInfo() {
		System.out.println(std.studentString());
	}
}
```

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">

	<bean id="student" class="com.sgg.ditest.Student">
		<constructor-arg type="java.lang.String" value="12345678"/>
    	<constructor-arg type="java.lang.String" value="丁卓非"/>
    	<constructor-arg type="java.lang.String" value="经济与工商管理学院"/>
	</bean>
	<bean id="printer" class="com.sgg.ditest.Printer">
		<property name="std" ref="student"></property>
	</bean>
</beans>
```

## 注入内部bean

> 可以在`bean`的内部定义其他的`bean`，接上文案例进行展示

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">
	<bean id="printer" class="com.sgg.ditest.Printer">
		<property name="std">
			<bean id="student" class="com.sgg.ditest.Student">
				<constructor-arg type="java.lang.String" value="12345678"/>
		    	<constructor-arg type="java.lang.String" value="丁卓非"/>
		    	<constructor-arg type="java.lang.String" value="经济与工商管理学院"/>
			</bean>
		</property>
	</bean>
</beans>
```

## 注入集合

| 元素      | 描述                                                        |
| --------- | ----------------------------------------------------------- |
| `<list>`  | 它有助于连线，如注入一列值，允许重复。                      |
| `<set>`   | 它有助于连线一组值，但不能重复。                            |
| `<map>`   | 它可以用来注入名称-值对的集合，其中名称和值可以是任何类型。 |
| `<props>` | 它可以用来注入名称-值对的集合，其中名称和值都是字符串类型。 |

> JavaCollection.java

```java
package com.sgg.ditest;

import java.util.List;
import java.util.Map;
import java.util.Properties;
import java.util.Set;

public class JavaCollection {
   List addressList;
   Set  addressSet;
   Map  addressMap;
   Properties addressProp;
   
   // a setter method to set List
   public void setAddressList(List addressList) {
      this.addressList = addressList;
   }
   // prints and returns all the elements of the list.
   public List getAddressList() {
      System.out.println("List Elements :"  + addressList);
      return addressList;
   }
   // a setter method to set Set
   public void setAddressSet(Set addressSet) {
      this.addressSet = addressSet;
   }
   // prints and returns all the elements of the Set.
   public Set getAddressSet() {
      System.out.println("Set Elements :"  + addressSet);
      return addressSet;
   }
   // a setter method to set Map
   public void setAddressMap(Map addressMap) {
      this.addressMap = addressMap;
   }  
   // prints and returns all the elements of the Map.
   public Map getAddressMap() {
      System.out.println("Map Elements :"  + addressMap);
      return addressMap;
   }
   // a setter method to set Property
   public void setAddressProp(Properties addressProp) {
      this.addressProp = addressProp;
   } 
   // prints and returns all the elements of the Property.
   public Properties getAddressProp() {
      System.out.println("Property Elements :"  + addressProp);
      return addressProp;
   }
}
```

> application.xml中加入bean

```xml
	<bean id="javaCollection" class="com.sgg.ditest.JavaCollection">

      <!-- results in a setAddressList(java.util.List) call -->
      <property name="addressList">
         <list>
            <value>INDIA</value>
            <value>Pakistan</value>
            <value>USA</value>
            <value>USA</value>
         </list>
      </property>

      <!-- results in a setAddressSet(java.util.Set) call -->
      <property name="addressSet">
         <set>
            <value>INDIA</value>
            <value>Pakistan</value>
            <value>USA</value>
            <value>USA</value>
        </set>
      </property>

      <!-- results in a setAddressMap(java.util.Map) call -->
      <property name="addressMap">
         <map>
            <entry key="1" value="INDIA"/>
            <entry key="2" value="Pakistan"/>
            <entry key="3" value="USA"/>
            <entry key="4" value="USA"/>
         </map>
      </property>

      <!-- results in a setAddressProp(java.util.Properties) call -->
      <property name="addressProp">
         <props>
            <prop key="one">INDIA</prop>
            <prop key="two">Pakistan</prop>
            <prop key="three">USA</prop>
            <prop key="four">USA</prop>
         </props>
      </property>

   </bean>
```

> App.java

```java
package com.sgg.ditest;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

/**
 * Hello world!
 *
 */
public class App 
{
    public static void main( String[] args )
    {
        ApplicationContext context = new ClassPathXmlApplicationContext("application.xml");
        JavaCollection jc=(JavaCollection)context.getBean("javaCollection");
        jc.getAddressList();
        jc.getAddressSet();
        jc.getAddressMap();
        jc.getAddressProp();
    }
}

```

