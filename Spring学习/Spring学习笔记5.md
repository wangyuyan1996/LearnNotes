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