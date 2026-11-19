

![](./狂神说JavaSE基础.assets/java学习路线.png)

# 总结

`alt + insert` 生成构造器， ==Constructor==

ctrl + h 显示继承关系

### 对象

==构造器==

- 构造器是用来初始化值
- 定义了`有参构造`，无参构造就没了，想使用`无参构造`，无参构造就必须显式的定义

---

==封装==： 属性私有， `private int id;`  高内聚、低耦合

- 提供一些公共的可以操作私有属性的方法： get、set 
- 隐藏数据的属性，避免直接访问

---

> ==继承==

- 类和类之间关系还有`继承、依赖、组合、聚合`等
- 子类继承父类的`public`方法和属性, 私有的不能继承`private`
- 所有的类，都直接或间接继承Object
- `单继承`：1个儿子有1个爸。  `多继承`：一个子类有多个父类

super和this

- `super`指代父类,是用来访问父类成员(属性、方法、构造器);    而this指代当前类
- new子类对象时，先执行隐藏的父类无参构造`super()`，再执行子类无参构造
- 父类写了有参构造,无参构造就没了,子类也没法调用父类无参构造
  - 要么给父类补回无参构造，要么让子类显式调用父类的有参构造。

==方法重写==

- ==父类引用指向子类对象==：  
  - 也叫**向上转型（upcasting）**。意思是：声明变量时用的是父类（或接口）类型，但 `new` 出来的实际对象是子类实例
  - `B b = new A()`，父类的引用是 `b`
  - `静态方法的调用`只和左边定义的数据类型有关
  - 非静态方法的调用： 重写只和非静态方法有关
- 能调用的方法取决于引用类型： 只能调用父类中定义过的方法，但运行时若该方法被重写，实际执行子类版本，即“==编译看左边，运行看右边==”
  - 编译时：引用类型（父类）决定能调用哪些方法，父类中不存在的方法不能通过该引用调用
  - 调用范围：父类引用只能调用父类中定义的方法；子类特有方法无法通过父类引用调用，需向下转型
- 方法重写时，==父类引用指向子类对象，这是多态的核心表现==，而不是“父对象作为子对象的类型”。 实际是`子类对象被父类类型的引用指向，运行时动态绑定到子类的重写方法`。
  - 这种机制让代码面向抽象编程，如==方法参数声明父类类型，即可接收所有子类对象==，实现参数统一化，遵循开闭原则，扩展时无需修改原有代码

引用

- 多个引用指向同一个对象，这些引用是不相同的，因为引用也是一种数据类型，需要一定的内存空间（栈）来保存， 但它们的值相同，都指示同一个对象在内存（堆）的中位置

---

> ==多态==

- 多态的核心： ==父类引用指向子类对象==
- 多态说的是`一个父类引用`，在`运行时可以指向不同子类对象`，从而调用出不同的行为
  - `Animal a = new Dog();` 和 `Animal a = new Cat();`
  - 这里的 `a` 是父类 `Animal` 类型的引用，它可以在不同时刻指向 `Dog` 或 `Cat` 对象，调用 `a.eat()` 时根据实际对象类型执行对应子类的实现
- 多态核心运行机制： 编译看左边，运行看右边
  - 编译阶段：编译器检查引用变量声明类型（左边）是否有该方法，如果父类没有定义该方法，编译会报错。
  - 运行阶段：JVM 根据实际对象类型（右边）调用对应重写的方法

==向上转型与向下转型==

- 向上转型：`Animal a = new Dog();`，自动完成，但父类引用无法调用子类独有的方法，比如 `Dog` 的 `barks()` 方法。
- 向下转型：把==父类引用强制转回子类类型==，可以调用子类特有方法，但必须先用 `instanceof` 校验，否则可能抛出 `ClassCastException`。

```java
if (a instanceof Dog) {
    Dog d = (Dog) a; //父类引用a强转回子类类型 Dog,父类型强转为子类型
    d.barks();  // 安全调用子类特有方法
}
```

==instanceof==：  引用类型之间的转换   [instanceof 运算符](https://www.runoob.com/java/java-operators.html)  [instanceof](https://cloud.tencent.com/developer/article/2422148)  

- instanceof运算符: 检查左边对象，是不是右侧的实例，是就为真

### 修饰符

1. 访问修饰符：   保护对类、变量、方法和构造方法的访问
   1. public：		所有类
   2. private：       同一类内可见
   3. default：       同一包内可见
   4. protected：     同一包内的类和所有子类可见
2. 非访问修饰符
   1. final：==常量修饰符==; final 修饰的类不能被继承、修饰的方法不能被继承类重新定义，修饰的变量为常量不可修改
   2. static：修饰类、方法和类变量
   3. abstract ：用来创建抽象类和抽象方法
   4. synchronized 和 volatile 修饰符，主要用于线程的编程。

---

> static

静态属性和静态方法==都存放在方法区，属于类本身(和类一起加载)==，全局只有一份，与对象实例无关

- **静态属性（类变量）**‌：类加载时在方法区分配内存，所有对象共享同一份，不随对象创建而复制。
- ‌**静态方法（类方法）**‌：方法字节码在类加载时进入方法区，调用时在栈帧中执行，不依赖对象实例

`静态方法`中想`访问实例`成员，必须先`创建对象`或通过`参数传入对象`引用

1. ==静态代码块==：`static{ }` ; 类一加载就直接执行，只执行一次
2. ==匿名代码块== { }：创建对象时创建，在构造器之前
3. 创建对象时调用顺序： 静态代码块 => 匿名代码块 => 构造方法； 静态代码块只执行一次

### 抽象类和接口

Java类是单继承，但接口可以多继承

1. ==抽象类==：不能new抽象类，只能靠子类去实现它(只能去new子类对象)，抽象类是一个约束。
2. ==抽象方法==：`抽象类里可写普通方法`，抽象方法必须在抽象类中
   1. 抽象类==子类通过继承==实现它的方法，除非子类也是抽象类，子子类实现
      1. `public abstract class Action{}`
         1. `public class A extends Action{}`
      1. `public abstract void do()`

> 接口

```java
public interface UserService {...}
public class User implements UserService,TimeService {...}  //多继承
```

### 内部类

内部类： 在一个类的内部再定义一个类，分4种

- 成员内部类: 类的内部再定义一个类      
  1. ==通过外部类来实例化内部类==：  `Out.Inner  inner = outer.new Inner();     new Person().new Inner();`
  2. ==内部类可以访问外部类的私有属性==、私有方法
  3. 调内部类方法：`Outer.Inner in = new Outer().new Inner();`
- 静态内部类：`public static class Inner { }` ;  不能访问外部类属性：因为先实例化的内部类， 内部类加载时外部类还没加载
  - 静态内部类，和外部类相同
- 局部内部类：类写在方法里面;   
  - 局部内部类的方法需要在方法的最后实例化调用
- ==匿名内部类==：类实例出来是没有名字的， 没有名字初始化类，不用将实例保存到变量中
  1. 一般这样：Apple app = new Apple()  ； `不要名字：new Apple().eat() ` ;  
  1. new UserService(){ }   new一个接口, 里面写接口实现的方法
  1. `匿名内部类在方法内部`   new Apple().eat()

### 异常处理

==异常分类==

1. 检查性异常      
2. 运行时异常
3. 错误: 栈溢出等，脱离程序员控制

> 异常处理机制

1. `所有的异常，用一个异常类表示，把异常当作对象处理`
   1. `ctrl +alt +T`，选中包裹代码，  监控代码
   2. `try{...}catch(参数){...}finally{...}`
2. 抛出异常
   1. throw==手动抛出异常==；  throws抛出异常给方法调用者
      1. throw： 知道肯定会错，主动抛出异常;  一般在方法中使用
   2. throws： 假设方法运行时报错了，往外抛异常； 
      1. 方法中处理不了主动抛的异常，把`异常对象抛出到更高级，用try...catch捕获处理这个异常`
3. 捕获异常： 
   1. ==try监控区域==; catch想要捕获的异常类型；  
   2. try 可以监控区域； catch 捕获异常。流程：`如果try里面出现了catch参数里的异常，就执行catch代码块里面的。`
      1. 假设要捕获多个异常，层次递进，从小到大，否则上面的捕获了，下面就不捕获
   3. finally执行善后工作，出不出异常，都执行这一步

> 自定义异常

只需要继承Exception类，然后重写父类的方法

# 1、Java入门

### 复习顺序

api帮助文档： [jdk 1.8 api](https://www.baidu.com/s?ie=UTF-8&wd=jdk%20api%201.8)   [Overview (Java Platform SE 8 )](https://docs.oracle.com/javase/8/docs/api/overview-summary.html)   

md: [web技术演变](.\web技术演变)   [java知识汇总](.\java知识汇总)  [IDEA快捷键](.\IDEA快捷键)  [对象知识汇总](.\对象知识汇总)  [jdk 1.8 api](.\jdk 1.8 api.CHM)

[23种设计模式](https://www.bilibili.com/video/BV1mc411h719/?spm_id_from=333.999.0.0&vd_source=7346303e5e18677d7261c2c0c109ecfd) => 

[SE](https://www.bilibili.com/video/BV12J41137hu/?p=15&vd_source=7346303e5e18677d7261c2c0c109ecfd) => [函数式接口与Lambda表达式](https://www.bilibili.com/video/BV15S4y1v7MM/?p=4&vd_source=7346303e5e18677d7261c2c0c109ecfd) => [常用类(千锋教育)](https://www.bilibili.com/video/BV1vt4y197nY/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd) =>[集合框架](https://www.bilibili.com/video/BV1zD4y1Q7Fw/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd) => [IO](https://www.bilibili.com/video/BV1Tz4y1X7H7/?spm_id_from=333.999.0.0&vd_source=7346303e5e18677d7261c2c0c109ecfd) => [多线程](https://www.bilibili.com/video/BV1V4411p7EF/?spm_id_from=333.999.0.0&vd_source=7346303e5e18677d7261c2c0c109ecfd) => [JUC并发编程](https://www.bilibili.com/video/BV1B7411L7tE/)

[泛型](https://www.bilibili.com/video/BV1VS4y1U7Pj/?p=26&vd_source=7346303e5e18677d7261c2c0c109ecfd)  

[JVM](https://www.bilibili.com/video/BV1iJ411d7jS?p=1&vd_source=7346303e5e18677d7261c2c0c109ecfd) => [注解和反射](https://www.bilibili.com/video/BV1p4411P7V3/?vd_source=7346303e5e18677d7261c2c0c109ecfd) => [网络编程](https://www.bilibili.com/video/BV1LJ411z7vY/?spm_id_from=333.999.0.0) => [GUI编程](https://www.bilibili.com/video/BV1DJ411B75F/?spm_id_from=333.999.0.0)

[JDBC](https://www.bilibili.com/video/BV1NJ411J79W/?p=45&spm_id_from=pageDriver&vd_source=7346303e5e18677d7261c2c0c109ecfd) => [JavaWeb](https://www.bilibili.com/video/BV12J411M7Sj/?spm_id_from=333.999.0.0&vd_source=7346303e5e18677d7261c2c0c109ecfd) => [Mybatis](https://www.bilibili.com/video/BV1NE411Q7Nx/) => [Spring5](https://www.bilibili.com/video/BV1WE411d7Dv/?vd_source=7346303e5e18677d7261c2c0c109ecfd) => [SpringMVC](https://www.bilibili.com/video/BV1aE41167Tu/?vd_source=7346303e5e18677d7261c2c0c109ecfd) 

视频备份： 

常用类  集合框架 I/O  多线程  网络编程 GUI  JVM JUC并发  注解反射

[函数式编程(行为参数化)](#jump)

1. 内部类
2. 函数式接口(接口作为方法参数) => Lambda表达式 => java8内置的函数式接口(4大类) => Lambda嵌套使用 => 方法引用
3. 4种类加载器 => Native方法栈 => 栈帧 => 堆内存调优 => GC算法 => JVM执行引擎
4. 内置/元/自定义注解 => 获取反射类的几种方式 => 类加载内存分析 => 获取运行时类的完整结构(字段、方法等) => 动态创建对象,调用方法和属性 => 通过反射获取泛型、注解
5. `重点：statement对象 => PreparedeStatement对象 => 数据库连接池`
6. JavaWeb:
7. Mybatis:
8. Spring:

| ![](./狂神说JavaSE基础.assets/lambda.jpg) |      |
| ----------------------------------------- | ---- |



### Hierarchy For All Packages

> 1. Class Hierarchy
> 2. Interface Hierarchy
> 3. Annotation Type Hierarchy
> 4. Enum Hierarchy

[聊聊Java这条路](https://blog.csdn.net/chinaherolts2008/article/details/118527413)    [学习路线](https://blog.csdn.net/m0_45214113/article/details/108766032)  [软件包 java.sql ](http://jszx-jxpt.cuit.edu.cn/JavaAPI/java/sql/package-use.html#javax.sql)  [网页文字不能选](https://www.zhihu.com/question/290009096/answer/2789879469)

==视频==： [狂神Java零基础学习](https://www.bilibili.com/video/BV12J41137hu?p=15&vd_source=7346303e5e18677d7261c2c0c109ecfd) 

知识库： [Java - 菜鸟教程 ](https://www.runoob.com/java/java-basic-syntax.html)  [阿里巴巴Java开发手册（全册四版）](https://blog.csdn.net/qq_52066025/article/details/121749470)

[什么是微服务](https://aws.amazon.com/cn/microservices/)   [JDK](https://www.cnblogs.com/kouhekouhe/p/14306605.html)  [Java Platform Standard Edition 8 Documentation](https://docs.oracle.com/javase/8/docs/)  [JVM类加载机制以及双亲委派模型](https://blog.csdn.net/weixin_40378837/article/details/114555161) [第5代语言](https://blog.csdn.net/weixin_46946511/article/details/106138214)   [Java 8（JDK 1.8）升级至 Java 17（JDK 17）](https://blog.csdn.net/beita08/article/details/122128069)  [idea生成javaDoc文档 ](https://blog.51cto.com/u_13137233/3411717) [ideal中创建多级包](https://blog.csdn.net/weixin_42458708/article/details/110071908)

==快捷键==： [Icon reference ](https://www.jetbrains.com/help/idea/symbols.html#project-tw-icons)   [Gutter Icons](https://www.jetbrains.com/help/idea/settings-gutter-icons.html)  [ idea的图标](https://blog.csdn.net/qq_43476358/article/details/119826477)  [idea图标](https://www.cnblogs.com/lsgxeva/p/13386238.html)  [IDEA图标](http://t.zoukankan.com/luzhanshi-p-13238019.html)  [IDEA 字体大小 ](https://nuoyanli.blog.csdn.net/article/details/91607534?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~default-1-91607534-blog-84773696.pc_relevant_multi_platform_whitelistv1_exp2&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~default-1-91607534-blog-84773696.pc_relevant_multi_platform_whitelistv1_exp2&utm_relevant_index=1) [Idea快捷键](http://t.zoukankan.com/lovestart-p-12318411.html)  [快捷键](https://blog.csdn.net/luckyspecter/article/details/125114277)  [ IDEA—— Live Templates ](https://juejin.cn/post/7186466344500953125)

开发工具：[大厂的 开发环境](https://www.zhihu.com/question/265829202/answer/2577678915)  [代码阅读神器Sourceinsight](https://zhuanlan.zhihu.com/p/56401787)  [source insight](https://www.cnblogs.com/xunbu7/p/7067427.html) [聪明人一辈子在社会最底层](https://www.zhihu.com/question/314284424/answer/2575490528)  

`运动357：快走30分，每周5天锻炼，运动后心率+年龄=170`

工作流程：workflow; escoffier埃斯科菲耶;  [高级法餐之父Auguste Escoffier与Cesar Ritz之间的故事](https://www.bilibili.com/read/cv7277912/) [行政总厨制度](https://baijiahao.baidu.com/s?id=1727618898294350656&wfr=spider&for=pc) [熊家餐馆](https://ddrk.me/the-bear/?ep=3)

IDEA创建：[IntelliJ IDEA详细学习 ](https://www.w3cschool.cn/intellij_idea_doc/intellij_idea_doc-bozq2p62.html)  [Jboss](https://baike.baidu.com/item/Jboss/5611767?fr=aladdin)  [Thymeleaf](http://c.biancheng.net/spring_boot/thymeleaf.html)  [JSF](https://www.oschina.net/p/jsf?hmsr=aladdin1e1)  [Maven简介](http://c.biancheng.net/maven2/profile.html) [Groovy](https://baike.baidu.com/item/Groovy/180590)  [Gradle比Maven好用](https://baijiahao.baidu.com/s?id=1718368309775220656&wfr=spider&for=pc)  [Grails入门系列](https://www.cnblogs.com/wwyz/p/6792687.html) [SDK管理利器sdkman](https://www.cnblogs.com/wwyz/p/6809869.html) [Grails Application Forge服务](https://www.w3cschool.cn/intellij_idea_doc/intellij_idea_doc-nhlf2u15.html)  [grails企业web应用开发与部署](https://max.book118.com/html/2021/1110/5301142133004103.shtm)   [JDK8与Java1.8一样](https://cloud.tencent.com/developer/article/2027967) [idea查看jdk版本](https://blog.csdn.net/weixin_72618340/article/details/127504319)  [IDEA 查看类之间的关系图](https://blog.csdn.net/qq_41971087/article/details/116406182?spm=1001.2101.3001.6650.2&utm_medium=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~Rate-2-116406182-blog-111991689.235^v38^pc_relevant_sort_base1&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~Rate-2-116406182-blog-111991689.235^v38^pc_relevant_sort_base1&utm_relevant_index=5)   [Idea 高效使用技巧（Mac）](https://www.jianshu.com/p/f2875ef9bceb)  [IDEA中一些小细节设置](https://www.cnblogs.com/ql-wind/p/12826189.html)  [IDEA 使用的小技巧](https://www.ppmy.cn/news/8949.html?action=onClick)  [IDEA优化](https://blog.51cto.com/u_15127569/3976220)  [IDEA 智能补全](http://hellojava.com/a/82243.html)  [IDEA使用技巧](http://www.taodudu.cc/news/show-764382.html?action=onClick)  [IDEA插件之Java Visualizer](https://www.cnblogs.com/chch213/p/16631874.html) [ IDEA 插件](https://www.cnblogs.com/switchvov/p/15086070.html)    [ IDEA 插件](https://blog.51cto.com/zhongmayisheng/5223584)  [IDEA技巧](https://mp.weixin.qq.com/s?__biz=MzU5NTAzNjM0Mw==&mid=2247494176&idx=3&sn=3b13bc7234934cd731a6bffac4d6b398&chksm=fe7abbf8c90d32eee83bac1b327ee85d0c3c35c2d769903ef89b5229719e5a9fe81290960b96&scene=27)  [IDEA 小技巧](https://www.shangyexinzhi.com/article/6059949.html)  [ IDEA技巧](https://blog.csdn.net/linsongbin1/article/details/80211919)

包管理系统和环境管理系统：[Conda](https://blog.51cto.com/u_14782715/5082286)   [Anaconda ](https://blog.51cto.com/u_14744108/5257275?articleABtest=1)

plugins：[ IDEA 日常](https://blog.csdn.net/yang_shibiao/article/details/122615377?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-0-122615377-blog-126281672.235^v36^pc_relevant_default_base3&spm=1001.2101.3001.4242.1&utm_relevant_index=3)   [ 函数签名（方法签名）Type signature](https://blog.csdn.net/notsaltedfish/article/details/75174852)   [aiXcoder](https://aixcoder.com/#/trial/?loginId=7d655117-f34f-4fe2-8307-be68e62a7468)  [codesearch](https://codesearch.aixcoder.com/#/)  [String Manipulation 字符串处理](https://blog.csdn.net/qq_41489540/article/details/119394122) [Translation](https://yiiguxing.github.io/TranslationPlugin/#/docs)  [Lombok介绍](https://www.cnblogs.com/holten/p/5729226.html)  [Lombok ](https://www.knowledgedict.com/tutorial/lombok-intro.html)  
java可重用组件：[JavaBean](https://www.cnblogs.com/mq0036/p/3873406.html)
[java中的goto和const](https://www.cnblogs.com/gengshao/p/15969030.html)  [Java中没有const？](https://zhuanlan.zhihu.com/p/58314726)

> 1. Lombok 是一个 java 类库，利用注解方式自动生成 java bean 中 getter、setter、equals 等方法，还能自动生成 logger、toString、hashCode、builder 等 日志相关变量、Object 类方法或设计模式相关的方法，能够让你的 代码更简洁，更美观； 简化了 JavaBean 的编写
> 2. Idea当前行背景色 ：caret row ；    caret 光标位置、插入号

> 1. `JBoss`：基于J2EE的开放源代码的应用服务器
> 2. `Thymeleaf`：用于渲染 XML/XHTML/HTML5 内容的模板引擎。它与 JSP，Velocity，FreeMaker 等模板引擎类似，也可以轻易地与 Spring MVC 等 Web 框架集成。与其它模板引擎相比，Thymeleaf 最大的特点是，即使不启动 Web 应用，也可以直接在浏览器中打开并正确显示模板页面 `Thymeleaf 语法分 2 类：标准表达式语法、th 属性`
> 3. JavaServer Faces (JSF) ：以组件为中心来开发 Java Web 用户界面
> 4. Maven ：项目管理工具，可以对 Java 项目进行构建、依赖管理；纯 Java 开发。基于项目对象模型（POM）概念，Maven利用一个中央信息片断能管理一个项目的构建、报告和文档等步骤。`将项目的开发和管理过程抽象成一个项目对象模型（POM）。开发人员只需要做一些简单的配置，Maven 就可以自动完成项目的编译、测试、打包、发布以及部署等工作。`
> 5. Groovy：基于[JVM](https://baike.baidu.com/item/JVM)（[Java虚拟机](https://baike.baidu.com/item/Java虚拟机)）的敏捷开发语言，它结合了[Python](https://baike.baidu.com/item/Python)、[Ruby](https://baike.baidu.com/item/Ruby/11419)和[Smalltalk](https://baike.baidu.com/item/Smalltalk)的许多强大的特性，Groovy 代码能够与 Java 代码很好地结合。
> 6. Gradle：基于Apache Ant和Apache Maven概念的项目自动化构建开源工具。它使用一种基于Groovy的特定领域[语言](https://baike.baidu.com/item/语言/72744)(DSL)来声明项目设置，也增加了基于Kotlin语言的kotlin-based DSL，抛弃了基于XML的各种繁琐配置。 面向Java应用为主。
> 7. Grails：用于快速 Web 应用开发的开源框架，基于 Groovy ，并构建于 Spring、Hibernate 和其它标准 Java 框架之上，从而为大家带来一套能实现超高生产力的一站式框架。

> 1. 三大版本：JavaSE 标准版； JavaEE 企业版；JavaMe嵌入式（基本淘汰）
> 2. JDK：Java Development  Kit      JRE：Java Runtime  Environment     JVM：Java Virtual Machine
>    1. java javac编译运行java； javadoc生成文档； jar把java打包成应用； 
>    2. jvm：java虚拟机，可看作一种规范，可用软件实现，也可用硬件实现，模拟了一个cpu，去处理java相关东西

| ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-18_10-12-03.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-18_10-12-52.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-18_10-14-16.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-18_10-15-29.jpg) |
| ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-18_10-17-35.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-18_10-19-58.jpg) |
| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-15_10-27-16.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-03_16-10-13.jpg) |

### 开发环境

[IDEA 2019.3激活](https://www.jb51.net/article/195716.htm)  

D盘目录下建 `Environment` 目录，把 Java、tomcat、maven、mingw64 等安装到这里

配置环境变量: `JAVA_HOME`， Path下 `%JAVA_HOME%\bin、 %JAVA_HOME%\jre\bin`

==javac编译==：`javac  Hello.java`，会生成一个class文件。     运行class文件：`java Hello`

1. jdk目录：bin可执行文件； include头文件； jre运行时环境； lib类库文件； src.zip资源文件，很多java类
2. java大小写敏感， ==文件名和类名必须一致，并且首字母大写==

> include：jdk由c开发，启动时要引入一些c语言头文件。 jre：java运行时环境，只跑java，有jre就够了。lib：java的类库文件
>
> - src.zip里面放java的资源文件，java基础类的一些源代码。

### 编译型和解释型

参考：  [java知识汇总](.\java知识汇总)

Java 被称为“编译与解释并存”的==混合型语言==，既有编译型又有解释型特点

将.java编译成.class字节码文件的过程是编译期, 从.class文件加载到内存，并对数据进行校验、转换解析和初始化，最终形成可被虚拟机直接使用的Java类型的过程就是运行期，也就是类加载过程。  字节码校验器：看代码写的对不对。

1. **javac** 后跟java文件，例如 HelloWorld.java。 用于将 java 源文件编译为 class 字节码文件
2. `javap`主要作用: 字节码文件反编译为.class文件, 我理解就是： 通过反射注解获取，不涉及运行中的java程序
   1. **展示Java类的结构**：可以从字节码级别上查看类的继承关系、方法和字段的信息
   2. **反编译Java字节码**：将已编译的Java类文件转化为人可读的源代码形式，以便进行分析和理解
3. 帮助开发人员深入了解和分析已编译的Java类文件
   1. 通过解析Java类文件的字节码数据，并根据Java虚拟机规范定义的格式和约定，将其转化为易于阅读的文本形式。它==使用反射和解析技术==来获取类的结构和信息，并进行适当的格式转换和展示

# 2、基础语法

[Java数据类型](https://www.cnblogs.com/sjch/p/java.html)   [ java中最常用的包和类](https://blog.csdn.net/piratesjjcf/article/details/52506458)  [类分层结构 ](https://download.oracle.com/technetwork/java/javase/6/docs/zh/api/overview-tree.html)  [Java.util包](https://baijiahao.baidu.com/s?id=1760980933322853938&wfr=spider&for=pc)  [java.util  ](https://www.apiref.com/java11-zh/java.base/java/util/package-summary.html)
[自带反编译工具javap](https://blog.csdn.net/LVSONGTAO1225/article/details/131476263)  [4款主流反编译工具](https://mikechen.cc/15822.html) [反编译工具](https://www.27ka.cn/34044.html)  [7个Java反编译器工具](https://baijiahao.baidu.com/s?id=1726712623310495935&wfr=spider&for=pc)  [arthas](https://arthas.aliyun.com/doc/)

[通俗易懂：字节码与Class文件的关系](https://blog.csdn.net/weixin_45987569/article/details/127852103)  `Class文件的本质是一个十六进制的文件` [Class字节码文件](https://www.cnblogs.com/billyqiu/p/14341860.html)  [从一个class文件深入理解Java字节码结构](https://code84.com/569307.html) [eclipse里打开.class文件为什么能看到源码？](https://www.zhihu.com/question/284044773/answer/877405454)   [.class是字节码,为什么还能显示源码](https://www.baidu.com/s?ie=UTF-8&wd=.class是字节码，为什么还能显示源码)

==空的项目==：  psvm  sout

1. Creat New Project $\Rightarrow$ `empty project`  
2. File $\Rightarrow$ `new_module`  
3. project structure : `^+alt+sh+s`， ==SDK设1.8， level设为8== 

> 1. idea颜色设置：editor->color scheme->java
> 2. 3种注释：单行//,  多行 /* */ ,  文档注释 /**开头  */结尾，可加参数@
> 3. 标识符：字母（A-Z 或者 a-z）,美元符（$）、或者下划线（_）开始
> 4. ==数据类型==：强类型语言，变量必须先定义后使用，分两类：
>    1. 8大基本类型(数值类型[整、小数、字符]、布尔类型)、引用类型(类、接口、数组)，long后加L，float后加F；string不是关键字，是类。`jdk7新特性，数字间可用下划线分割，10_000`
>    2. 引用类型： 类、接口、数组
>    3. 数据类型扩展：二进制0b开头；八进制0开头 ；十六进制0x； 浮点数扩展：舍入误差，`银行用BigDecimal数学工具类表示钱`。
> 5. ==类型转换==：所有字符本质还是数字(编码解码，几个二进制数代表字符);Unicode编码（2字节）：65代表A；  `char  c100 = '\u0061'` ==运算中，不同类型先转化为同一类型，再进行运算==；强制类型转换(从高到低)：` (int)c2` .自动类型转换(低到高)。 注意：转换可能内存溢出或精度问题。
>    1. 强制转换：(类型)变量名；由高到低内存溢出：只能存127，放个128就溢出
>    2. 自动转换：低到高
> 6. ==变量==： 注意：变量声明是完整语句，==必须以分号结尾==。除了基本类型，其余的默认值都是`null`;类变量能直接使用，为了方便调用，都加static。 实例变量调用要new一个对象。  变量类型 变量名字 = xxx
>    1. 命名规范：类：首字母大写+驼峰；   方法：首字母小写+驼峰；  变量：首字母小写+驼峰；   常量：大写字母
>    2. 局部变量：方法里面，必须声明和初始化值
>    3. 类变量：静态变量，写在类里面,`有static`
>    4. 实例变量： 成员变量、非静态变量`无static`==从属于类==） 
> 7. 常量：final 常量名=值；常量名一般大写。static  final double PI = 3.14;  `修饰符不分先后顺序`
> 8. ==运算符==：等于2个等号==。 int b=a++(先给b赋值，再自增);  ++a(先自增，再赋值);幂运算：用数学类Math.pow(3,2)； `位运算：左移*2,和计算机底层打交道，效率很高` a+=b  //a=a+b;     三元运算符： `x?y:z,如果x==true，结果为y，否则z`运算符优先级
> 9. ==包机制==：src->new package -> refactor；作用：`为了更好的组织类，防止类名的命名空间冲突。包的本质就是文件夹`包名：一般域名倒置，com.baidu.www   导包：import   java.util.Date  《阿里巴巴Java开发手册》
>    1. Java.util包是最常用包之一，包含了许多与数据结构、日期时间、随机数、集合框架等相关的类和接口
> 10. JavaDoc  -encoding UTF-8  -charset UTF-8  Doc.java    //IDEA生成JavaDoc文档
>     1. 将注释信息生成帮助文档
> 11. javac Hello.java   将java源文件编译为 class 字节码文件(Hello.class)
>     1. java Hello         运行java类, 不加 .class
>     2. **.class**文件通过**java虚拟机(JVM)**传送指令给**解释器**, **解释器**将指令翻译成**特定机器**上的目标**机器码**，进行运行
>     3. .java编译成.class文件，类加载器，字节码校验器，解释器

### 数据类型

参考： [c语言汇总](.\..\..\编程语言\C语言\c语言汇总)， 传值、传址、传引用，传引用底层也是通过指针实现

java数据类型分为2大类：

- 8大基本类型：[范围](https://www.runoob.com/java/java-basic-datatypes.html)  `2的8次方 到 64次方 (1\2\4\8个字节) ； 浮点数32、64位;  char 16位`
  - `1B(byte)=8b(bit)  1KB=1024B`
  - 浮点数是有问题的，离散的，会四舍五入；银行业务用BigDecimal数学工具类
- 引用类型：类接口数组
- 类型转换
  - 从低到高
  - ==强制类型转换==：由高到低，转换会内存溢出
  - ==自动类型转换==：低到高， `(type)value`
  - 2个数相乘内存溢出时，一个数要先转为高


| ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-03_17-02-06.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-03_17-03-14.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-21_11-37-51.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-21_17-16-52.jpg) |
| ![银行用工具类](./狂神说JavaSE基础.assets/Snipaste_2023-12-09_07-01-19.jpg) | ![其中一个数转换为高](./狂神说JavaSE基础.assets/Snipaste_2023-12-09_06-49-09.jpg) |
| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-15_14-35-29.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-21_17-28-40.jpg) |

### 变量

[实例变量](https://cloud.tencent.com/developer/article/2172481)  

> Arrays类中的方法是==静态方法==，使用时可直接==使用类名调用==，而==不用使用对象调用==

- 类变量：相当于C语言的`静态变量`（static）
  - ==静态变量‌== 又称 ==类变量==
- 实例变量：相当于==结构体成员（或全局变量）==
  - 实例变量属于对象,随对象创建而存在,销毁而消失
  - 类中定义在方法外部、且没有static修饰的变量称为‌==实例变量‌==，也常被称为‌==成员变量‌==或‌非静态成员变量
- 局部变量：相当于自动变量（auto）

这是从存储位置、生命周期和作用域三个维度对应的

常量： final 修饰常量， `final double PI = 3.1415927`

| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-15_15-18-50.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-15_15-33-45.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-03_20-40-55.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-03_21-29-02.jpg) |

### 运算符

Java运算符：a++ : a=a+1       a+1后赋值给a

 三元运算符： `x?y:z,如果x==true，结果为y，否则z`运算符优先级


| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-15_15-35-14.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-15_17-55-27.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |

### 包机制和JavaDoc

1. ==包机制==：src->new package -> com.baidu.www，一个包拖入另一个包时，出现提示按do refactor； 左边打开包位置：`package java.lang;` 按ctrl点lang
   1. 作用：为了更好的组织类，防止类名的命名空间冲突
   2. ==包的本质就是文件夹==，包名：一般域名倒置，com.baidu.www   
      1. ==导包==：`import   java.util.Date`  《阿里巴巴Java开发手册》
         1. 例 Date，按alt+enter，导入包路径
   3. Java.util包是最常用包之一，包含了许多与数据结构、日期时间、随机数、集合框架等相关的类和接口
2. `JavaDoc  -encoding UTF-8  -charset UTF-8  Doc.java`    //IDEA生成JavaDoc文档
   1. 将注释信息生成自己的API帮助文档

| ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-21_22-55-16.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-21_23-02-49.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-03_21-59-25.jpg) |                                                              |

### 用户交互Scanner

`用户交互Scanner`：通过Scanner类获取用户输入。java.util.Scanner，Scanner类的next()与nextLine()方法获取输入的字符串。
Scanner s = new Scanner(System.in);

```java
package com.Britney.scanner;
import java.util.Scanner;

public class Demo {
    public static void main(String[] args) {
        //创建一个扫描器对象，用于接收键盘数据
        Scanner scanner = new Scanner(System.in);
        System.out.println("使用nextLine方式接收：");

        //判断用户有没有输入字符串
        if (scanner.hasNext()) {
            String str = scanner.nextLine();
            System.out.println("输出内容为：" + str);
        }
        //IO流的类如果不关闭会一直占用资源
        scanner.close();
    }
}
```
1

| ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-03_23-12-13.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-03_23-12-47.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-04_00-54-21.jpg) | ![]()                                                        |

# 3、流程控制

顺序、选择、循环

### 选择结构

> 1. if单选择：
> 2. if双选： if -> else
> 3. if多选： if -> else if ->else
> 4. 嵌套if：
> 5. switch多选择：switch(expression){case value:语句}

| ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-04_01-03-28.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-04_01-06-10.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-04_01-07-01.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-04_01-07-56.jpg) |
| ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-04_01-08-53.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-22_12-49-00.jpg) |

### 循环结构、迭代

==while==先判断后执行 、==do...while==先执行后判断 、==for==循环   
[九九乘法表](https://blog.csdn.net/i_tenkai/article/details/103010141)   [什么是迭代器](https://blog.csdn.net/phantomthief1412/article/details/122119673)  [迭代器 ](https://learn.microsoft.com/zh-cn/dotnet/csharp/iterators) [迭代器(iterator)](https://blog.csdn.net/qq_45963013/article/details/119217905)  [单步调试 step into/step out/step over](https://blog.csdn.net/huangfei711/article/details/51220382)
[迭代](https://baike.baidu.com/item/迭代/8415523?fr=aladdin)  ==每一次对过程的重复==称为一次“*迭代*”，而每一次*迭代*得到的结果会作为下一次*迭代*的初始值。
a+=2： a=a+2；每次循环，将a的值刷新，叫做迭代
迭代器遍历容器的对象，尤其是列表 ； 迭代器的作用是用来访问容器中的元素

| ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-04_01-16-06.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-04_01-16-46.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-04_01-18-31.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-04_01-19-22.jpg) |
| ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-23_13-30-16.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-23_13-38-43.jpg) |
| ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-23_13-45-44.jpg) |                                                              |

反编译：类文件能在idea反编译。 点击：Project  structure (^alt+sh+s) ；在idea中打开编译后的.class文件

> step into：单步执行，遇到子函数就进入并且继续单步执行（简而言之，==进入子函数==）；
> step out：当单步执行到子函数内时，用step out就可以执行完子函数余下部分，并返回到上一层函数。
>
> step over：在单步执行时，在函数内遇到子函数时不会进入子函数内单步执行，而是将子函数整个执行完再停止，也就是把子函数整个作为一步。有一点,经过我们简单的调试,在不存在子函数的情况下是和step into效果一样的（简而言之，==越过子函数==，但子函数会执行）

> 1. while： while (i<100) {
>    		i++; 
>       		System.out.println(i);
>    }
> 2. do...while：至少执行一次。
>    1. do { 代码语句 }  while  { 布尔表达式 }；
> 3. for：快速输入100.for ;

```java
package com.Britney.loop;

public class For {
    public static void main(String[] args) {
        //计算0到100奇数和偶数的和
        int oddSum = 0;
        int evenSum = 0;
        for (int i = 0; i <= 100; i++) {
            if (i % 2 != 0) {
                oddSum += i; //oddSum = oddSum + i;
            } else {
                evenSum += i;
            }
        }
        System.out.println("奇数的和：" + oddSum);
        System.out.println("偶数的和：" + evenSum);
    }
}
```

```java
package com.Britney.loop;
public class Demo {
    public static void main(String[] args) {
        //输出1-1000之间能被5整除的数，并且每行输出3个
        for (int i = 1; i <= 1000; i++) {
            if (i % 5 == 0) {
                System.out.print(i + "\t");  //tab间隔
            }
            if (i % (5 * 3) == 0) {  //换行
                System.out.println();
                //System.out.print("\n");
            }
        }
    } //printLn输出完换行；print输出完不换行
}
```

```java
/*
1*1=1
2*1=2	2*2=4
3*1=3	3*2=6	3*3=9
4*1=4	4*2=8	4*3=12	4*4=16
5*1=5	5*2=10	5*3=15	5*4=20	5*5=25
6*1=6	6*2=12	6*3=18	6*4=24	6*5=30	6*6=36
7*1=7	7*2=14	7*3=21	7*4=28	7*5=35	7*6=42	7*7=49
8*1=8	8*2=16	8*3=24	8*4=32	8*5=40	8*6=48	8*7=56	8*8=64
9*1=9	9*2=18	9*3=27	9*4=36	9*5=45	9*6=54	9*7=63	9*8=72	9*9=81
思路：1、先打印第一列 2、把固定的1再用一个循环包起来 3、去掉重复项，j<=i  4、调整样式
 */
public class Demo2 {
    public static void main(String[] args) {
        for (int i = 1; i <= 9; i++) {
            for (int j = 1; j <= i; j++) {
                System.out.print(i + "*" + j + "=" + (j * i) + "\t");
            }
            System.out.println();    //输出完换行
        }
    }
}
```

增强for循环，用于数组和集合，遍历数组：for(声明语句：表达式)

```java
public class Demo3 {
    public static void main(String[] args) {
        int[] numbers = {10, 20, 30};   //定义数组
        for (int x : numbers) {
            System.out.println(x);
        }
    }
}
```

break：跳出switch，结束循环：强行退出循环，不执行循环中剩余语句；continue终止某次循环，接着进行下一次循环。  
return:方法结束，返回一个结果
打印三角形  

# 4、方法
### 1、方法定义及调用
[值传递](https://blog.csdn.net/longgetaotao_06/article/details/125941193)  [值传递与引用传递](https://blog.csdn.net/Start1234567/article/details/109373902)  [值传递和引用传递](https://baijiahao.baidu.com/s?id=1687423265048253873&wfr=spider&for=pc)

`System.out.println(sum);`   System==类.对象.方法==

> 1. 方法：保持原子性，一个方法只完成1个功能
> 2. 返回值：void不返回东西；如果方法有返回值，一定要把返回值用return返回出去。  return 0 终止结束方法。
> 3. 值传递：Java都是值传递。引用传递
>    1. 类是一个模板，它描述一类对象的行为和状态。  对象是类的一个实例，有状态和行为。
> 4. 修饰符：修饰类中方法和属性。主要有两类修饰符：访问控制修饰符、非访问控制修饰符
> 5. static方法调用：  有返回值 int sum = add(1, 2)   或   无返回值System.Out.printLn()
>    1. 不是static方法调用：Demo04 demo04 = new Demo04()  //new一个类，返回一个实例对象； demo04.test()   对象.方法
>    1. ==静态方法调用==：有static   在另一个类中调用Student.sya() ;  类名.方法      ==非静态方法==：没有static，调用要实例化 Student stu=new Student();   stu.sya()      //new student().say()

```java
public class Demo1 {
    public static void main(String[] args) {
        int sum = add(1, 2); //调用方法
        System.out.println(sum);  //System类.对象.方法
    }

    //定义方法
    public static int add(int a, int b) {
        return a + b;
    }
}
```

| ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-24_11-56-03.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-12-09_17-22-53.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-04_10-06-14.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-24_14-59-24.jpg) |
| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-16_15-24-13.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-12-09_17-37-20.jpg) |
| ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-24_16-36-46.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-24_16-44-20.jpg) |
| ![可变参数](./狂神说JavaSE基础.assets/Snipaste_2026-11-04_15-26-06.jpg) |                                                              |

### 2、==方法重载==

参数不同，执行结果不同:  加珍珠,店员做成珍珠奶茶；  加红枣，做成红枣奶茶

> 重载是“同名不同参”，方便调用； 重写是“==子类改父类的方法==”，实现多态
>
> - 重载：同一个类里，多个方法名一样，参数不一样。
> - 重写：子类和父类之间，方法名和参数都一样，子类重新实现

例如：比大小，参数是(int a, int b)；现在想比较小数的大小，就复制一个方法，参数改为(double a,double b);比较时：int max=max(10,20)比较int类型，double max=max(10.0,20.0)比较double类型。
就是一个类，有2个方法，有相同的名字，只是参数不同。  同一个类中定义了多个同名方法，但参数类型或个数不同、顺序不同

### 3、命令行传参、可变参数
[Linux标准输入、重定向与参数传递 ](https://zhuanlan.zhihu.com/p/337386886)

> 1. 命令行传参：了解就行。 `java com.kuang.Demo01   this is kuangshen` ；  运行程序时传参，`this is kuangshen` 是传进去的数组
>    1. 给main()函数传递参数
> 2. 可变参数... ：方法有很多不确定参数怎么办？传递同类型的可变参数给一个方法。 //不定项参数：不规定给它传多少参数。 
>    1. 方法声明中，在指定==参数类型后加省略号== 
>    2. 一个方法只能指定一个可变参数，必须是方法的最后一个参数，普通的参数必须在它之前声明。  //public void test(int x,int... y){}

### 4、递归
`A方法调用A方法，就是自己调用自己. 阶乘：!5=5*4*3*2*1;   递归头:什么时候不调用自身方法； 递归体：什么时候调用自身方法` ；递归有3个阶段： 前阶段 => 递归边界 => 返回阶段   **函数进行自我调用，就被称为递归**
[递归遍历和递归删除](https://www.bilibili.com/video/BV1Tz4y1X7H7/?p=29&vd_source=7346303e5e18677d7261c2c0c109ecfd)  [递归_打印目录树结构](https://www.bilibili.com/video/BV1qL411u7eE/?p=147&vd_source=7346303e5e18677d7261c2c0c109ecfd)  [递归的原理及其机制 ](https://leetcode.cn/circle/article/PR90sP/)

> 1. 分析：阶乘传入2，不等1，就走else，2*jiecheng(2-1), 2x1=2,就返回2。  `传入3，走else，3*jiecheng(2),jiecheng(2)再往下调自身，直到jiecheng(1),会返回一个具体的结果1，再往前计算。`  递归要有一个尽头
>2. 递归头：就是尽头，执行到底了，递归能跑的出来。jiecheng(1)就是尽头。
>    1. 递归边界：尽头。  `前面阶段：参数不等于1时，不停的调用自身。` 返回阶段
>3. 每调用一次，就压一次栈。嵌套层次比较深，电脑就卡死，栈溢出，能不用递归就不用，小计算用递归，层次深的就免了

| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-16_18-07-41.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-25_17-01-05.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-25_16-04-21.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-12-09_19-41-03.jpg) |

# 5、数组
### 1、数组声明、创建、数组元素赋值、三种初始化
> 1. ==声明==一个数组：int[] nums;       创建一个数组，==分配空间==：nums=new int[10]    //可存10个int类型的数字。    ==数组元素赋值==：nums[0]=1
>    1. 声明创建写一起：`int[] nums = new int[10]`
>    1. 常用类型后加[]； 变量名后加[]是c风格的，为了让c程序员快速学java。
> 2. ==使用==：定义了一个什么类型的数组，就new一个什么类型的数组。  //int[] nums = new int[10]， 这里面可存10个int类型数字
>    1. 给数组元素赋值：nums[0] = 1

> 1. ==声明数组时==，int[] array; 栈里压入一个array, ==创建数组时==，array=new int[10];  new了一个int[10],==在堆里开辟了一个空间==，分成10个小份。==给数组赋值==: nums[1]=1;   
> 2. ==数组的三种初始化== 
>    1. `静态初始化`：直接定义, int[] a= {1,2,3,4}	//创建 +  赋值
>    2. `动态初始化`： int[] a= new int[10];  new分配空间，里面所有值都是默认的，需要后期赋值。  包含默认初始化；  方便理解下面：很多男人里有男人1，男人2.      引用类型要.(点)出来  System.num
>    3. `默认初始化`:数组一经分配空间，有默认值，隐式初始化; `int[] a= new int[10]之后，10个元素有个默认值0`
> 3. 声明数组时，数组是空的，栈里只是一个名字，没实际作用。  =>  然后new创建数组,new的东西，都会放在堆里面，在堆里开辟了一块数组空间，分成10个小份  =>然后给数组赋值，
> 4. 除了8大基本类型，都是引用类型

类变量

实例变量==相当于结构体成员， 存在堆内存==，随对象创建/回收

局部变量

| ![](./狂神说JavaSE基础.assets/Snipaste_2023-12-09_20-39-01.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-12-09_20-50-50.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-17_00-06-53.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-17_00-09-23.jpg) |
| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-27_14-26-05.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-17_00-22-15.jpg) |
| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-17_00-27-29.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-04_16-30-08.jpg) |
| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-17_00-30-48.jpg) | ![]()                                                        |

### 2、数组使用

1. 数组遍历：`for: arr[i].sout`;  
   1. for
   2. for each循环
      1. 增强for遍历：`for(int x : arrays){ }`；  int x数组中的元素
   3. 计算元素和、查找最大元素、反转数组
      1. 反转数组：数组元素1234变成4321
2. ==数组作为方法参数、返回值==：`public static int[]   reverse(int[]  arrays){...}`
   1. 作为方法参数：用来对数组进行一些操作
   2. 数组作为返回值：像反转数组，把数组修改一下，返回一个新的数组



| ![](./狂神说JavaSE基础.assets/Snipaste_2023-12-10_20-51-49.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-26_17-29-40.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-27_13-45-55.jpg) | ![]()                                                        |

##### Java内存分析
 [Java内存分析图解](https://blog.51cto.com/u_15697790/5419611)     [Java内存分析工具](https://www.cnblogs.com/oldpub-blog/p/16517155.html)  [Java内存分析](https://www.cnblogs.com/rsp2012/p/16052834.html)    [Debug方式+内存分析，真正学懂设计模式](https://baijiahao.baidu.com/s?id=1766602880405656200&wfr=spider&for=pc)
[单例模式](https://zhuanlan.zhihu.com/p/426672787)  [单例模式](https://www.runoob.com/design-pattern/singleton-pattern.html)  [ JAVA设计模式之单例模式](https://blog.csdn.net/jason0539/article/details/23297037/)  
[ Java内存分析工具 JProfiler](https://blog.51cto.com/u_15746412/5711369)    [Java性能调优](https://www.bilibili.com/video/BV1oE411t7pZ/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd)   [Java的继承内存分析](https://blog.csdn.net/z2768557792/article/details/124307039)  [java继承中内存分析](https://blog.51cto.com/topic/javajichengzhongneicunfenxi.html)  [ java 创建对象的内存图解](https://blog.csdn.net/TYRA9/article/details/128508466?spm=1001.2014.3001.5501)  [ java 继承关系的内存图解](https://blog.csdn.net/TYRA9/article/details/128729074)   [Java中数组的内存分析](https://blog.51cto.com/u_11702014/6187652)  [java dump 内存分析 java分析内存占用](https://blog.51cto.com/u_16099281/6338697)  [java中多态机制的内存解析、抽象类、接口](https://www.jianshu.com/p/0599a3dab8b9)   
[JVM](https://www.bilibili.com/video/BV1hX4y1m7QP?p=4&vd_source=7346303e5e18677d7261c2c0c109ecfd)  [jvm](https://search.bilibili.com/all?vt=03514452&keyword=jvm&from_source=webtop_search&spm_id_from=333.1007&search_source=5)
内存分析工具：[Java Visualizer](https://blog.csdn.net/zhj1698/article/details/126344041)  [性能分析VisualVM Launcher](https://www.lmlphp.com/user/64336/article/item/661616/)  

[JAVA性能分析工具](https://blog.csdn.net/qq_36908872/article/details/124062589)  [VisualVM](https://www.lmlphp.com/user/62390/article/item/877396/)  [VisualVM](https://blog.51cto.com/u_14014612/5690468) [VisualVM工具](https://www.rstk.cn/news/727889.html?action=onClick)  [VisualVM](https://blog.csdn.net/weixin_42753193/article/details/124523127)  [jvisualvm](https://www.cnblogs.com/hd92/p/16901756.html)  [VisualVM 远程](https://blog.csdn.net/wngpenghao/article/details/82884874) [VisualVM Launcher](https://blog.csdn.net/zhouzhiwengang/article/details/124323799)   

[JVM加载class文件的原理机制实例详解](https://www.jb51.net/article/246418.htm)

图书：[JVM经典书籍](https://blog.csdn.net/xiaojin21cen/article/details/87826283)

`堆内存保存对象的真实信息，只要是new出来的对象都在堆内存；栈内存保存的是一块堆内存的地址，通过该地址可以找到对应的真实对象数据；方法区是保存静态属性`
Java内存分析：堆：存放new出来的数组和对象。栈：存放变量类型

> 1. JVM内存分类
>    1. 栈内存
>       1. 连续的存储空间，遵循后进先出的原则,  生命周期与线程相同
>       2. 栈分为3个部分：基本类型变量区、执行环境上下文、操作指令区(存放操作指令)
>          1. ==是Java方法执行的内存模型==，每个方法执行时会创建**局部变量表、操作数栈、动态链接、方法出口**等信息
>          2. ==局部变量表存放==：各种基本数据类型、对象引用、returnAddress类型，所需内存空间在编译期完成分配固定
>          3. long和double占2个局部变量空间（Slot）,其它基本数据类型占1个
>       3. 每个栈中的数据(原始类型和对象引用)都是私有的，其他栈不能访问
>       4. 每个线程包含一个栈区，栈中只保存基础数据类型的对象和自定义对象的引用(不是对象)
>    2. 堆内存
>       1. 不连续的空间，用于存放new出的对象，保存的是真正的数据
>          1. 唯一目的是存放**对象实例**
>       2. JVM只有一个堆区(heap)被所有线程共享:  所有线程共享，在虚拟机启动时创建
>    3. 方法区
>       1. 又叫静态区，跟堆一样，被所有的线程共享
>       2. 方法区中包含的都是在整个程序中永远唯一的元素，如class，static变量等静态属性（①类的代码信息；②静态变量和方法；③常量池（字符串常量等，具有共享机制））
>          1. 用于存储虚拟机加载的，**类信息、常量、静态变量、编译后的代码**等
>    4. 运行时常量池
>    5. 程序计数器
>    6. 本地方法栈
>    7. 直接内存
> 2. 引用传递
>    1. 产生的原因是同一块堆内存被多个栈内存指向
>    2. 引用传递，垃圾产生：ball2原本指向的一块堆内存在引用传递后，再也没有指向它的引用，就会成为垃圾空间被JVM的GC回收掉
>       1. 一个栈内存只能保存一个堆内存的地址，如果发生改变，之前指向的堆内存就会成为垃圾空间。垃圾空间是指没有任何栈内存所指向的堆内存空间，由GC不定期回收，垃圾空间过多会影响GC的处理性能
> 3. 内存泄漏
>    1. 不再被使用的对象的内存不能被回收，就是内存泄露
>    2. 当长生命周期的对象持有短生命周期的对象时，就会产生内存泄露
>       1. 解决内存泄露： 需要把短生命周期的对象定义成局部变量，随着方法体的结束而结束； 尽量减小对象的作用域
>       2. 或者 手动标记成垃圾空间，由GC回收；  垃圾回收(Garbage Collection,简称*GC*)
>    3. 单例模式导致的内存泄露
>       1. 单例模式就是确保一个类在**任何情况下**都**只有一个实例**，并**提供一个全局访问点**
>          1. 有些对象我们只需要一个，比如线程池、ServletContext、ApplicationContext、 Windows中的回收站，此时我们便可以用到单例模式
>       2.  单例模式，是一个长生命周期的对象。如果这个对象持有其他对象的引用，也很容易发生内存泄露
>       3. 解决方案：使用弱引用

| ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-26_12-47-08.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-26_12-50-41.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-26_12-53-52.jpg) | ![](./狂神说JavaSE基础.assets/20190804125050490.png)         |
| ![](./狂神说JavaSE基础.assets/0ead2dce0895486cb9bb3592b9798705.jpg) | ![](./狂神说JavaSE基础.assets/r.png)                         |

##### JVM体系结构

[JVM](https://blog.csdn.net/weixin_43771403/article/details/121288104)   [JVM内存模型和类加载运行机制](https://zhuanlan.zhihu.com/p/500205913)    [Java内存区域和内存模型](https://www.cnblogs.com/czwbig/p/11127124.html)  [JVM内存模型](https://zhuanlan.zhihu.com/p/411021919)   [栈帧](https://zhuanlan.zhihu.com/p/87360857) [JVM内存结构图](https://zhuanlan.zhihu.com/p/359379225)  [类文件结构](https://blog.csdn.net/CoderLai/article/details/90054471)  [JVM如何分配内存](https://blog.csdn.net/u013547284/article/details/71055640/)  [对象内存布局](https://blog.csdn.net/CoderLai/article/details/90054471)

`类加载器->校验->解释器`

###### 1、栈帧

- **类加载器**：加载class文件；
- **运行时数据区**：包括方法区、堆、Java栈、程序计数器、本地方法栈
- **执行引擎**：执行字节码或者执行本地方法

1. 栈：用于描述Java方法执行的模型。每个方法在执行的同时都会创建一个栈帧，存储方法的局部变量表、操作数栈、动态链接、方法出口(返回地址)等信息。每一个`方法从调用至执行完成，对应于一个栈帧入栈到出栈`
   1. 操作数栈：随着方法执行和字节码指令的执行，会从局部变量表或对象实例的字段中复制`常量或变量写入到操作数栈`，再随着计算的进行将栈中元素`出栈到局部变量表或者返回给方法调用者`，也就是出栈/入栈操作
   2. ==动态链接==:每个栈帧都包含一个指向运行时常量池中该栈所属方法的`符号引用（类和接口的全限定名、字段名称和描述符、方法名称和描述符）`，持有这个引用的目的是为了支持方法调用过程中的动态链接(Dynamic Linking)
      1. 每个栈帧中包含一个在常量池中对当前方法的引用， 目的是支持方法调用过程的动态连接
2. 堆：存放对象实例
3. 方法区：共享内存区域，存储已被虚拟机加载的`类信息、常量、静态变量、即时编译器编译后的代码等数据`
4. **本地方法栈**：与虚拟机栈作用相似，虚拟机栈为执行Java方法服务，而本地方法栈为执行Native方法服务
5. **程序计数器**：`当前线程所执行字节码的行号指示器`。每一个线程都有一个独立的程序计数器，线程的阻塞、恢复、挂起等一系列操作都需要程序计数器的参与，因此必须是线程私有的

- 垃圾回收
  - `程序计数器、虚拟机栈、本地方法栈是线程私有的`，所以会随着线程结束而消亡。 Java `堆和方法区是线程共享的`，在程序处于运行期才知道哪些对象会创建，这部分内存的分配和回收都是动态的，垃圾回收所关注的就是这部分内存
- `执行引擎`：执行方法中代码时，代码通过执行引擎执行中的“解释器”执行；方法中经常调用的代码，即热点代码，通过“即时编译器”执行，其执行速度非常快

> ##### 类加载的五个过程
>
> 1. ==加载==：类加载器获取二进制字节流，将静态存储结构`转化为方法区的运行时数据`结构，并生成此类的Class对象
> 2. ==验证==：验证文件格式、元数据、字节码、符号引用，确保Class的字节流中包含的信息符合当前虚拟机的要求
> 3. ==准备==：为`类变量分配内存并设置其初始值`，这些变量使用的内存都将在方法区中进行分配
> 4. ==解析==：将常量池内的`符号引用替换为直接引用`，包括类或接口的解析、字段解析、类方法解析、接口方法解析
> 5. ==初始化==：前面过程都是以虚拟机主导，而初始化阶段开始执行类中的 Java 代码
>
> - 内存区域：数据分区域存储，强调对内存空间的划分
> - 内存模型：JMM，JVM在内存中的工作方式

###### 2、对象

==对象访问定位==:  JDK8 之前的内存区域

- reference：指向对象的引用，句柄或直接指针的方式访问对象
  - 句柄：reference中存放句柄地址。java堆中有句柄池（存放到实例数据的指针和到类型数据的指针）
  - 直接指针：reference存放对象地址。java对象中有到对象类型数据的指针

==对象内存布局==： 

对象在内存中存储布局：对象头、实例数据、对齐填充

- 对象头
  - 一部分数据：存储对象自身的运行时数据（哈希码、GC分代年龄、锁状态标记、线程持有的锁、偏向线程ID、偏向时间戳等），MARK WORD
    另一部分：类型指针(`类型数据`)，对象指向它的类元数据的指针，通过这个指针来`确定对象是哪个类的实例`。（注：java数组对象头会记录数组长度，而普通java对象虚拟机会通过元数据信息判断对象大小）
- `实例数据`
  - 真正存储的有效信息，程序中定义各种类型字段内容
    存储顺序会有分配策略，long/double、int、shorts\chart、byte\boolean、opps,然后父在子前
- 对齐填充
  - 占位符作用：对象起始地址（对象大小）必须是8字节的整数倍，不够时，对其填充。对象头正好是8字节的一倍或两倍



| ![](./狂神说JavaSE基础.assets/jvm.png) | ![](./狂神说JavaSE基础.assets/v2-7a7c516c0aeb622705c86fd9b5e8c44a_r.jpg) |
| -------------------------------------- | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/aa.png)  | ![](./狂神说JavaSE基础.assets/bb.png)                        |
| ![](./狂神说JavaSE基础.assets/21.jpg)  | ![](./狂神说JavaSE基础.assets/24.png)                        |



### 3、多维数组

数组里的每个元素，又是一个数组。`int[][] array = {{1,2},{2,3}}`；  `int[2][5]   2行5列队数组`

| ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-27_20-42-35.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-04_16-44-37.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |

### 4、Arrays工具类、冒泡排序

> Arrays类中的方法是静态方法，使用时可直接使用类名调用，而不用使用对象调用

工具类，专门操作数组。[DOM EventListener事件传递有两种方式：冒泡与捕获](https://www.runoob.com/js/js-htmldom-eventlistener.html)    [数据结构常见的八大排序算法](https://www.cnblogs.com/hokky/p/8529042.html)  [十大排序算法](https://blog.csdn.net/qq_51664685/article/details/124427443)  [ 十大常用经典排序算法总结](https://blog.csdn.net/weixin_42711189/article/details/116351162)  

`冒泡排序是最出名的排序算法之一，有8大排序算法。理解：2层循环，外层表示第几轮排序，里层比较：两个依次比较，然后移动`

[二分查找](https://www.bilibili.com/video/BV1H64y1R7Ax/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd)

| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-17_09-07-27.jpg) | ![]()                                                        |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-17_09-44-09.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-27_22-10-43.jpg) |

```java
public class Array {
    public static void main(String[] args) {
        //测试排序方法,返回一个排序后的数组
        int[] a = {1, 23, 45, 12, 4433, 1, 32, 424, 12, 4, 44, 5, 665};
        int[] sor = sort(a);
        System.out.println(Arrays.toString(sor));
    }

    //冒泡排序
    //1、比较数组中，两个相邻的元素，如果第一个比第二个数大，就交换他们的位置
    //2、每一次比较，都会产生出一个最大，或者最小的数字
    //3、下一轮则可以少一次排序
    //4、依次循环，直到结束
    public static int[] sort(int[] array) {
        //加一个临时变量，存比较的数据
        int temp = 0;
        //外层循环，判断要走多少次
        for (int i = 0; i < array.length - 1; i++) {
            //内存循环，比较判断两个数，如果第一个数，比第二个数大，则交换位置
            for (int j = 0; j < array.length - 1 - i; j++) {
                if (array[j + 1] > array[j]) {  //如果后一个数大于当前数，就交换位置。
                    temp = array[j];            //当前数给临时变量
                    array[j] = array[j + 1];    //大的数赋给当前数
                    array[j + 1] = temp;
                }
            }
        }
        return array;                           //交换完后，返回出去
    }
}
```
### 5、稀疏数组
是一个数据结构。压缩数组，便于保存。  [五子棋](https://www.bilibili.com/video/BV12J41137hu?p=59&vd_source=7346303e5e18677d7261c2c0c109ecfd)
| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-17_09-49-35.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-17_09-52-01.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |

### 6、数组与排序

[西部开源Java之数组与排序](https://www.bilibili.com/video/BV1T4411A7Fy/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd)

# 6、对象

md: [java知识汇总](.\java知识汇总)   [对象知识汇总](.\对象知识汇总) 

> 用类组织代码,用对象组织数据：  **类组织行为，对象组织数据**
>
> - **类回答"这类东西能做什么、必须满足什么规则"，对象回答"此刻这个具体的东西是什么状态"。** 
> - 代码按类分层分职责，数据按对象聚合带约束，程序的可读性和可维护性基本就立住了

### 类
理解面向对象：物以类聚； 先考虑问题该怎么分类； 例如盖楼要分工程部、设计部等。面向对象解决复杂的问题。 ==类组织代码，对象封装数据； 类是对象的抽象==
`封装：就是把数据包起来，不想让钱暴露在外面。留一个口把钱取出来。多态：同一个事物有多种形态，不同的人，通过学习这个方法，有的学的好。 都是人，表现的形态不一样`; 同一个行为具有多个不同表现形式;  更进一步：  同一个接口，使用不同的实例执行不同操作; 例如打印机

- 多态存在的三个必要条件：继承、重写、父类引用指向子类对象：`Parent p = new Child()`
- 多态的实现方式：重写、接口、抽象类和抽象方法
- 对象可以作为参数传给方法，就可以调用对象的属性和方法

| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-17_10-04-30.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-17_10-19-51.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-17_10-20-37.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-27_23-36-03.jpg) |
| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-17_15-14-13.jpg) | ![非静态方法是类实例化后才有](./狂神说JavaSE基础.assets/Snipaste_2023-05-28_17-10-44.jpg) |
| ![有/无返回值](./狂神说JavaSE基础.assets/Snipaste_2023-12-11_11-10-08.jpg) | ![非静态方法调用](./狂神说JavaSE基础.assets/Snipaste_2023-12-11_11-23-17.jpg) |
| ![引用传递](./狂神说JavaSE基础.assets/Snipaste_2023-05-28_22-34-41.jpg) | ![]()                                                        |

#### 静态方法

[值传递-引用传递 ](https://www.bilibili.com/video/BV12J41137hu?p=62&spm_id_from=pageDriver&vd_source=7346303e5e18677d7261c2c0c109ecfd)  [In word错误](https://blog.csdn.net/wfxyjsjwjs/article/details/110502575)   [JAVA 类中的成员变量Fields和属性Properties区别](https://blog.csdn.net/xiyafei122/article/details/117341262)

> Arrays类中的方法是==静态方法==，使用时可直接==使用类名调用==，而==不用使用对象调用==
>
> 
>
> 非静态和静态方法相互调用规则: 
>
> - 核心规则只有一条：静态方法里没有 `self`/`this`，所以它想调用实例方法，必须先拿到一个实例引用；
> - 反过来，实例方法调用静态方法毫无障碍。 所有细节都是这条规则的推论
>
> 静态方法和类一起加载，出来的时间早； 非静态方法是对象创建以后才存在
>
> 1. 非静态调非静态（同类）：直接写方法名调用。
> 2. 非静态调静态（同类）：也可以直接调用。
> 3. 静态调非静态（同类）：不行，必须先 `new` 对象再通过对象调用。

1. 结束方法并==返回一个值==：方法有返回类型（如 `int`、`String`）时，必须用 `return 值;` 返回匹配类型的数据，如 `return a + b;` 先计算表达式再返回结果。
2. 结束方法但==不返回数据==：`void` 类型方法用 `return;` 直接退出，常用于提前结束，如条件不满足时终止执行。

`return` 结束当前方法，`break` 结束当前循环、`continue` 跳过本次循环进入下一次

> 1. ==静态方法调用==：有static   在另一个类中调用Student.sya() ;  类名.方法      ==非静态方法==：没有static，调用要实例化类 Student stu=new Student();   stu.sya()      //new student().say()
>    1. 静态方法不能调用非静态方法：因为静态方法和类一起加载，而非静态方法在类实例化之后才存在
>    2. 静态方法和类一起加载， `非静态方法：类实例化后才存在`
>    3. 对象类型：对象是哪个类的实例   `变量类型 变量名=变量值; 对象类型 对象名 = 对象值`
> 2. 实参：调用方法时实参才传给形参
> 4. 类和对象的创建
>    1. 类里面只有属性和方法
>    2. 一个类只能有1个public class，但能有多个class
>    3. 成员变量Fields：就是定义的字段name、age、gender（没有get/set）； **属性Properties**：有get/set
>    4. 类是抽象的，要实例化,类实例化后返回一个自己的对象,同一个类产生不同的对象，小明小红
>    5. 类是模板，有多个属性，属性不能写死
>    6. ==使用new时==，除了分配内存空间，还会给对象默认初始化，以及对类中构造器的调用

#### 值传递和引用传递

值传递：传递值。      引用传递：一般传递的是对象，本质还是值传递。

> 1. 使用new创建对象时，会给对象分配默认的值和空间。

```ts
//一个项目应该只存在一个main方法S
public class Application {
    public static void main(String[] args) {
        //类：抽象的，要实例化,类实例化后返回一个自己的对象。
        //xiaoming对象就是一个Student类的具体实例
        Student xiaoming = new Student();

        xiaoming.name="小明";
        System.out.println(xiaoming.name);

    }
}
```

### 创建对象

> ==new创建对象时==，除了==分配内存空间==，还进行==默认初始化==，以及==调用类中构造器==
>
> - `类中的构造器也称为构造方法`，是创建对象时必须要调用的

#### ==构造器==

`alt + insert` 生成构造器， ==Constructor==

构造方法（构造器）：㈠新建一个类，里面什么不写`public class Person{}`，依然能new一个方法`Person person = new Person();` ，说明存在一个空的Person()方法。`一个类，即使什么都不写，它也会存在一个方法。`  无参、有参构造器

- java文件编译后生成class文件，打开class文件： 打开项目结构，Modules,添加out目录，左边窗口就可以看到编译后的class文件
- 创建对象时调用构造器： 是为了==让对象在诞生那一刻就完成初始化，保证它一开始就处于可用状态。== 如果只分配内存而不初始化，对象里的成员变量会停留在默认值（如 `null`、`0`、`false`），后续必须手动赋值才能用，容易遗漏，也会让代码变得松散。
  - 构造器是用来初始化值


> 1. 构造器也叫构造方法，是在创建对象时必须要调用的
> 2. 构造器作用：
>    1. 无返回值、和类名同名的方法   `public Person(){}`
>    2. 使用new关键字，必须要有构造器； `new一个对象时，本质是在调用构造器`(==通过new调构造方法==)。  无参数构造器public Person() {}、有参构造 
>    3. ==㈡用来初始化一些信息，给对象一些默认值==  无参： this.name等于类的字段`this.name = "qinjiang";` 有参：`this.name = name;`
> 3. ==㈢定义了有参构造，无参构造就没了，想使用无参构造，无参构造就必须显式的定义==,  方法的重载
>    1. public Person(){},定义一个空的无参  
> 4. `构造器特点：1、和类名相同，2、没有返回值。`         
> 5. `alt + insert` 生成构造器。   ==Constructor==

有参构造：public Person(String name){this.name = name}

```java
public class Person {
    String name;  //this.name等于类的字段
    //无参数构造器；可以初始化一些信息，就像游戏有初始值一样
    public Person() {
        this.name = "qinjiang";
    }
    //有参构造：定义了有参构造，想使用无参构造，无参构造就必须显式的定义
    //String name 等于传进来的name
    public Person(String name) {  //上面有一个参数String name,所以就重载，会执行有参数的方法
        this.name = name;  //第一个name指上面的类属性(String name)，后面的name代表传进来的参数name
    }
}
```
`this.name=name;`  this.name是对象本身的name ， 右边是参数传进来的name

- 有参构造器
- 定义了有参构造，想使用无参构造，无参构造就必须显式的定义

| ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-29_09-17-51.jpg) | ![类是模板属性不能写死](./狂神说JavaSE基础.assets/Snipaste_2023-12-11_12-05-33.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2023-12-11_15-21-09.jpg) | ![]()                                                        |
| ![定义了有参构造,无参构造就必须显式的定义](./狂神说JavaSE基础.assets/Snipaste_2023-05-29_11-53-50.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-29_12-04-40.jpg) |
| ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-29_09-19-09.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-29_09-23-56.jpg) |

#### 创建对象时内存分析

对象内存分析：栈、堆(堆里有一个特殊区域叫方法区，静态方法区和类一起加载，这样后面的所有对象都能访问它)；`栈里面存方法和对象的引用，具体的对象在堆中，所以对象是通过引用来操作的。栈->堆，引用指向对象的地址，真实操作的是堆`。堆里面存具体创建出来的对象和数组。
`new一个pet动物类，会产生不同的对象cat\dog,因为它们是堆中不同的区域，不同的地址。`

| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-17_17-03-38.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-29_15-29-18.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-29_15-39-11.jpg) | ![]()                                                        |

### OOP三大特性(封装继承多态)
#### 1、封装_属性私有
[setter和getter方法](https://www.cnblogs.com/hissia/p/5419793.html)   [JavaScript对象添加getter与setter的5种方法](https://baijiahao.baidu.com/s?id=1619262495795436631&wfr=spider&for=pc)   [封装性、getter方法setter方法、以及构造方法的作用](https://blog.csdn.net/TFHoney/article/details/123433091)  
<span style="color:red;font-size:18px">封装：高内聚、低耦合。封装针对属性。 核心：属性私有 `private String name;`  get、set；</span>

> 1. 封装：`private String name；`属性私有，私有属性不能直接调用：s1.name就报错。`要提供可以操作私有属性的方法(get/set)`。`提供公共的方法去获取私有属性`
>    1. 例如拿遥控器换台，没必要知道电视里面是什么； age.sout
>    2. 封装一般针对的是属性，方法不用封装； 封装的核心是==㈠属性私有 private==
>    3. ==㈡get/set==： ==给私有属性提供一些，可以操作这个私有属性的方法==(因为私有属性即使new了，也不能使用)

> 1. 私有属性不能直接调用：s1.name就报错。这样就要提供可以操作私有属性的方法。`提供一些public的get、set方法。`
> 2. 封装好处
>    1. 提高程序安全，保护数据
>    2. 隐藏代码实现细节。例如：age属性，set方法里设置一些不合法age检验。大于999的不合法。
>    3. 统一接口。所有的方法都是get、set，用户调用的接口就是这2个。

```java
//Application.java main方法
//一个项目应该只存在一个main方法S
public class Application {
    public static void main(String[] args) {
        Student s1 = new Student();
        //私有属性，不能直接s1.name访问了，但能通过getName()获得属性
        //提供一些公共的方法去获取私有属性
        s1.getName();
        s1.setName("小日本");
        System.out.println(s1.getName());
    }
}
```

```java
//Student类
public class Student {
    //属性私有
    private String name;
    private int age;

    //要访问私有属性，就要提供一些可以操作这个属性的方法！提供一些public的get、set方法    //
    //get 提供一些公共的方法去获取私有属性
    public String getName() {
        return this.name;
    }
    //set 给数据设置值，小日本传给name，然后this.name="小日本"，类的name就被赋值。
    public void setName(String name) {
        this.name = name;
    }
}
```

封装： 属性私有， `private int id;`

- 提供一些公共的可以操作私有属性的方法： get、set 
- 隐藏数据的属性，避免直接访问

| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-17_17-20-09.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-30_13-16-27.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-30_13-26-11.jpg) |                                                              |

#### 2、继承

[继承,组合 ](https://www.cnblogs.com/waller/p/11247101.html)  [类图(Class Diagram)](https://www.cnblogs.com/hongguang-kim/p/5698710.html) [ UML六大关系](https://blog.csdn.net/Valhalla_God/article/details/121682323)  [依赖、关联、聚合、组合_组合](https://blog.csdn.net/lwwl12/article/details/82463441)  

[Java类与类之间的关系（关联、组合、聚合、依赖、继承、实现）](https://blog.csdn.net/qq_36944952/article/details/125023259)
[ Object类中的Clone方法 和Cloneable接口之间的关系](https://blog.csdn.net/m0_60358315/article/details/125772395)    [包的使用与继承](https://blog.csdn.net/m0_68840064/article/details/127717566)   [不同包之间的继承](https://www.cnblogs.com/baby-zhude/p/8017758.html)
<span style="color:red;font-size:18px">继承： 子类继承父类的方法和属性，private不能继承；   类多了也要抽象，例如人又分不同国家，不同民族。</span>

> 1. 所有类默认直接或间接继承==㈢Object类。ctrl + h 显示继承关系==
>    1. 子类继承父类的方法
>    2. 单继承：1个儿子有1个爸。  多继承：一个子类有多个父类。
>    3. 私有的东西不能被继承
>    4. 组合：Student类里包含Person类； 类和类之间关系还有==继承、依赖、组合、聚合==等
> 2. ==㈠子类继承父类的public方法和属性==, ㈡私有的不能继承private， [Java 修饰符](https://www.runoob.com/java/java-modifier-types.html#protected-desc)
>    1. public 、 private、 protected 、 default(什么也不写int name)
> 3. ㈣java中，==所有的类，都直接或间接继承Object==

```
public class Student extends Person{}
```

| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-17_23-53-49.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-30_19-55-41.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |

##### super和this

[this 和 super](https://developer.aliyun.com/article/1669507)  [继承和多态](https://cloud.tencent.com/developer/article/2603004)   [继承](https://cloud.tencent.com/developer/article/2542535)     [ Super关键字的使用](https://blog.csdn.net/cqq19990909/article/details/126920210) 

<span style="color:#ff00ff;font-size:18px">super：调用父类的属性、方法、构造器。super.print(); this.print()； super() ； this() </span>

- `super`指代父类,是用来访问父类的;    而this指代当前类
- super指向父类对象,用于访问父类成员；  this指向当前对象,用于访问本类成员
- super用来访问⽗类继承下来的方法和属性；  this用来访问本类的方法和属性
- super用于访问父类（超类）的成员： 属性、方法、构造器

new子类时，先执行父类无参构造(隐藏的:super())

- 父类写了有参构造,无参构造就没了,子类也没法调用父类无参构造
- 要么给父类补回无参构造，要么让子类显式调用父类的有参构造。

> ==super==：(this调用当前的) ==㈠调用父类属性、方法、构造器==( ㈡ 父类private的不行,protected可以)，super要写在方法里           
>
> - 父类属性super.name ;  父类方法super.print()   父类构造器super() 
> - 当前类无参构造this()
>
> 1. `调父类方法 super.print()`  ,this.pring()调当前类方法，只写print（），搞不清调谁的方法
> 1. 实例化对象时，调用父类无参构造器(子类有隐藏方法super());   `调父类属性、方法、构造器`
> 1. ==㈢new一个子类对象时，先执行子类构造器中，隐藏的父类无参构造super()，再执行子类无参构造==
>
> super注意点：
>
> 1. ㈣==super()  显式调用父类的构造器，必须放在子类构造器里面的第一行==。
> 2. super必须只能出现在子类的方法或者构造方法中
> 3. super和this不能同时调用构造方法，因为它们都要在第一行
>
> this vs super:
>
> 1. 代表对象不同：this：谁调用它就是谁。super：代表父类对象的引用。
> 2. 前提：this：没有继承也能使用。 super：只能在继承条件下才能使用。
> 3. 调用构造方法的区别：this():调用本类的构造方法    super()调用父类的构造方法。

1. super==出现在实例方法和构造方法中==
2. super的语法是“super.”和“super()”
3. super不能出现在静态方法中
4. super==大部分情况下是可以省略的==。
   1. 当父类和子类的方法名或者变量名相同时，要加super
5. new一个子类对象时，==先执行隐藏的父类无参构造==  super()，再执行子类无参构造
6. ==super()必须在构造方法的第一行==，是为了先初始化父类型特征，一般情况下super是默认不写的，默认不写系统会自动送你一个super

| ![super调父类属性](./狂神说JavaSE基础.assets/Snipaste_2022-07-18_08-00-07.jpg) | ![super调父类方法](./狂神说JavaSE基础.assets/Snipaste_2023-05-31_16-59-36.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![new一个子类对象，先执行父类无参构造](./狂神说JavaSE基础.assets/Snipaste_2023-05-31_17-19-59.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-05-31_17-34-00.jpg) |
| ![super()必须在构造方法第一行](./狂神说JavaSE基础.assets/Snipaste_2023-07-20_12-48-24.jpg) |                                                              |

##### 方法重写

[好：父类与子类的引用赋值关系](https://blog.csdn.net/weixin_42929607/article/details/107168033)  

`子类继承父类，重写父类的方法，方法体不同。`   [Java 重写(Override)与重载(Overload) ](https://www.runoob.com/java/java-override-overload.html)   [Java中方法重写和方法重载的6个区别](https://zhuanlan.zhihu.com/p/455750710)  [引用传递](https://blog.51cto.com/u_15697790/5419611)  [继承特性以及重写的内存分析](https://blog.csdn.net/qq_41485414/article/details/83022703)  [Object中的clone()方法_浅克隆和深克隆](https://blog.csdn.net/m0_59841734/article/details/126610489) 

`1、有static，  无static的方法重写    2、private方法不能重写    3、修饰符： 重写范围可以扩大但不能缩小 (子类的修饰符范围要比父类大)`

总结：方法有==static==：父类的引用指向子类

- `静态方法的调用`只和左边定义的数据类型有关
- 非静态方法的调用： 重写只和非静态方法有关
  - ==无static==：子类重写父类的方法

修饰符范围、抛出异常的范围

> 1. 重写：需要有继承关系，子类重写父类的方法！跟属性无关
>    1. `有static  B b = new A(); 父类的引用指向子类对象。 左边是栈引用，右边是堆对象`    ==父子类的同名静态方法调用时，只和左边定义的数据类型有关==
>       1. 引用传递产生的原因是同一块堆内存可以被多个栈内存指向
>       1. 引用传递，垃圾产生: 一个栈内存只能保存一个堆内存的地址，如果发生改变，之前指向的堆内存就会成为垃圾空间
>    1. 去掉static，就出现重写图标。`子类重写父类的方法，重写只和非静态方法有关,public方法；`   privated私有方法不能重写
>    
> 2. 方法名必须相同，参数都一样；`方法名、参数都一样`  重载：`方法名相同，参数不同`
>    1. 注解：有功能的注释
>    2. super.test()；重写默认调用父类的方法，可以重写自己的方法 
>    3. 重载本类的，重写父子类才有
>
> 3. 参数列表必须相同
> 4. 修饰符：重写范围可以扩大但不能缩小，例如：public不能缩小private。 `public > protected > default >private`
>    1. private不能重写
>
> 5. 重写可能会抛出异常：范围可以被缩小，但不能扩大。例如：ClassNotFoundException ---> Exception(范围大) `不能抛出新的检查异常，或者比被重写方法更加大的异常`
>
> 重写：子类的方法和父类必须一致；方法体不同（里面的代码不同）。
>
> ==为什么要重写==：父类的功能，子类不一定需要，或者不一定能满足。   `子类可以根据需要，定义特定于自己的行为`
>
> 1. java的方法调用，运行时和动态对象绑定`s1.eat(),s2.eat()`。多态是方法的多态。//父run(),子
> 2. 父类的引用指向子类类型 `Person s2 = new Student()`
> 3. 对象能执行哪些方法，主要看对象左边的类型。【子类有的方法，父类没有，父类就不能执行子类的方法】
>

==有static==：static 用来声明独立于对象的==静态方法==， 类的方法；   ==㈠ 父类的引用指向子类对象，  方法的调用只和左边定义的数据类型有关==； 类的方法类一加载就出来了

- `静态方法的调用`只和左边定义的数据类型有关
- 非静态方法的调用： 重写只和非静态方法有关

```java
public class B {
    void test() {
        System.out.println("B方法");
    }
}

class A extends B {
    void test() {
        System.out.println("A方法");
    }

    public static void main(String[] args) {
        A a = new A();
        a.test();		//A方法
        B b = new A();
        b.test();		//A方法,子类重写父类方法
    }
}
```

```java
//一个类有多个对象
Ball ball = new Ball();
Ball ball2 = new Ball();
ball.name = "篮球";
ball.size = 11;
ball2.name = "足球";
ball2.size = 22;
//栈区：ball2的引用指向ball的引用
ball2=ball;
ball2.size=6666;
System.out.println(ball2.size);
```

| ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-01_15-19-31.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-05_12-55-12.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-18_14-08-12.jpg) | ![](./狂神说JavaSE基础.assets/v2-8ecdbd775731153ac0fb1d89c579a991_r.jpg) |
| ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-01_16-02-36.jpg) |                                                              |



==无static==：==㈡去掉static， 子类重写了父类的方法==。`重写只和非静态方法有关。重写不能是private方法` ； 重写后都走的子类的方法，子类重写了父类的方法
对象能执行哪些方法，主要看对象左边的类型，和右边关系不大。
子类能调用自己和继承父类的方法；  父类可以指向子类，但不能调用子类独有的方法。

#### 3、多态

[Java 多态](https://www.runoob.com/java/java-polymorphism.html)  [Java多态内存分析 ](https://www.dandelioncloud.cn/article/details/1584000683089317889)  [java中引用类型有哪些](https://so66.cn/33397.html)  [深入理解Java引用类型](https://blog.csdn.net/guanshengg/article/details/126502906)  [ Java 中引用与指针的关系](https://blog.csdn.net/Chenhui98/article/details/126864649) [Java引用类型](https://www.cnblogs.com/hetaoyuan/p/10582553.html)  [Java的四种引用类型](https://blog.csdn.net/Fantasy_Lin_/article/details/105004740)  [java的引用类型](https://worktile.com/kb/ask/33666.html)

总结：==多态存在条件：继承、重写、父类的引用指向子类==

- 多态的核心： ==父类引用指向子类对象==
- 多态说的是同`一个父类类型的引用`变量，在`运行时可以指向不同子类对象`，从而调用出不同的行为

> `对象的实际类型是确定的，但指向对象的引用类型有很多。一般是父类、有关系的类。`
>
> 1. java中的==引用类型是指指向对象的指针==，它们允许程序员以更高效的方式操作对象
> 1. 父类的引用指向子类的类型  	    Person s2 = new Student()
>    1. ==父类的引用指向子类对象==	Person person = student
>       1. 当使用多态方式调用方法时，首先检查父类中是否有该方法，如果没有，则编译错误；如果有，再去调用子类的同名方法
>       1. 多态可实现动态编译：类型只有在执行中才能决定； ㈠ 一个对象的实际类型是确定的，==但指向的引用类型就不确定了==  Person s2 = new Student()
>       1. 父类指向子类，但不能调用子类独有的方法；㈡  ==对象能执行哪些方法，主要看对象左边的类型==，和右边没关系，左边类型有的方法才能调用； Person s2 = new Student()
>    2. ==多态是同一行为具有不同形态(表现形式)==;    ==同一行为发生在不同对象上会产生不同的结果==  例：都是打印，能打黑白和彩色； 按F1弹出的帮助不同
>       1. ㈢==多态的实现方式==：
>          1. 重写
>          2. 接口： 例如生活中不同的插座， 就是一些方法特征的集合，但没有方法的实现
>          3. 抽象类和抽象方法
>
> 多态注意事项：
>
> 1. 多态是方法的多态，属性没有多态
> 2. 父类和子类，有联系，例如：狗转成猫不行，会报错误：类型转换异常 classCastException
> 3. 存在条件：继承关系，方法需要重写，父类引用指向子类对象！Father f1 = new Son()
>

`(Student) s2`： 父类型 s2 强转为子类型 Student

| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-18_14-57-56.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-12-14_14-11-26.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![对象能执行哪些方法，主要看对象左边的类型](./狂神说JavaSE基础.assets/Snipaste_2023-06-02_09-48-13.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-02_09-47-04.jpg) |
| ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-02_09-52-09.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-02_10-52-21.jpg) |

##### instanceof和类型转换

[instanceof 运算符](https://www.runoob.com/java/java-operators.html)    [ instanceof用法](https://blog.csdn.net/mingyuli/article/details/120411767)

先用==instanceof 判断==左右两边有没有关系 ->  ==再类型转换==，强制转换可能丢失自己的方法

强制类型转换是==为了方便方法的调用==

instanceof运算符: 检查左边对象，是不是右侧的对象，是就为真

> 1. ==**引用类型之间的转换**==
> 1. instanceof 判断一个对象是什么类型。 判断对象是否是指定的类型，如果是返回 true；  判断左边的对象是否是右边类的实例  ㈠==先instanceof, 判断2个类之间是否有父子关系==。 比较要2边有关系，没关系会报错。`x instanceof y //x是y的子`
>    1. 测试左边的对象是否是右边的类的实例
>    1. 两边必须是同种类或存在继承关系,也就是说需要位于同一个继承树
>
> 1. Person  s1 = new Student()；`㈡ 类型转换： Student转Person，低转高不需要强制转换。 (Student) s1` Student s2 = (Student) s1,`s1强制转为Studeng方法`
>
> 总结：
>
> 1. 父类引用子类的对象
> 2. 子类转父类，不用强制转换。 父类要运行子类特有方法，要强转为子类
>    1. 子类转父类，会丢失自己的方法
>    2. 父转子类，强制转换，会丢失父类的方法(父类的方法不能用)。
> 3. 作用：基本类型的转换是为了方便计算，这里的类转换，为了==方便方法的调用==(不用重新new一个对象，升级或降级就可以调用转换后类的方法，减少重复代码)
> 4. 抽象类比多态更抽象(类的抽象)，接口比抽象类更抽象。

| ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-02_11-17-18.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-02_11-51-49.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-02_11-51-03.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-12-14_14-39-28.jpg) |

##### 值传递_引用传递

[Java的值传递和引用传递](https://zhuanlan.zhihu.com/p/89794950?utm_id=0)    [彻底明白Java的值传递和引用传递](https://xuliugencn.blog.csdn.net/article/details/83508006?spm=1001.2101.3001.6650.3&utm_medium=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-3-83508006-blog-84146202.235^v38^pc_relevant_sort_base1&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-3-83508006-blog-84146202.235^v38^pc_relevant_sort_base1&utm_relevant_index=6)   [引用传递](https://blog.csdn.net/u010454030/article/details/84146202)  [值传递和引用传递](https://www.cnblogs.com/xiaohu666/p/17335240.html)  [值传递和引用传递](https://www.cnblogs.com/konglxblog/p/16456809.html) [值类型和引用类型](https://blog.csdn.net/xinlingmen/article/details/106279141)  

[简单名、全限定名、描述符、签名、符号引用、直接引用](https://blog.csdn.net/gg1229505432/article/details/121405221)   [全限定名](https://blog.csdn.net/weixin_36873225/article/details/117060872)  [JVM内存模型和类加载运行机制](https://zhuanlan.zhihu.com/p/500205913)  [类的直接超类的权全限定名](https://www.baidu.com/s?ie=UTF-8&wd=类的直接超类的权全限定名) 

**pass by reference** ；

1. ==形参与实参==
   1. 形参：只有在被调用期间才会分配内存空间 (生命周期开始)，在方法执行完成后，就会被销毁释放空间
   2. 实参：在方法被调用前就已经被初始化，并且在方法被调用时传入
2. ==Java的数据类型==
   1. 数据类型，是对内存的一种抽象表达, 程序由代码文件和静态资源组成 
   2. 数据类型实质上是相同类型的数据的存储形式
   3. Java的数据类型: 
      1. 基本类型: 四大类八种类型
      2. 引用类型：引用也叫句柄，引用类型，是在句柄中存放着,实际内容所在地址的==地址值==的一种数据形式, ==引用类型主要包括: 类、接口、数组== ； 
      3. 栈中有基本类型和对象句柄，基本类型又叫值类型，对象句柄又叫引用类型；java中的方法值中传值时，就有了值传递和引用传递
      4. 有了数据类型，JVM对程序数据的管理就规范化了，不同的数据类型，它的存储形式和位置是不一样的
3. ==JVM内存==
   1. java代码被编译器编译成字节码之后，JVM开辟一片内存空间（也叫运行时数据区），通过类加载器加到到运行时数据区来存储程序执行期间需要用到的数据和相关信息， 由以下几部分组成：栈、堆、方法区、本地方法栈、程序计数器
      1. 栈：
         1. 栈中存栈帧，==每个栈帧对应一个被调用的方法==，方法的调用过程对应栈帧在虚拟机中入栈到出栈的过程
         2. 栈是线程私有的，也就是线程之间的栈是隔离的；当程序中某个线程开始执行一个方法时就会相应的创建一个栈帧并且入栈（位于栈顶），在方法结束后，栈帧出栈
         3. ==栈帧中包括==: 局部变量表（存局部变量：非静态变量、函数形参）、指向运行时常量池的引用、 方法执行完的返回地址、 操作数栈、 附加信息
      2. 堆：
         1. 存储对象本身和数组，JVM只有一个堆，因此，堆被所有线程共享
      3. 方法区：
         1. 所有线程共享
         2. 存储的内容有：类的全路径名、类的直接超类的全限定名(包名+类型)、类的访问修饰符、类的类型（类或接口）、类的直接接口全限定名的有序列表、常量池（字段，方法信息，静态变量，类型引用（class））等
      4. 本地方法栈：
      5. 程序计数器：
4. ==数据如何在内存中存储==
   1. Java中的数据类型有基本数据类型和引用数据类型
   2. 基本数据类型的存储:
      1. 基本数据类型的==局部变量==: 写int age=50；分为两步，变量名及字面量值都==存储在栈中==，而且是真实的内容
         1. 基本数据类型的数据本身不会改变，当局部变量重新赋值时，并不是在内存中改变字面量内容，而是重新在栈中寻找已存在的相同的数据，若栈中不存在，则重新开辟内存存新数据，并且把要重新赋值的局部变量的引用指向新数据所在地址
      2. 基本数据类型的==成员变量==：类中定义的变量,  成员变量名和值都==存储于堆中==，其生命周期和对象的一致
      3. 基本数据类型的==静态变量==: 静态变量名以及值==存储于方法区的运行时常量池中==，静态变量随类加载而加载，随类消失而消失
   3. 引用数据类型的存储：
      1. Person per=new Person(); 分2步，`Person per;//定义变量   per=new Person();//赋值`
      2. 执行Person per;时，JVM先在栈的变量表中开辟一块内存存放per变量，在执行per=new Person()时（赋值时），JVM创建一个Person类的实例对象, 并在堆中开辟一块内存存储这个实例，同时把实例的地址值赋值给per变量
      3. 因此，对于引用数据类型的对象/数组，变量名存在栈中，变量值存储的是对象的地址，并不是对象的实际内容
5. ==值传递和引用传递==
   1. 值传递：  在方法被调用时，实参通过形参把它的内容副本传入方法内部，此时==形参接收到的内容是实参值的一个拷贝==，因此在方法内对形参的任何操作，都仅仅是对这个副本的操作，不影响原始值的内容
   2. 引用传递：方法调用时，==实参的地址==通过方法调用==被传递给形参==，在方法体内，形参和实参指向同一个内存地址，对形参的操作会影响真实内容

![JVM内存](./狂神说JavaSE基础.assets/static.jpg)

| ![](./狂神说JavaSE基础.assets/fream.jpg)          | ![](./狂神说JavaSE基础.assets/value_jubu.png) |
| ------------------------------------------------- | --------------------------------------------- |
| ![成员变量](./狂神说JavaSE基础.assets/member.jpg) | ![](./狂神说JavaSE基础.assets/dui.jpg)        |



### Static关键字 ( 修饰符 )

[Java 修饰符](https://www.runoob.com/java/java-modifier-types.html)  
静态区在堆里面。 ==static属性或方法是在方法区保存==。 

- 静态属性和静态方法==都存放在方法区，属于类本身(和类一起加载)==，全局只有一份，与对象实例无关
  - 静态属性和静态方法可==通过类直接调用==
- `静态方法`中想`访问实例`成员，必须先`创建对象`或通过`参数传入对象`引用
  - 因为类加载时还没有对象

`static属于类，不属于实例；   通过类调用变量   通过对象调用变量`

访问静态属性方法 -> 匿名代码块{} 静态代码块 构造方法执行顺序

> 1. ==静态属性==：㈠==静态变量可用类名访问==，  Student.age   
>    1. static属于类，不属于实例
> 2. ==静态方法调用==：随着类一起加载。==㈡ Student.go() 或 go()==
>    1. 非静态方法调用：要new个对象， new Student().run() ;   
>    2. ==非静态方法可访问类中的静态方法==： void run(){  go()  }
>    3. 静态方法中可调用静态方法：main也是静态方法， 静态方法中不能调用非静态方法，因为有静态方法时，非静态方法还没加载
>    4. `类变量：通过类调用变量；  （对象变量：通过对象调用）`
> 3. ㈢==匿名代码块== { }：创建对象时创建，在构造器之前
> 4. ㈣==静态代码块==：static{ } ; 类一加载就直接执行，只执行一次
>    1. 创建对象时调用顺序： 静态代码块 => 匿名代码块 => 构造方法； 静态代码块只执行一次
> 5. `静态导入包：import static java.lang.Math.random;`  ：导入math里面的random方法， 加static
> 6. final修饰的类不能被继承

> 1. 访问修饰符：   保护对类、变量、方法和构造方法的访问
>    1. public：	所有类
>    2. private：       同一类内可见
>    3. default：       同一包内可见
>    4. protected：   同一包内的类和所有子类可见
> 2. 非访问修饰符
>    1. final：==常量修饰符==; final 修饰的类不能被继承、修饰的方法不能被继承类重新定义，修饰的变量为常量不可修改
>    2. static：修饰类、方法和类变量
>    3. abstract ：用来创建抽象类和抽象方法
>    4. synchronized 和 volatile 修饰符，主要用于线程的编程。
> 3. 方法重写： 重写修饰符范围可以扩大但不能缩小 (子类的修饰符范围要比父类大)

```java
public class Person {
    {
        //{} 叫做代码块(匿名代码块)；为了方便初始化一些东西。  赋初始值
        System.out.println("匿名代码块");
    }
    
    static {
        System.out.println("静态代码块");
    }
    
    public Person() {
        System.out.println("构造方法");
    }

    public static void main(String[] args) {
        //执行main，查看代码块调用顺序
        Person person = new Person();
        Person person2 = new Person();
    }      
}       //先调用静态代码块 => 匿名代码块 => 构造方法；静态代码块只执行一次
```

| ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-02_16-48-03.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-02_16-55-33.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-02_17-03-45.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-07_10-32-18.jpg) |

### 抽象类和接口(==函数式、lambda==)

[C++ 数据抽象](https://www.runoob.com/cplusplus/cpp-data-abstraction.html)   

抽象把代码分离为接口和实现。

- 在设计组件时，必须保持接口独立于实现，这样，如果改变底层实现，接口也将保持不变
- 在这种情况下，不管任何程序使用接口，接口都不会受到影响，只需要将最新的实现重新编译即可

#### 抽象类

Java类是单继承，但接口可以多继承

> 1. ==抽象类==：不能new抽象类，只能靠子类去实现它(只能去new子类对象)，抽象类是一个约束。
> 2. ==抽象方法==：`抽象类里可写普通方法`，抽象方法必须在抽象类中
>    1. Java类是单继承，所以抽象类有局限性，但接口可以多继承。    //抽象类不重要，接口才常用。
>    1. ==㈠ 抽象类子类通过继承实现它的方法==，除非子类也是抽象类，子子类实现
>    1. `public class A extends Action{}`
>
>
> 思考：
>
> 1. 抽象类不能new对象，里面有构造器吗？
> 2. 抽象类存在的意义。

| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-19_17-59-21.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-02_20-10-51.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-02_20-25-37.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-02_20-29-13.jpg) |

```java
//加abstract，变成抽象类
//Java是单继承，所以抽象类有局限性，但接口可以多继承
public abstract class Action {
    //假设方法里没东西，只是一个约束，我们不想写，有人帮助实现就好了
    //如果写框架，只写约束就好了，方法让别人写
    //抽象方法，只有方法名字，没有方法的实现
    public abstract void doSomething();
}
```

子类继承抽象类，实现抽象类方法

```java
//继承抽象类，提示必须重写抽象方法
//抽象类的所有方法，必须由子类实现
//抽象类的所有方法，继承了它的子类，都必须要实现它的方法
public class A extends Action {
}
```

#### 接口

[Java 接口](https://www.runoob.com/java/java-interfaces.html)    [面向接口编程](https://www.cnblogs.com/huhu1203/p/7794915.html)  
[微服务接口设计](https://zhuanlan.zhihu.com/p/28310642)  [区域医疗卫生系统的接口规范、接口类型和接口设计方式](https://baijiahao.baidu.com/s?id=1749192087542689951&wfr=spider&for=pc)  [大型系统开放平台接口设计](https://zhuanlan.zhihu.com/p/150078662?utm_id=0)  [LabVIEW架构师必学OOP知识之接口设计决策](https://blog.csdn.net/counter555/article/details/127311930)  

总结：接口里的方法默认public abstract， 常量public static final；  `多继承要实现接口的全部方法`

> 1. 面向接口编程
>    1. 大型开发中，系统之间接口先设计好，文档定义好，然后找码农实现
>    2. 设计模式研究的就是：如何合理的去抽象
> 2. 接口是一个约束
>    1. 接口定义一些方法，让不同的人实现，==㈠ 接口中的方法其实都是抽象的public== abstract ，默认不写，void run();  常量都是public static final
>    1. ==㈡ 多继承== `public class UserServiceImpl implements UserService,TimeService`
>       1. ==要实现接口里定义的全部方法==
> 3. 接口不能被实例化，因为接口没有构造方法，
> 4. 实现接口，必须要重写接口里面的方法。

| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-19_19-07-15.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-03_12-03-04.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-03_12-03-49.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-03_12-08-45.jpg) |

接口类：

```java
public interface UserService {
    //接口里常量的默认定义,public static final int AGE = 99;
    //一般接口里写方法，没人会写常量
    int AGE = 99;
    
    //接口中的所有定义都是抽象的,都是public  abstract，不写，默认就是
    //public abstract  void run();
    //这里只有定义，没有具体的实现，所以接口都需要实现类，实现类名字Impl结尾
    void add(String name);
    void delete(String name);
    void update(String name);
    void query(String name);
}
```

用implements实现接口类，需要重写接口里定义的方法

```java
//用implements实现接口类，需要重写接口里定义的方法
public class UserServiceImpl implements UserService,TimeService {
    @Override
    public void add(String name) {
    }
    @Override
    public void delete(String name) {
    }
    @Override
    public void update(String name) {
    }
    @Override
    public void query(String name) {
    }
    @Override
    public void timer() {
    }
}
```

多继承：多个接口类，里面的方法是实现(上面)`public class UserServiceImpl implements UserService,TimeService `

```
public interface TimeService {
    void timer();
}
```

```java
//Person.java
public interface Person {}
interface Teacher {void run();}
interface Doctor{void go();}
class Swim {
    void fire() {}
}

//Student.java
public class Student extends Swim implements Person,Doctor,Teacher{
    //实现多继承接口的方法, 继承父类的方法和属性
    @Override
    public void run() {}
    @Override
    public void go() {}
    public static void main(String[] args) {
        Swim s = new Swim();
        s.fire();
    }
}
```

<span id = "jump">函数式编程</span>

##### 1、函数式编程

> 重点：jdk8函数式接口和Lambda 表达式

视频：[视频教程](https://www.bilibili.com/video/BV15S4y1v7MM?p=4&vd_source=7346303e5e18677d7261c2c0c109ecfd)  [Lambda表达式、函数式编程](https://www.bilibili.com/video/BV1Gh41187uR/?spm_id_from=333.788.recommend_more_video.0&vd_source=7346303e5e18677d7261c2c0c109ecfd)   

[Lambda表达式详解](https://www.cnblogs.com/knowledgesea/p/3163725.html)   [Java Lambda 表达式](https://www.runoob.com/java/java8-lambda-expressions.html)  [Java 8 新特性](https://www.runoob.com/java/java8-new-features.html)  [函数式编程 ](https://mp.weixin.qq.com/s?__biz=MjM5NTY1MjY0MQ==&mid=2650860571&idx=2&sn=48d9f58592a88f0e37271c100a1dc075&chksm=bd0179558a76f0433657838a379c7a03ee8ed095687868242f2d5ec94ae524fdaea8cca36f04&scene=27)  [ JAVA中Function的使用—Function<T, V> ](https://blog.csdn.net/weixin_44792849/article/details/127888526)
[Function接口](https://blog.csdn.net/qq_61592687/article/details/127722564)   [Java中的::_方法引用](https://blog.csdn.net/qq_51452131/article/details/127929327)   [函数式接口 ](https://www.cnblogs.com/lyq-9726/p/14948178.html)  [函数式接口 ](https://www.cnblogs.com/ashScc/p/15972683.html)  [Java 8 函数式接口](https://www.runoob.com/java/java8-functional-interfaces.html)  [Java语法笔记 ](https://www.cnblogs.com/newsea/p/4839540.html)  [Java BinaryOperator接口](https://geek-docs.com/java/java-basic-tutorial/g_binaryoperator-interface-in-java.html)  [函数式编程](https://www.cnblogs.com/openmind-ink/articles/15860100.html) [五种方式创建线程](https://blog.csdn.net/m0_63571404/article/details/127668856)

> 1. 函数式接口(Functional Interface)
>    1. jdk8以前，接口中只能有抽象方法，jdk8中，㈠ ==除了抽象方法，还可以有多个默认方法、静态方法==
>    2. 就是一个有且仅有一个抽象方法，但是可以有多个非抽象方法的接口（默认方法、静态方法），
>    3. @FunctionalInterface， 如果接口中只有一个抽象方法，默认是函数式接口
> 2. 函数式接口的使用
>    1. 可作为方法的参数和返回值类型
>    2. 三种调用方法
>       1. 用子类实现接口，new实现类再调用    `new MyInterfaceImpl().say()`
>       2. 匿名内部类方式：  new接口，里面实现方法；
>       3. 通过接口创建一个匿名内部类，并把这个类的实例赋值给一个变量
> 3. Lambda 表达式，也可称为闭包，它是推动 Java 8 发布的最重要新特性
>    1. Lambda 允许把函数作为一个方法的参数（函数作为参数传递进方法中）
>    2. JDK8提供了一些常用类型的 ㈡==函数式接口==，用来支持Java函数式编程，java.util.function包， 这些函数式接口分四种类型
>       1. Consumer：消费型接口，有参，无返回值， 消费给它传的参数
>       2. Supplier：供给型，没有输入，只有返回结果
>       3. Function：函数型接口，有输入T，有输出R  `Function<Integer,String>` 
>       4. Predicate：断言接口，有输入，返回true、false
>    3. **“语法糖”是指使用更加方便，但是原理不变的代码语法**， 从应用层面来讲，Java中的Lambda可以被当做是匿名内部类的“语法糖‘，但二者在原理上是不同的。

```java
public interface InterfaceDemo {
    void run();
    //默认方法
    public default void sing() {
        System.out.println("sing........");
    }
    //静态方法，可直接通过接口名调用
    public static void swim() {
        System.out.println("swim..........");
    }
    public static void main(String[] args) {
        InterfaceDemo.swim();
    }
}
```

| ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-27_16-42-29.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-27_16-46-47.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |

```java
//接口类
@FunctionalInterface
public interface InterfaceDemo {
    void say();
}
//测试Lambda
public class Test {
    public static void main(String[] args) {
        InterfaceDemo interfaceDemo =()->{
            System.out.println("say.........");
        };
        interfaceDemo.say();
    }
}
```

##### 2、方法引用

视频：[Java语法中的方法引用](https://www.bilibili.com/video/BV1je4y1c79s/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd) [双冒号::](https://www.bilibili.com/video/BV1Yu411W77v/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd) 

[System.out::println](https://blog.csdn.net/qq_36929361/article/details/84926277)   [Java8新特性](https://zhuanlan.zhihu.com/p/461812824)

方法引用根据Lambda表达式，所引用的函数式接口的上下文，==动态的进行类型匹配和方法的调用==； 用来简化代码

- 根据函数式接口里面方法要实现的参数的形式，来决定后面的调用
- 指向一个方法，具体表示哪个方法，看通过什么函数式接口接收的？（看方法形参和返回值，和函数式接口是不是对应）
  - ==根据函数式接口要实现的参数的形式，来决定调用哪个方法==


> - 通常使用lambda表达式来创建匿名方法。然而，有时候我们仅仅是调用了一个已存在的方法
>   - 
> - 方法引用是用来直接访问类或者实例的已经存在的方法或者构造方法。方法引用提供了一种==引用而不执行方法==的方式，它需要由兼容的==函数式接口构成的目标类型上下文==。计算时，方法引用会创建函数式接口的一个实例。
> - 注意方法引用是一个Lambda表达式
> - 当Lambda表达式中只是执行一个方法调用时，不用Lambda表达式，直接通过方法引用的形式可读性更高一些。方法引用是一种更简洁易懂的Lambda表达式
> - 函数式接口通常通过Lambda书写，方法引用根据lambda所引用的，函数式接口的上下文，动态的类型匹配和方法的调用；

下面的方法总结的有点不对，主要是还不懂：

> 1. ==静态方法引用== :  类名：：方法
>    1. 有lambda表达式
>    2. 已经存在静态方法
>    3. 静态方法签名（入参和出参）符合函数式接口中抽象方法的要求
>    4. 静态方法引用适用于lambda表达式主体中==仅仅调用了某个类的静态方法==
> 2. ==实例方法引用==： 先new个对象，其他和静态方法引用差不多
>    1. `构造函数本质上是静态方法，只是方法名字比较特殊`
>    2. 适用于lambda表达式的主体中==仅仅调用了某个对象的某个实例方法==
> 3. 对象方法引用：使用条件更加严格，先new个对象    对象名：：方法
>    1. `Mouse mouse2 = new Mouse();   Runnable runnable = mouse2::service;   runnable.run();`
> 4. ==构建方法引用==：分别调用不同的构造函数
>    1. 例：将ArrayList实例化，==调用它的构造方法==,`Collectors.toCollection(ArrayList::new)`
>    2. 适用于lambda表达式主体中==仅仅调用了某个类的构造函数返回的实例==
> 5. stream流应用

```java
public class TestUsb {
    static class Hello{
        static void a() {
            System.out.println("a1无参");
        }
        static void a(String s) {
            System.out.println("a2有参");
        }
    }
	//指向一个方法，因为Runnable没有入参，所以调用无参方法；如果改为Consumer，就调用有参方法
    public static void main(String[] args) {
        Runnable runable=Hello::a;
        runable.run();       //a1无参
        
        //Consumer<String> consumer = Hello::a;
        //consumer.accept("Hello");  a2有参
    }
}
```

[Java语法中的方法引用](https://www.bilibili.com/video/BV1je4y1c79s/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd)  [方法引用](https://www.cnblogs.com/bigfairy/p/14002058.html)

```java
public class Person {
    private String name;
    private Integer age;

    public Person() {
    }

    public Person(String name, Integer age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }

    public static int compare(Person a, Person b) {
        //先年龄比较，年龄相同则进行名字升序排列
        int r = a.getAge().compareTo(b.getAge());
        if(r!=0){
            return r;
        }else{
            return a.getName().compareTo(b.getName());
        }
    }

    public static int compare(Person a,Person b,Person c){return 0;}

    public Person concat(Person b) {
        //将2个人名进行连接：当前对象名称加上传入的对象名称
        this.setName(this.getName() + "," + b.getName());
        System.out.println(this);
        return this;
    }
}

```

```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;
import java.util.function.*;

public class Demo {
    public void case1() {
        List<Person> personList=new ArrayList<>();
        personList.add(new Person("Sam", 20));
        personList.add(new Person("Lily", 23));
        personList.add(new Person("Jack", 20));

        //传统写法
        personList.sort(new Comparator<Person>() {
            @Override
            public int compare(Person a, Person b) {
                return Person.compare(a, b);
            }
        });
        //Lambda写法
        personList.sort((a,b)->Person.compare(a,b));
        //方法引用写法，调用static静态方法，参数类型动态推断
        personList.sort(Person::compare);
        System.out.println(personList);
    }

    //stream流应用
    public static void case2() {
        List<Person> personList=new ArrayList<>();
        personList.add(new Person("Sam", 20));
        personList.add(new Person("Lily", 23));
        personList.add(new Person("Jack", 20));
		//遍历出来的每一个对象都调用System.out（也就是PrintStream类的一个实例）的println方法
        personList.stream().sorted(Person::compare).forEach(System.out::println);
    }

    //调用对象方法引用
    public static void case3() {
        List<Person> personList;
        personList = new ArrayList<>();
        personList.add(new Person("Sam", 20));
        personList.add(new Person("Lily", 23));
        personList.add(new Person("Jack", 20));
        Person p = new Person("ZhanSan", 0);

        personList.stream().sorted(Person::compare).forEach(p::concat); //对象方法引用  p::concat
    }
    
    //::new 实例化对象
    public static void case4() {
        List<Person> personList = new ArrayList<>();
        personList.add(new Person("Sam", 20));
        personList.add(new Person("Lily", 23));
        personList.add(new Person("Jack", 20));
        personList.add(new Person("老六", 1));
        //personList.stream().sorted(Person::compare).collect(Collectors.toList()).forEach(System.out::println);
        //将ArrayList实例化，调用它的构造方法
        personList.stream().sorted(Person::compare).collect(Collectors.toCollection(ArrayList::new));
    }

    //指代特定实例
    public void case5() {
        String[] stringArray = {"Barbara", "James", "Mary", "John", "Robert"};
        //原始写法
        Arrays.sort(stringArray, new Comparator<String>() {
            @Override
            public int compare(String a, String b) {
                return a.compareToIgnoreCase(b);
            }
        });
        //Lambda写法
        Arrays.sort(stringArray, (a, b) -> a.compareToIgnoreCase(b));
        //::写法 String指代a对象
        Arrays.sort(stringArray,String::compareToIgnoreCase);
    }

    public static void main(String[] args) {
        case3();
    }
}

```



##### 3、匿名内部类

==总结：作用、使用、$1.class==

没有名字初始化类； `正常： Apple apple = new Apple()   匿名时：new Apple()`

没有名字, 只能使用一次, 针对抽象类和接口使用匿名内部类(==new的同时，把方法实现了==)； 
`Demo$1.class 是匿名内部类编译出来的类，` `javap -v Demo.class 将class文件反编译成字节码`

1.  ==作用==：很多类只用1次，写抽象类，再用继承子类实现它的方法麻烦
   1. 匿名内部类只用一次
   2. 没有名字初始化类，==不用将实例保存到变量中==
2. 使用匿名内部类
   1. ==抽象类==上使用匿名内部类
   2. ==接口==上使用匿名内部类
   3. ==Runnable接口==的匿名内部类实现
   4. ==其实任何类都能用匿名内部类== `new Apple().eat()`

```java
public abstract class Person {
    public abstract void talk();
}
 
public class Demo {
    public static void main(String[] args) {
        Person p = new Person() {	//抽象类上使用匿名内部类
            public void talk() {
                System.out.println("说些什么....");
            }
        };
        p.talk();
    }
}
```



##### 4、普通接口

jdk8，接口中除了抽象方法，还可以有静态方法、默认方法， `public default void sing(){}` 
在实现类中==可以对默认方法重写，也可以不重写==

##### 5、函数式接口(行为参数化)

==定义==：只有1个抽象方法的接口，但可有静态方法、默认方法

==作用==：可作为方法的参数和返回值类型； ==3种调函数式接口的实现方法 ：==把函数式接口通过方法参数传进来 （传实现接口方法的对象）

- 把实现函数式接口的对象，传到方法参数里          [参数里传一个接口实例]
- 也可以把实现接口的匿名内部类，作为方法参数       [参数里传一个匿名内部类]
- 也可以把匿名内部类赋值给变量，用变量名.方法()    [通过变量调用接口中的方法]

```java
//写一个方法，参数：实现函数式接口方法的对象
public static void show(MyInterface myInterface){
     myInterface.say();
}

//第一种方法： 还要写个接口的实现类，用匿名内部类省掉这个类
MyInterface myInterface = new MyInterfaceImpl();
show(myInterface);

//第二种： 传匿名内部类； 但还要写一个静态方法，用第3种方法省掉这个方法
show(new MyInterface() {
            public void say() {
                System.out.println("say...");
            }
        });
    }

//第三种：赋给一个变量
MyInterface my=new MyInterface() {
            @Override
            public void say() {
                System.out.println("say...");
            }
};
my.say();

//第四种方法：new 接口 也省掉了
Lambda表达式
MyInterface my=()->{
      System.out.println("say...");
};
my.say();
```

| ![](./狂神说JavaSE基础.assets/Snipaste_2024-01-07_00-34-11.jpg) |      |
| ------------------------------------------------------------ | ---- |



##### 6、Lambda表达式

[lambda表达式怎么判断被调用接口名称和接口中方法](https://www.cnblogs.com/b3051/p/11090553.html)

总结：简化函数式接口； ==调实现方法的简化==

函数式接口 => Lambda表达式 => java8内置的函数式接口(4大类) => Lambda嵌套使用 => 方法引用（4类）

`行为参数化->简化：匿名类、lambda表达式->将List类型抽象化`

- Lamba参数：==是接口实现方法的参数==; 例：int add(intx,int y)

![](./狂神说JavaSE基础.assets/lambda.jpg)

```java
//通过变量调用接口中的方法； 
MyInterface myInterface2=()->{
      System.out.println("say...");
};
myInterface2.say();
```

- ==Lambda表达式==
  - 有形参、有返回值： (int a,int b) -> {return a+b;}
  - 有形参、无返回值： 接口的方法定义时，没有返回值； void hello(String name);
  - 无形参，有返回值  ()-> "win"; 省略了return

##### 7、JDK8中提供的函数式接口

java.util.function 包含很多类，用来支持 Java的 函数式编程

分==四种类型函数式接口==

1. Consumer：消费型接口
   1. 只有输入，没有返回
2. Predicate：断言接口
3. Supplier：供给型接口
   1. 有输出，没输入
4. Function：函数型接口
   1. ==BiFunction== 2个入参，1个出参     a+b < 100
   2. BinaryOperator  入参是比较器，返回一个Lambda表达式
      1. 例：创建一个Student类，2个参数：name score
      2. 讲不清楚

```java
public class Demo {
    public static void main(String[] args) {
//      Consumer<String> con=(name)->System.out.println(name);
        Consumer<String> con = System.out::println;
        con.accept("zhanshan");
        
//      Predicate<Integer> pre = (in) -> in < 12 ? true : false;
        Predicate<Integer> pre = (in) -> in < 12;
        System.out.println(pre.test(15));

//      Supplier<Integer> sup = () -> {return 12};
        Supplier<Integer> sup = () -> 12;
        System.out.println(sup.get());

//      Function<Integer,Boolean> func = (score) -> {return score>10?true:false};
        Function<Integer,Boolean> func = (score) -> score>10?true:false;
        System.out.println(func.apply(20));
    }
}
```

##### 8、Lambda表达式嵌套使用

### ==内部类==

[局部内部类](https://www.cnblogs.com/xingyboy/p/15266359.html) [四大内部类详细解析](https://blog.csdn.net/qq_40979103/article/details/124840199)  

视频： [匿名内部类](https://www.bilibili.com/video/BV1vt4y197nY/?p=8&spm_id_from=pageDriver&vd_source=7346303e5e18677d7261c2c0c109ecfd)

就是在一个类的内部再定义一个类

内部类分类： 

==定义在外部类局部位置==上(比如方法体内)

- 局部内部类（有类名）
  - 定义在外部类方法中，作用范围和创建对象范围仅限于当前方法中

- 匿名内部类（无类名）
  - 没有类名的局部内部类；  匿名内部类相当于创建了一个局部内部类

==定义在外部类的成员位置上==（作为成员）：

- 非静态成员内部类

- 静态成员内部类

1. 成员内部类
   1. 在类的内部定义，与实例变量、实例方法同级别的类
   2. 外部类的一个实例部分，创建内部类对象时，必须依赖外部类对象

> 1. 4种内部类
>    2. 成员内部类: 类的内部再定义一个类      `public class Inner { }`
>       1. ==通过外部类来实例化内部类==：㈠ Out.Inner  inner = `outer.new Inner()`     `new Person().new Inner();`
>       2. ㈡  ==内部类可以访问外部类的私有属性==、私有方法       public void getID( ) { System.out.println(id); }
>       3. 调内部类方法：`Outer.Inner in = new Outer().new Inner();`
>    3. 静态内部类：`public static class Inner { }` ;  不能访问外部类属性：因为先实例化的内部类， 内部类加载时外部类还没加载
>       1. 静态内部类，和外部类相同
>    4. 局部内部类：`类写在方法里面`;   
>       1. 局部内部类的方法，需要在方法的最后实例化调用
>    5. ==匿名内部类==：类实例出来是没有名字的， 没有名字初始化类，不用将实例保存到变量中
>       1. 一般这样：Apple app = new Apple()  ； `不要名字：new Apple().eat() ` ; 
>       1. new UserService(){ }   new一个接口, 里面写接口实现的方法
>       1. `匿名内部类在方法内部`   new Apple().eat()

| ![](./狂神说JavaSE基础.assets/Snipaste_2024-01-06_15-03-29.jpg) | ![]() |
| ------------------------------------------------------------ | ----- |





| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-19_20-06-04.jpg) | ![成员内部类](./狂神说JavaSE基础.assets/Snipaste_2023-06-03_17-08-02.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![内部类可以访问外部类的私有属性](./狂神说JavaSE基础.assets/Snipaste_2023-06-03_17-11-31.jpg) | ![局部内部类](./狂神说JavaSE基础.assets/Snipaste_2023-06-03_17-19-28.jpg) |
| ![匿名内部类](./狂神说JavaSE基础.assets/Snipaste_2023-06-03_17-23-13.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-03_17-25-54.jpg) |



##### 1、成员/静态内部类

> 1. 成员内部类
>    1. 与实例变量、实例方法同级别的类；
>    2. 必须==先创建外部类对象，才能创建内部类对象==
>       1. `Outer outer = new Outer();        inner inner = outer.new inner();`
>    3. ==外部类、内部类属性重名==时，访问内部类属性；这时访问外部类属性用：Outer.this.name
>    4. 成员内部类不能定义静态成员，但可定义静态常量：static final;
>    5. 成员内部类==访问外部类属性、方法==
>       1. 访问外部类私有属性： ==get+属性()== 或 ==Outer.this.name==
>    6. 外部类==访问成员内部类属性、方法==
> 2. 静态内部类
>    1. ==不依赖外部类对象==：创建内部类对象时，不需要创建外部类对象,==可直接创建或通过类名访问==
>       1. `new Outer.Inner()`不是new Outer对象，只是表示类的包含关系
>       1. `Outer.inner inner = new Outer.inner();` //创建静态内部类对象
>    2. 静态内部类可包含静态成员； 相当于一个外部类：普通类可包含什么，静态内部类就能包含什么
>    3. ==访问外部类成员==：相当于另外一个普通类访问外部类，==要先new外部类==
>    4. 只有静态内部类能加static，其它类都不能加static

| ![成员内部类访问外部类属性用get方法](./狂神说JavaSE基础.assets/Snipaste_2024-02-02_00-46-22.jpg) | ![]()                                                        |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![成员内部类](./狂神说JavaSE基础.assets/Snipaste_2023-12-18_22-34-11.jpg) | ![成员内部类方法调用](./狂神说JavaSE基础.assets/Snipaste_2023-12-18_22-30-40.jpg) |
| ![](./狂神说JavaSE基础.assets/Snipaste_2024-01-06_15-39-53.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2024-01-06_15-25-10.jpg) |
| ![静态内部类](./狂神说JavaSE基础.assets/Snipaste_2023-12-19_00-31-10.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-12-19_00-33-02.jpg) |

##### 2、局部/匿名内部类

[匿名内部类中定义的方法最好不要超过3个](https://blog.csdn.net/qq_45557294/article/details/102393679)

- 局部内部类作用范围和创建对象范围，近限于当前方法

> 1. 局部内部类：==类写在方法里面==;   //==作用域仅限当前方法，所以局部内部类的方法，需要在方法的最后实例化调用==
>    1. ==外部类、内部类属性重名==时，这时访问外部类属性用：Outer.this.name
>
>    2. 外部类的局部变量必须是常量，因为方法运行一次，变量就没了；而局部内部类和它new出的对象不会消失，但变量没有了，没法引用，所以把它变成常量，相当于不引用，直接使用常量 `System.out.println("地球")`
>
> 2. ==匿名内部类==：类实例出来是没有名字的， 没有名字初始化类，不用将实例保存到变量中
>    1. 实际就是==没有类名的局部内部类==, `在方法里面使用`；
>       1. 局部内部类有类名，==匿名内部类没有类名，new的接口==，里面的方法和局部内部类里面的一样。
>       1. ==匿名内部类是：定义类、实现类、创建对象的语法合并==，==只能创建一个==该类的==对象==
>    1. ==用在接口或父类中==：继承一个父类或实现一个接口
>       1. 例：定义一个Usb接口，service(); 
>       1. Mouse实现类；
>       1. TestUsb测试
>          1. main方法里写个实现类，实现接口的局部内部类 
>       1. 匿名内部类原理：接口实现类没有了，只能new 接口(),但接口不能new，new 接口(){}里写方法就可以new了;   ==匿名内部类new的是接口或父类==：new inter(){},大括号里写实现方法或重写方法；  
>    1. 一般这样：Apple app = new Apple()  ； `不要名字：new Apple().eat() ` ; 
>    1. new UserService(){ }   接口new, 里面写接口实现的方法
>    1. `匿名内部类在方法内部`   new Apple().eat()

| ![](./狂神说JavaSE基础.assets/Snipaste_2024-01-06_15-43-25.jpg) | ![局部内部类](./狂神说JavaSE基础.assets/jubuneibulei.png)    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![调用局部内部类的外部方法](./狂神说JavaSE基础.assets/Snipaste_2024-01-06_15-53-47.jpg) | ![main方法里创建一个实现接口的内部类](./狂神说JavaSE基础.assets/Snipaste_2024-01-06_17-31-48.jpg) |
| ![把局部内部类去掉，new接口，里面的方法一样](./狂神说JavaSE基础.assets/Snipaste_2023-12-17_23-05-59.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2024-01-06_20-24-22.jpg) |

```java
//Outer.java
public class Outer {
    private String name = "张三";
    private static int a = 10;

    public void show() {
        final String address = "地球";  //局部变量

        class Inner {     //局部内部类
            private String phone = "213434"; //局部内部类属性

            public void show2() {            //局部内部类方法
                //调外部类属性，用：类名.this.属性
                System.out.println(Outer.this.a);
                //调局部变量，因为局部变量执行一次后就消失，所以必须为常量
                System.out.println(address);
                //调局部内部类属性
                System.out.println(this.phone);
            }
        }
        //局部内部类的方法需要在方法的最后实例化调用
        new Inner().show2();
    }
}

//App.java
public class App {
    public static void main(String[] args) {
        Outer outer = new Outer();
        outer.show();
    }
}
//10
//地球
//213434
```



##### 3、内部类使用场景

视频： [匿名内部类使用场景](https://www.bilibili.com/video/BV15S4y1v7MM/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd)  

[四大内部类详细解析](https://blog.csdn.net/qq_40979103/article/details/124840199)

> 1. 抽象类、接口上使用匿名内部类
>    1. 如果子类只使用一次，将其写为一个类麻烦，用匿名内部类
>    1. ㈠new抽象类同时，要把抽象类的抽象方法实现了 `Person p = new Person(){ }`
> 2. ㈡Runnable接口的匿名内部类实现
>    1. ㈢反编译class文件：  javap -v Demo

```java
//Runnable接口的匿名内部类实现
public class Demo {
    public static void main(String[] args) {
        Runnable r = new Runnable() {
            @Override
            public void run() {
                System.out.println("子线程。。。。");
            }
        };
        Thread t = new Thread(r);
        t.start();
        System.out.println("主线程运行完毕");
    }
}
```

### 泛型

视频： [泛型基本写法_前端乐哥](https://www.bilibili.com/video/BV1VS4y1U7Pj?p=26&vd_source=7346303e5e18677d7261c2c0c109ecfd)    

[Java 泛型  ](https://www.runoob.com/java/java-generics.html)  [方法声明中static后的表示什么意思](https://zhidao.baidu.com/question/489108221655560652.html)   

泛型就是类型参数化， 简单说，就是==把类型本身当作参数来传递==，定义代码时先用占位符（如 `T`）顶着，==使用时再传入具体类型==，让同一套逻辑能适配多种类型，同时保留类型安全检查

> 1. 泛型
>    1. 类型的形参
>       1. 下面黑色图片是TS泛型
>       1. 约束，避免类型转换之间的问题
>       1. ==< >里面类似形参==， 调用时< >里面传入类型（实参）
>       1. 所有泛型方法声明都有一个类型参数声明（尖括号分隔,形参声明），该声明在方法返回类型之前  `public static < E > void printArray( E[] inputArray ){ }`
>       1. <? extends T>表示该通配符所代表的类型是T类型的子类
>       1. <? super  T>   表示该通配符所代表的类型是T类型的父类
>    2. 有界的类型参数：例如，只接受Number或者Number类型
>    3. 泛型类：类名后面添加类型参数声明部分   `public class Box<T>`

![](./狂神说JavaSE基础.assets/Snipaste_2023-06-08_10-44-49.jpg)

![](./狂神说JavaSE基础.assets/Snipaste_2023-06-08_10-48-39.jpg)

# 7、Java异常机制

### 异常分类

总结：==try里面出现了catch参数里的异常，就执行catch代码块里面的代码==； 捕获多个异常，层次递进；  选中代码ctrl+alt+T;  throw throws

1. 检查性异常      [ 检查型异常（Checked Exception）与非检查型异常（Unchecked Exception）](https://blog.csdn.net/weixin_45575129/article/details/102761535)
   1. 文件不存在、用户错误等，程序员无法预见
2. 运行时异常
   1. 程序员知道程序怎么运行的，可避免
3. 错误
   1. 栈溢出等，脱离程序员控制


| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-20_08-38-25.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-20_08-40-13.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-20_08-41-42.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-20_08-43-50.jpg) |

### 异常处理机制

异常出现，把它捕获住

1. `所有的异常，用一个异常类表示，把异常当作对象处理`
   1. `ctrl +alt +T`，选中包裹代码：把选中代码自动加try      `System.out.printLn(a/b)` 
2. 抛出异常
   1. throw==手动抛出异常==；  throws抛出异常给方法调用者
      1. throw： 知道肯定会错，主动抛出异常;  一般在方法中使用
      2. `if(b==0){throw new ArithmeticException();}`
   2. throws： 假设方法运行时报错了，往外抛异常； 
      1. 方法中处理不了主动抛的异常，把`异常对象抛出到更高级，用try...catch捕获处理这个异常`
3. 捕获异常： `try{...}catch(参数){...}finally{...}`
   1. ==try监控区域==; catch想要捕获的异常类型  
   2. try 可以监控区域； catch 捕获异常。流程：`如果try里面出现了catch参数里的异常，就执行catch代码块里面的。`
      1. 假设要捕获多个异常，层次递进，从小到大，否则上面的捕获了，下面就不捕获
      2. finally执行善后工作，出不出异常，都执行这一步

| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-20_08-44-38.jpg) | ![捕获多个异常，大的写下面](./狂神说JavaSE基础.assets/Snipaste_2023-06-07_19-11-36.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-04_10-48-33.jpg) | ![throw](./狂神说JavaSE基础.assets/Snipaste_2023-06-07_19-19-21.jpg) |
| ![throws](./狂神说JavaSE基础.assets/Snipaste_2023-06-07_19-24-54.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-05_17-00-24.jpg) |

```java
public class Test {
    public static void main(String[] args) {
        int a = 1;
        int b = 0;
        //假设要捕获多个异常，层次递进，从小到大
        //若try里出现Error异常，就执行catch代码块里面的
        try {   //try监控区域; catch捕获异常
            System.out.println(a / b);
        } catch (Error e) {   //catch捕获异常,(里面是想要捕获的错误类型，最高的是Throwable，层层递进最大范围的异常写下面)
            System.out.println("Error");
        } catch (Exception e) {
            System.out.println("Exception");
        } catch (Throwable e) {
            System.out.println("Throwable");
        } finally {                         //处理善后工作
            System.out.println("有没有错误，finally都会执行");
        }
    }
    public void a(){b();}  //a调用b，b调用a
    public void b(){a();}
}
```

主动抛出异常throw：

```java
public class Throw {
    public static void main(String[] args) {
        try {
            //调用下面的方法,加try为了捕获，不用try..catch，遇到错就停止，用后程序能继续往后运行
            new Throw().test(1, 0);
        } catch(ArithmeticException e) {
            e.printStackTrace();
        }
    }

    //假设这方法中，处理不了这个异常(throw)，就需要把异常抛到更高级(thorws)，在方法上抛出异常
    //主动抛出是throw，在方法上是throws
    //throw手动抛出异常，throws方法抛出异常
    public void test(int a, int b) throws ArithmeticException {
        if (b == 0) {
            throw new ArithmeticException();  //主动抛出异常，一般在方法中用
        }
    }
}
```

### 自定义异常

> 自定义异常
>
> 1. 知道会出错，==主动的抛出异常==，throw;    new ; 
> 2. 自定义异常：继承Exception类，父类，然后重写父类的方法
>    1. 要么捕获； 要么抛到更高的地方

| ![](./狂神说JavaSE基础.assets/Snipaste_2022-07-20_10-50-55.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2023-06-27_12-40-34.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-05_19-26-22.jpg) | ![](./狂神说JavaSE基础.assets/Snipaste_2026-11-05_19-29-43.jpg) |

```java
//自定义异常类
public class MyException extends Exception {
    //数字>10抛出异常
    private int detail;

    public MyException(int a) {
        this.detail = a;
    }

    //toString:异常的打印信息
    @Override
    public String toString() {
        return "MyException{" + "detail=" + detail + '}';
    }
}
```

```java
//测试类
public class Test {
    //可能存在异常的方法,抛出异常，外面捕获
    static void test(int a) throws MyException {
        System.out.println("传递的参数为：" + a);
        if (a > 10) {
            throw new MyException(a);
        }
        System.out.println("OK");
    }
    //测试test方法,捕获抛出的异常，e就是toString()方法
    public static void main(String[] args) {
        try {
            test(11);
        } catch (MyException e) {
            System.out.println("MyException=>" + e);
        }
    }
}
```



