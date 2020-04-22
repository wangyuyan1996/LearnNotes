# SpringBoot简介&项目创建

## 0 SpringBoot简介

这里引用一段来简单介绍：

>Spring 框架就像一个家族，有众多衍生产品例如 boot、security、jpa等等。但他们的基础都是Spring 的 ioc和 aop ioc 提供了依赖注入的容器 aop ，解决了面向横切面的编程，然后在此两者的基础上实现了其他延伸产品的高级功能。Spring MVC是基于 Servlet 的一个 MVC 框架 主要解决 WEB 开发的问题，因为 Spring 的配置非常复杂，各种XML、 JavaConfig、hin处理起来比较繁琐。于是为了简化开发者的使用，从而创造性地推出了Spring boot，约定优于配置，简化了spring的配置流程。
>
>说得更简便一些：Spring 最初利用“工厂模式”（DI）和“代理模式”（AOP）解耦应用组件。大家觉得挺好用，于是按照这种模式搞了一个 MVC框架（一些用Spring 解耦的组件），用开发 web 应用（ SpringMVC ）。然后有发现每次开发都写很多样板代码，为了简化工作流程，于是开发出了一些“懒人整合包”（starter），这套就是 Spring Boot。
>
>链接：https://www.zhihu.com/question/64671972/answer/223383505
>来源：知乎

所以简单来说，SpringBoot让Spring应用配置更简单，更轻量化，使用SpringBoot来开发有以下优点：

- 为所有Spring开发者更快的入门
- 开箱即用，提供各种默认配置来简化项目配置
- 内嵌式容器简化Web项目
- 没有冗余代码生成和XML配置的要求



## 1 创建SpringBoot项目

创建SpringBoot可以使用[Spring Initializr页面](https://start.spring.io/)来创建好压缩包后在本地解压，再从IDE导入项目。

也可以直接在IDE里创建好Maven项目后添加SpringBoot的依赖。

这里主要介绍第二种方法。

### 1.0 Maven下载配置&创建Maven项目

Maven的下载及配置在本人的"SpringMVC学习笔记1:环境.md"中有讲解，在此不多赘述。

主要介绍如何在Eclipse中创建Maven项目。

创建一个Maven项目：`File->New->Other->Maven Project->Next->Next`，此时进入选择Maven Archetype界面，如果界面是空白的一般稍等几分钟加载就好，Eclipse主窗口右下角会显示`Retrieving Archetypes`，这是因为Maven需要到http://repo1.maven.org/maven2/archetype-catalog.xml加载archetypes信息。

这里推荐把archetype-catalog.xml下载到本地，官网地址不允许直接浏览器访问，可以到http://insecure.repo1.maven.org/maven2/archetype-catalog.xml下载，放到自己的Maven文件夹里，然后到`Eclipse->Preferences->Maven->Archetypes->Add Local Catalog`，选择刚下载的archetype-catalog.xml就好。

回到创建项目，到选择Maven Archetype界面时，选择`maven-archetype-webapp`，点`Next`，输入以下信息：`Group Id: 通常为公司域名反过来，可以随便输；Artifact Id: 项目名称；其他: 默认`，`Finish`，创建完成。

这里介绍一下Archetype：

> Archetype 是一个 Maven 项目模板工具包。原型被定义为原始模式或模型，从中创建所有其他相同类型的东西。这些名称适合我们尝试提供一个系统，该系统提供生成Maven项目的一致方法。Archetype 将帮助作者为用户创建 Maven 项目模板，并为用户提供生成这些项目模板的参数化版本的方法。-- [摘自官网](https://maven.apache.org/archetype/index.html)

此时项目src会报错，原因是找不到HttpServlet类，可以通过导入tomcat到工作目录解决：`右键项目名称->Build Path->Configure Build Path->Java Build Path->Libraries->Add Library->Server Runtime->Next`，选择自己配置的tomcat即可，更新设置后就创建好项目了。

PS：需要自行配置一下tomcat。相关配置在本人`SpringMVC`笔记内也有讲，欢迎查阅。



### 1.1 Maven构建SpringBoot项目

在创建好的Maven web-app的pom.xml文件添加依赖项，完整代码如下：

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.1.5.RELEASE</version>
  </parent>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.7</maven.compiler.source>
    <maven.compiler.target>1.7</maven.compiler.target>
  </properties>

  <dependencies>
  	<!-- 提供了web模块的依赖  -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    <!-- 热部署  -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <scope>provided</scope>
        <optional>true</optional>
    </dependency>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        </dependency>
  	
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <scope>test</scope>
    </dependency>
  </dependencies>
```



右键项目名，`Maven->Update Project`，勾选上`Force Update of Snapshots/Releases`，更新项目后会自动下载依赖项。

到此就在Eclipse中通过Maven创建好了一个SpringBoot项目。