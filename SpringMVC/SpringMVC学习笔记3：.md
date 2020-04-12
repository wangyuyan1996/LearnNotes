# 学习笔记3：第一个SpringMVC应用

在上一篇笔记里，我们已经搭建了第一个SpringMVC应用，并在web.xml中部署了DispatcherServlet，并在tomcat上显示出了"Hello World!"。本篇在此基础上继续完善该应用。

## 0 编写Web应用首页

在程序的`/src/main/webapp/`下有个index.jsp文件，此即为我们的Web应用首页文件，编写代码如下：

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
    
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
    未注册的用户，请<a href="${pageContext.request.contextPath }/register"> 注册</a>！
    <br/>
    已注册的用户，去<a href="${pageContext.request.contextPath }/login"> 登录</a>！
</body>
</html>
```

在这里，主要是要实现一个注册登陆的效果，并且插入了超链接，显示文字为“登陆”“注册”，用于跳转到相应页面。



## 1 创建Controller类

在 src 目录下创建 controller 包，并在该包中创建 RegisterController 和 LoginController 两个传统风格的控制器类（实现了 Controller 接口），分别处理首页中“注册”和“登录”超链接的请求。

在进行这一步之前，更新一下项目依赖，打开pom.xml，加入以下代码：

```xml
  <!--   统一版本号 -->
  <properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<spring.version>4.1.7.RELEASE</spring.version>
		<mybatis.version>3.4.5</mybatis.version>
  </properties>


  
  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>
    <!-- spring依赖 -->
	<!-- 核心包 -->
	<dependency>
		<groupId>org.springframework</groupId>
		<artifactId>spring-core</artifactId>
		<version>${spring.version}</version>
	</dependency>
		
	<!-- pring IOC的基础实现，包含访问配置文件、创建和管理bean等 -->
	<dependency>
		<groupId>org.springframework</groupId>
		<artifactId>spring-beans</artifactId>
		<version>${spring.version}</version>
	</dependency>
<!-- 这个jar文件为Spring核心提供了大量扩展。可以找到使用Spring ApplicationContext特性时所需的全部类，JDNI所需的全部类，UI方面的用来与模板（Templating）引擎如Velocity、FreeMarker、JasperReports集成的类，以及校验Validation方面的相关类。 -->
	<!-- Spring 扩展服务 -->
	<dependency>
		<groupId>org.springframework</groupId>
		<artifactId>spring-context</artifactId>
		<version>${spring.version}</version>
	</dependency>
		
<!-- 为JDBC、Hibernate、JDO、JPA等提供的一致的声明式和编程式事务管理 -->
	<dependency>
		<groupId>org.springframework</groupId>
		<artifactId>spring-tx</artifactId>
		<version>${spring.version}</version>
	</dependency>
<!-- 这个jar文件包含在应用中使用Spring的AOP特性时所需的类。使用基于AOP的Spring特性，如声明型事务管理（Declarative Transaction Management），也要在应用里包含这个jar包。 -->
	<dependency>
		<groupId>org.springframework</groupId>
		<artifactId>spring-aop</artifactId>
		<version>${spring.version}</version>
	</dependency>
		
<!-- 提供对AspectJ的支持，以便可以方便的将面向方面的功能集成进IDE中，比如Eclipse AJDT。  外部依赖。   -->
	<dependency>
		<groupId>org.springframework</groupId>
		<artifactId>spring-aspects</artifactId>
		<version>${spring.version}</version>
	</dependency>
		
<!-- springmvc依赖 -->
<!-- 这个jar文件包含Spring MVC框架相关的所有类。包含国际化、标签、Theme、视图展现的FreeMarker、JasperReports、Tiles、Velocity、XSLT相关类。当然，如果你的应用使用了独立的MVC框架，则无需这个JAR文件里的任何类。 -->
	<dependency>
		<groupId>org.springframework</groupId>
		<artifactId>spring-webmvc</artifactId>
		<version>${spring.version}</version>
	</dependency>
<!-- web依赖 -->
	<dependency>
		<groupId>org.springframework</groupId>
		<artifactId>spring-web</artifactId>
		<version>${spring.version}</version>
	</dependency>
		
<!-- jdbc支持包 -->
	<dependency>
		<groupId>org.springframework</groupId>
		<artifactId>spring-jdbc</artifactId>
		<version>${spring.version}</version>
	</dependency>
		
	 <!--mysql驱动包-->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.35</version>
    </dependency>
        
    <!-- mybatis核心包 -->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>${mybatis.version}</version>
    </dependency>
		
<!-- 添加mybatis与Spring整合的核心包 -->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis-spring</artifactId>
        <version>1.3.1</version>
    </dependency>
<!-- JSON-lib解析json字符串-->
	<dependency>
		<groupId>net.sf.json-lib</groupId>
		<artifactId>json-lib</artifactId>
		<version>2.4</version>
		<classifier>jdk15</classifier>
	</dependency>
               
<!-- servlet相关接口-->
	<dependency>
		<groupId>javax.servlet</groupId>
		<artifactId>javax.servlet-api</artifactId>
		<version>3.1.0</version>
		<scope>provided</scope>
	</dependency>
<!-- jstl标签库 -->
	<dependency>  
		<groupId>javax.servlet</groupId>  
		<artifactId>jstl</artifactId>  
		<version>1.2</version>  
 		<scope>runtime</scope>  
	</dependency> 
        
        <!-- 日志文件 -->
	<dependency>
		<groupId>log4j</groupId>
		<artifactId>log4j</artifactId>
		<version>1.2.17</version>
	</dependency>


  </dependencies>
  <build>
    <finalName>hello_world</finalName>
  </build>
</project>
```



RegisterController：

```java
package controller;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import org.springframework.web.servlet.ModelAndView;
import org.springframework.web.servlet.mvc.Controller;

public class RegisterController implements Controller {
    public ModelAndView handleRequest(HttpServletRequest arg0,
            HttpServletResponse arg1) throws Exception {
        return new ModelAndView("/WEB-INF/jsp/register.jsp");
    }
}
```

LoginController：

```java
package controller;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import org.springframework.web.servlet.ModelAndView;
import org.springframework.web.servlet.mvc.Controller;

public class LoginController implements Controller {
    public ModelAndView handleRequest(HttpServletRequest arg0,
            HttpServletResponse arg1) throws Exception {
        return new ModelAndView("/WEB-INF/jsp/login.jsp");
    }
}
```

未完待续...