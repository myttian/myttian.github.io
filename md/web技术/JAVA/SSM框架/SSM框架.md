## 1、SSM框架

[ADB 开启 USB调试后，无法自动弹出调试授权窗口的解决方法](https://blog.csdn.net/weixin_48591974/article/details/128849023)  [索尼Xperia XZ1 USB驱动程序](https://www.androidusbdrivers.com/sony-xperia-xz1-usb-drivers/#how_to_install_google_android_drivers)   [黑阈激活](https://www.jianshu.com/p/23f5b2c7a7df)
`adb -d shell sh /data/data/me.piebridge.brevent/brevent.sh`

[bat批处理执行](http://www.manongjc.com/detail/64-atxkapjpkvphxyt.html)  [bat批处理](https://www.cnblogs.com/wztshine/p/16295775.html) [bat批处理](https://www.jb51.net/jiaoben/286225kya.htm)  [BAT脚本](https://www.jb51.net/article/49627.htm?tdsourcetag=s_pcqq_aiomsg) [windows bat脚本](https://www.jb51.net/article/266580.htm) [html在线手册](http://shouce.jb51.net/)

[JAVA框架的层级](https://blog.csdn.net/m0_62314761/article/details/127282881)  [MFC的类层次结构图](https://blog.51cto.com/u_8081755/3356400) [java类层次结构图](https://blog.51cto.com/topic/javaleicengcijiegoutu.html)  [JAVA基础-层级结构](https://www.cnblogs.com/qiyiyifan/p/16779608.html)

### 1、MyBatis

[千锋教育_MyBatis](https://www.bilibili.com/video/BV19t4y1X7kw/?spm_id_from=333.999.0.0&vd_source=7346303e5e18677d7261c2c0c109ecfd)  [狂神说Java-Mybatis](https://www.bilibili.com/video/BV1NE411Q7Nx/?vd_source=7346303e5e18677d7261c2c0c109ecfd)  [mybatis学习笔记 ](https://www.cnblogs.com/wu-wang/p/14836122.html)  [MyBatis---学习笔记](https://blog.51cto.com/u_15127558/4266525)  [持久化与持久层](https://www.cnblogs.com/CnFallTime/p/16023178.html)  [mybatis](https://cloud.tencent.com/developer/article/1748417)  [快速搭建第一个Mybatis程序](https://www.huoban.com/news/post/17730.html) 

> 1. 持久化：将程序的数据在持久状态和瞬时状态转化的过程
> 2. 持久层：完成持久化工作的代码块
> 3. 第一个Mybatis程序
>    1. pom.xml中导入maven依赖
>    2. 核心配置文件：resources下创建mybatis-config.xml



### 2、Spring

[狂神SSM教程](https://www.kuangstudy.com/zl/ssm#1381882854652260353)   [Spring5最新完整教程IDEA](https://www.bilibili.com/video/BV1WE411d7Dv/?vd_source=7346303e5e18677d7261c2c0c109ecfd)   [由Rod Johnson创建的一个开源框架](https://baike.baidu.com/item/spring/85061?fr=aladdin)   [Spring5学习笔记  ](https://www.cnblogs.com/wu-wang/p/14902100.html)
[spring框架](https://baike.baidu.com/item/spring框架/2853288?fr=aladdin)  [spring](https://baike.baidu.com/item/spring/85061?fr=aladdin) [SSM 框架集](https://baike.baidu.com/item/SSM/18801167?fr=aladdin)  [Spring Framework 2.5 开发参考手册](http://shouce.jb51.net/spring/)
AOP：[AOP理解](https://blog.csdn.net/qq_42176665/article/details/128006114)   [AOP理解](https://www.cnblogs.com/Sweetp/p/16615568.html)  [读懂 AOP](https://www.jianshu.com/p/0799aa19ada1)  [学习笔记](https://www.bilibili.com/read/cv8013835)  [Spring 笔记](https://blog.csdn.net/q12584154/article/details/122287796)

> 1. Spring： Spring   FrameWork，Spring框架
>    1. 针对bean的生命周期进行管理的轻量级容器
>    2. Spring框架主要由七部分组成，分别是 Spring Core、 Spring AOP、 Spring ORM、 Spring DAO、Spring Context、 Spring Web和 Spring Web MVC
>    3. Spring是一个轻量级的[控制反转](https://baike.baidu.com/item/控制反转/1158025?fromModule=lemma_inlink)(IoC)和面向切面(AOP)的容器框架
>    4. spring理念：使现有的技术更加容易使用，本身是一个大杂烩，整合了现有的技术框架； SSH、SSM
> 2. Spring Boot 
>    1. 一个快速脚手架，可以基于Spring Boot 快速开发单个微服务
>    2. 学Spring Boot前提，要完全掌握Spring、SpringMVC
> 3. Spring Cloud
>    1. 基于Spring Boot实现的
>    2. Spring Boot专注于快速、方便集成的单个微服务个体，Spring Cloud关注全局的服务治理框架
>    3. Spring Boot使用了约束优于配置的理念，很多集成方案已经帮你选择好了，能不配置就不配置 , Spring Cloud很大的一部分是基于Spring Boot来实现，Spring Boot可以离开Spring Cloud独立使用开发项目，但是Spring Cloud离不开Spring Boot，属于依赖的关系
>    4. SpringBoot在SpringClound中起到了承上启下的作用，如果要学习SpringCloud必须要学习SpringBoot
> 4. IOC
>    1. **控制反转IoC(Inversion of Control)，是一种设计思想，DI(依赖注入)是实现IoC的一种方法**
>    2. IoC是Spring框架的核心内容，使用多种方式完美的实现了IoC，可以使用XML配置，也可以使用注解，新版本的Spring也可以零配置实现IoC
>       1. 构造器注入、依赖注入_set
> 5. 使用Spring来创建对象，在Spring中这些都成为Bean
> 6. 依赖注入
>    1. 依赖 : Bean对象的创建依赖于容器 
>    2. 注入 : bean对象的所有属性，由容器注入。  Bean对象所依赖的资源 , 由容器来设置和装配 

| ![]() | ![]() |
| ----- | ----- |



### 3、SpringMVC

[SpringMVC](https://blog.csdn.net/weixin_48426115/article/details/126995442)   [Web框架](https://so.csdn.net/so/search?q=Web框架&spm=1001.2101.3001.7020)  [SpringMVC](https://www.bilibili.com/video/BV1aE41167Tu/?vd_source=7346303e5e18677d7261c2c0c109ecfd)    [SpringMVC执行原理](https://www.cnblogs.com/wu-wang/p/14856280.html)  [SpringMVC](https://www.cnblogs.com/XiaoMaGuai/p/16172814.html)  

> 1. SpringMVC：spring帮我们做三层架构， Spring MVC是Spring Framework的一部分，是基于Java实现MVC的轻量级
>    1. spring的web框架围绕[DispatcherServlet](https://so.csdn.net/so/search?q=DispatcherServlet&spm=1001.2101.3001.7020)【调度servlet】设计

## 2、SpringBoot

[SpringBoot学习笔记](https://www.cnblogs.com/yamiya/p/12452657.html)  [SpringBoot入门](https://bbs.huaweicloud.com/blogs/384618)    [初探SpringBoot ](https://www.cnblogs.com/CHENFANgY/p/13599097.html)  [人人都是接口开发大师](http://www.taodudu.cc/news/show-4854116.html?action=onClick)  [详细文章目录索引](https://blog.csdn.net/cl939974883/article/details/113203243)  [Springboot的入门初探](https://blog.csdn.net/cczj0/article/details/126785465)   [狂神说SpringBoot笔记](https://www.jb51.net/books/785526.html)    [SpringBoot](https://blog.csdn.net/qq_48575500/article/details/125008623)    [ SpringBoot](https://blog.csdn.net/weixin_46662378/article/details/109279445)  [SpringBoot课堂笔记](https://gitee.com/spears/SpringBoot/blob/master/SpringBoot课堂笔记/SpringBoot01：Hello,World！.md)  [微服务-阿里云开发者社区](https://developer.aliyun.com/article/1137800)

> 1. SpringBoot： 是一个javaweb开发框架

## 3、SpringCloud

## 2、微服务开发

[Apache Dubbo](https://cn.dubbo.apache.org/zh-cn/index.html)

> 1. 微服务是一种架构风格，它要求我们在开发一个应用的时候，这个应用必须构建成一系列小服务的组合；可以通过http的方式进行互通。
>    1. 要说微服务架构,先得说说过去我们的单体应用架构
>    2. 业务拆分成模块

## 3、常用中间件

