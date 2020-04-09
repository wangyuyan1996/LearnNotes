# Spring学习笔记2

> 作者：DZF
> 邮箱：872573678@qq.com



## 简介

* 本次笔记主要记录如何安装Spring框架
* 默认读者已成功安装了java与eclipse
* 默认读者已具备java编程基础



## 1. 安装springsource-tool-suite

* **查看eclipse版本**

> help--About Eclipse

<img src="./image/image-20200405011707594.png" alt="image-20200405011707594" style="zoom: 33%;" />

* **使用eclipse安装对应的springsource-tool-suite**

> help--Install New Software

<img src=".\image\image-20200405011855871.png" alt="image-20200405011855871" style="zoom:33%;" />

* **选择对应版本下载**

> 链接http://dist.springsource.com/release/TOOLS/update/xxx/
>
> 其中xxx为eclipse的版本号

<img src=".\image\image-20200405012255708.png" alt="image-20200405012255708" style="zoom:33%;" />

> 安装对应的插件

<img src=".\image\image-20200405011707595.png" alt="img" style="zoom: 50%;" />



## 2. 下载Spring framework

* **选择合适的版本下载**

> 链接：https://repo.spring.io/release/org/springframework/spring/5.2.5.RELEASE/

![image-20200405013208068](.\image\image-20200405013208068.png)

* **下载完解压framework**

![image-20200405013327393](.\image\image-20200405013327393.png)

## 3. 下载Common Logging

![img](.\image\image-20200405011707590.png)

## 4. 建一个Spring工程

* **新建java工程**

<img src=".\image\image-20200405013909798.png" alt="image-20200405013909798" style="zoom:33%;" />

* **右击刚才创建的项目，"New"-->"Folder"新建文件夹，并命名为“lib”,"Finish"**

<img src=".\image\image-20200405014439967.png" alt="image-20200405014439967" style="zoom:33%;" />

* **把几个jar添加进lib中**

> 来自解压后的framework与common logging

<img src=".\image\image-20200405014858209.png" alt="image-20200405014858209" style="zoom:33%;" />

<img src=".\image\image-20200405015037727.png" alt="image-20200405015037727" style="zoom:33%;" />

> 从eclipse粘贴进lib

<img src=".\image\image-20200405015339465.png" alt="image-20200405015339465" style="zoom:33%;" />

* **然后选中5个jar包，右键--"bulid path"--"add to build path"**

<img src=".\image\image-20200405015443488.png" alt="image-20200405015443488" style="zoom:33%;" />