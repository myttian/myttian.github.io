# Tomcat

## artifacts

[tomcat的artifacts是项目吗_百度搜索](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=tomcat%E7%9A%84artifacts%E6%98%AF%E9%A1%B9%E7%9B%AE%E5%90%97&oq=artifacts&rsv_pq=83f97996000132ef&rsv_t=98e1aDzIhvmivVbayIF2oIBkJ9HuvR4MS0hEEmU3D5mHJzVB5I6ZgXRUjJo&rqlang=cn&rsv_enter=1&rsv_dl=tb_enter&rsv_sug3=24&rsv_sug1=9&rsv_sug7=100&rsv_btype=t&inputT=10689&rsv_sug4=10690)  

[war和war exploded的区别](https://blog.51cto.com/u_15319091/4575565)  [IDEA中Tomcat单实例多项目部署实践](https://blog.csdn.net/weixin_28826961/article/details/170002835)  

项目的“部署包”或“构件”。Artifacts 是 IDEA 里把你写的代码、依赖库和资源文件按标准结构组装成的可部署单元，本质是“打包配置”或“组装说明书”，而非项目本身。

### 它和项目的关系

- 项目是源码：你写的 Java 类、HTML、JSP、配置文件等，散落在模块里。
- Artifacts 是打包产物：按 Tomcat 能识别的目录结构（`WEB-INF/classes`、`WEB-INF/lib`、`web.xml` 等），把源码编译结果和依赖收集到一起，生成 WAR 包或展开目录。

### 两种常见类型

- Exploded（展开式）：不压缩的目录结构，开发时用，改完文件能热部署，不用重新打包。
- Archive（归档式）：打包成 `.war` 文件，生产环境用，部署时 Tomcat 自动解压。

⚠️ 为什么必须配置它

Tomcat 本身不知道你的项目长什么样，Artifacts 就是告诉它“这是我的 Web 应用，按这个结构部署”。不配置的话，启动 Tomcat 会报 No artifacts configured，应用跑不起来。

Artifacts 是打包配置，那exploded和archive有什么区别? 或者web.xml配置在哪个目录?

## webapp和tomcat头文件一致

webapp4.0 通常指的是基于 Servlet 4.0 规范的 Web 应用，而 Tomcat 9 是支持该规范的主流服务器。两者搭配时，关键要让项目的 `web.xml` 版本声明和 Tomcat 版本匹配，否则可能出现加载问题。

### 版本对应关系

- Servlet 4.0 对应 Tomcat 9.x：Tomcat 9 实现了 Servlet 4.0 和 JSP 2.3 规范，是 webapp4.0 的标准运行环境。
- Tomcat 10+ 对应 Servlet 5.0+：Tomcat 10 及以上版本已升级到 Jakarta EE 规范，`web.xml` 头声明需改为 `web-app_5_0.xsd` 或更高版本，与 4.0 不通用。
- Tomcat 11 对应 Servlet 6.1：最新 Tomcat 11 实现 Servlet 6.1 和 JSP 4.0 规范，已完全脱离 4.0 体系。

### webapp4.0 的 web.xml 写法

使用 Tomcat 9 时，`web.xml` 头部应声明为 Servlet 4.0 格式：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                             http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0"
         metadata-complete="true">
</web-app>
```

### 在 IDEA 中配置 webapp4.0 + Tomcat 的要点

1. 检查默认版本：IDEA 创建 Maven webapp 项目时，默认 `web.xml` 可能是 2.3 版本，需要手动替换为上面 4.0 的声明，与 Tomcat 保持一致。
2. 配置 Tomcat 实例：在 IDEA 的 Run/Debug Configurations 中添加 Tomcat Server，选择本地安装的 Tomcat 9，然后在 Deployment 选项卡添加项目 artifact（war exploded 模式便于热部署）。
3. 启动与访问：配置完成后启动服务，浏览器访问 `http://localhost:8080/项目名/` 即可看到页面，IDEA 会生成 `target` 目录存放编译产物。

### ⚠️ 常见问题

- 端口占用：8080 被其他进程占用时，可在 Tomcat 配置中改端口，或用 `netstat -ano | findstr "8080"` 找到进程并结束。
- 控制台乱码：修改 Tomcat 的 `logging.properties` 或 IDEA 的 VM 选项为 `-Dfile.encoding=UTF-8` 即可解决。
- 配置文件未生效：Maven 的约定大于配置，若 `src/main/java` 下的配置文件未被导出，在 `pom.xml` 的 `build` 中配置 `resources` 即可。

webapp4.0 和 Tomcat 的搭配细节不少，可以继续了解`metadata-complete="true"` 的作用是什么? 或者Tomcat 9 支持哪些新特性?

## Tomcat还有用吗

[Tomcat 依然是 Java Web 世界的“老大”](https://baijiahao.baidu.com/s?id=1865892538524552956&wfr=spider&for=pc)   

Tomcat依然是Java Web领域的主力服务器之一。 2026年它活得挺好，只是角色变了：从“开发者的应用服务器”变成“运维和部署的基础设施”，并且是Spring Boot默认内嵌的Servlet容器。

### 2026年Tomcat的定位

1. 新项目首选：新项目推荐Tomcat 11.x（对应Jakarta EE 11规范，需JDK 17+），生产环境建议用JDK 21 LTS。Tomcat 10.1.x也是稳定选择，适合需要JDK 11+的项目。
2. 老项目维护：还在用`javax.*`包名的老代码，Tomcat 9.x是最后的选择，但其维护周期已于2025年12月终止，不建议新项目使用。
3. Spring Boot标配：Spring Boot内置Tomcat作为默认容器，绝大多数Java后端服务跑在Tomcat上，只是你可能感知不到。

### 关键变化：javax → jakarta

从Tomcat 10开始，Servlet API包名从`javax.servlet`迁移到`jakarta.servlet`。老项目部署到Tomcat 10+会直接报`ClassNotFoundException`，这是升级时最大的坑。

### 什么时候用外部Tomcat

- 单体或多应用共享资源：一台服务器跑多个内部系统，用外部Tomcat统一管理，比每个Spring Boot内置Tomcat起一个JVM更省内存。
- 需要精细控制：生产环境需要完全掌控线程池、JVM参数、安全配置时，外部Tomcat更灵活。
- 容器化场景：Docker/K8s里直接用官方镜像跑Tomcat也很普遍，环境隔离干净。

### 安全提醒

2026年4月Apache修复了CVE-2026-34486，这是一个Tomcat集群加密绕过RCE漏洞，仅影响Tomcat 9.0.116、10.1.53、11.0.20三个特定版本，且需开启集群+配置EncryptInterceptor+4000端口可达才可能被利用。建议升级到9.0.117、10.1.54或11.0.21。

> 单机部署、无集群配置的Tomcat不受此漏洞影响，不用过度紧张。

### 版本选择速览

| 版本          | 适用场景                 | JDK要求 |
| ------------- | ------------------------ | ------- |
| Tomcat 11.x   | 新项目首选               | JDK 17+ |
| Tomcat 10.1.x | 生产环境常见             | JDK 11+ |
| Tomcat 9.x    | 老项目维护（已停止维护） | JDK 8+  |

2026年学Java Web，Tomcat依然是绕不开的基础设施，放心学。

Tomcat的版本选择挺关键，要不要看看为什么新项目要选Tomcat 11.x?或者Tomcat 9.x为什么已经停止维护?

# Servlet

## servlet工作流程

[servlet工作流程_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=servlet%E5%B7%A5%E4%BD%9C%E6%B5%81%E7%A8%8B)  

Servlet的工作流程核心是：`浏览器发送请求 → Tomcat解析并找到对应Servlet → 调用service()处理 → 返回响应`。整个过程由Web容器（如Tomcat）接管，开发者只需继承HttpServlet并重写doGet()/doPost()。

### 完整流程拆解

1. 请求接收：浏览器发HTTP请求，Tomcat的Connector监听端口（默认8080）接收，解析请求行、请求头和请求体。
2. 请求封装：Tomcat把解析后的数据封装成`HttpServletRequest`对象，同时创建`HttpServletResponse`对象。
3. 路由匹配：根据URL路径，通过`web.xml`或`@WebServlet`注解找到对应Servlet类。
4. 实例化与初始化：首次访问时，Tomcat反射创建Servlet实例，调用`init()`方法（仅执行一次）。
5. 调用service()：每次请求到来，Tomcat分配线程调用`service()`方法，`HttpServlet`根据请求方式（GET/POST）自动分发到`doGet()`或`doPost()`。
6. 业务处理：在`doGet()`/`doPost()`中写业务逻辑，通过`HttpServletRequest`获取参数，处理完后把结果写入`HttpServletResponse`输出流。
7. 响应返回：Tomcat把响应对象序列化成HTTP报文，通过Socket发送回浏览器，浏览器解析并渲染页面。

### 生命周期要点

| 阶段   | 方法                         | 执行次数 |
| ------ | ---------------------------- | -------- |
| 实例化 | 构造器                       | 1次      |
| 初始化 | init()                       | 1次      |
| 服务   | service() → doGet()/doPost() | 每次请求 |
| 销毁   | destroy()                    | 1次      |

> Servlet是单实例多线程模型：所有请求共用同一个Servlet实例，但每个请求由独立线程处理。因此不要用实例变量存可变状态，否则会有线程安全问题。

### 容易混淆的点

- 请求转发 vs 重定向：转发是服务器内部跳转（1次请求，地址栏不变）；重定向是浏览器发起新请求（2次请求，地址栏改变）。
- doGet vs doPost：doGet参数在URL中，有长度限制、安全性低；doPost参数在请求体中，无长度限制、相对安全。

你之前刚看过MyBatis的流程，Servlet这套机制其实就是SpringMVC的底层基础，理解它对后面学框架很有帮助。

Servlet和MyBatis的底层机制都挺关键，可以接着看看Servlet和SpringMVC的关系或者MyBatis的执行流程

## servlet-mapping作用

[servlet-mapping作用_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=servlet-mapping%E4%BD%9C%E7%94%A8)  : Servlet 映射到 URL

`servlet-mapping` 的作用是把一个 ==URL 访问路径绑定到具体的 Servlet== 上，这样 Web 容器（如 Tomcat）就能根据用户访问的地址，找到对应的 Servlet 来处理请求。

### 核心机制

它通过 `<servlet-name>` 和 `<url-pattern>` 两个子元素配合 `<servlet>` 声明，完成“URL → Servlet”的映射关系。

1. URL 绑定：用户访问某个路径时，容器根据配置找到对应 Servlet，并调用 `doGet()` 或 `doPost()` 等方法处理请求。
2. 名字纽带：`<servlet-name>` 在 `<servlet>` 和 `<servlet-mapping>` 中必须一致，以此把 URL 和具体的类关联起来。

### 映射方式

`<url-pattern>` 支持几种匹配规则：

- 精确匹配：如 `/hello`，只有访问这个确切路径才触发。
- 前缀匹配：如 `/api/*`，该路径下的所有请求都交给这个 Servlet。
- 后缀匹配：如 `*.do`，符合这种格式的请求都由它处理。
- 默认匹配：如 `/`（注意不是 `/*`），作为默认处理入口。

### 配置示例

```xml
<servlet>
    <servlet-name>MyServlet</servlet-name>
    <servlet-class>com.example.MyServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>MyServlet</servlet-name>
    <url-pattern>/hello</url-pattern>
</servlet-mapping>
```

> 另外，也可以用 `@WebServlet("/hello")` 注解直接写在 Servlet 类上，效果和 `servlet-mapping` 一样，两者不冲突，同时定义时两个地址都能访问。

映射方式和注解写法都清楚了，可以接着看看精确匹配和前缀匹配怎么分清或者注解写法和配置文件怎么配

## servlet是如何应用在网站中的

Servlet 在网站中扮演“控制器”角色，负责接收浏览器发来的 HTTP 请求，调用业务逻辑处理后，把动态结果返回给浏览器。它运行在 Tomcat 等 Servlet 容器中，是 Java Web 应用处理请求的核心组件。

### 核心工作流程

1. ==请求到达容器==：浏览器访问 URL，请求先打到 Tomcat 等 Servlet 容器上。
2. ==匹配 Servlet==：容器根据 URL 路径，在 `web.xml` 或通过 `@WebServlet` 注解找到对应的 Servlet 类。
3. ==处理请求==：容器创建或复用 Servlet 实例，调用 `service()` 方法，再按请求类型分发到 `doGet()` 或 `doPost()` 方法里执行业务逻辑。
4. ==生成响应==：Servlet 通过 `HttpServletResponse` 输出 HTML、JSON 或重定向，容器把结果返回给浏览器。

### 生命周期

Servlet 由容器管理，遵循“一次创建、多次服务”模式：

- 初始化：首次请求到达时，容器加载类并调用 `init()`，只执行一次，适合加载配置或建立连接池。
- 服务：每次请求都触发 `service()` 方法，多个请求由多线程并发处理同一个实例。
- 销毁：应用停止或容器关闭时调用 `destroy()`，释放资源。

> 注意：Servlet 是单例多线程的，实例变量会被所有请求线程共享，所以不要用实例变量存请求相关的数据，否则会出现线程安全问题。

### 在网站中的实际应用方式

1. 处理表单提交：如登录、注册、搜索等，Servlet 用 `getParameter()` 获取表单数据，处理后响应结果。
2. ==做 MVC 的控制器==：Servlet 负责接收请求、==调用业务层（Service/DAO）==、把数据交给 JSP 或其他视图渲染，是 Spring MVC 等框架的底层基础。
3. 会话管理：通过 `HttpSession` 跟踪用户登录状态、购物车信息等。
4. 过滤器与监听器配合：`Filter` 可做编码设置、登录校验、日志记录，`Listener` 可监听会话创建、属性变化等，与 Servlet 协同工作。

### 现在的使用情况

直接写原生 Servlet 的场合变少了，但 ==Spring MVC 的 DispatcherServlet 本身就是个 Servlet，所有基于 Servlet 容器的框架底层都跑在 Servlet API 上==。理解 Servlet 原理，对排查请求流程、配置容器、调优性能都很有帮助。

Servlet 的生命周期和线程安全是关键点，可以看看Servlet 的单例多线程模式如何避免线程安全?或者Servlet 初始化和销毁方法分别在什么时机调用?

## servlet本质是java吗

Servlet本质上是Java技术，它是用Java编写的服务器端程序，属于Java EE（现Jakarta EE）规范的一部分。

### 核心概念

1. 规范与接口：==Servlet是Sun公司定义的一套规范（接口），核心是javax.servlet.Servlet接口==，所有`Servlet类必须实现它或继承已实现的类`。
2. Java程序本质：Servlet本质是运行在服务端的Java类，通常继承`HttpServlet`并重写`doGet`、`doPost`等方法处理HTTP请求。
3. 需要容器运行：Servlet不能独立运行，必须部署在Tomcat、Jetty等Servlet容器中，容器负责生命周期管理（加载、初始化、服务、销毁）。

### 工作原理

Servlet采用“请求-响应”模型，容器监听网络请求，解析HTTP报文后封装成`HttpServletRequest`和`HttpServletResponse`对象，再回调Servlet的`service()`方法，由`HttpServlet`按HTTP方法分发到`doGet()`或`doPost()`。

### 常见误区

- 不是框架：Servlet是标准接口，不是框架。Spring MVC等框架底层仍基于Servlet API实现。
- 与JSP关系：JSP本质是Servlet的简化写法，最终会被容器转换成Servlet运行。

> Servlet就像服务器端的“小助手”，容器负责网络、线程、协议解析等繁琐工作，开发者只需专注处理请求和生成响应。

Servlet本质是Java，但它的运行依赖容器，可以看看Tomcat和Jetty容器有何区别?或者Servlet和JSP具体怎么转换?

## servlet注册和映射

[web应用程序servlet的映射名称的规则及请求过程](https://www.cnblogs.com/xiaoQ0725/p/8861797.html)  

[servlet的注册和映射](https://blog.csdn.net/czj4451/article/details/84200211)  [使用@WebServlet注解来实现servlet和url的映射](https://my.oschina.net/zjllovecode/blog/961994)  [Servlet实现映射的两种方法](https://hestyle.blog.csdn.net/article/details/101790302)  

> servlet映射：将servlet类与URL（前端访问服务器的链接）一一对应。
>
> - 比如我们访问 http://localhost:8080/Hello/ServletDemo01，一般情况下末端的ServletDemo01肯定不是一个静态的资源文件，这个URL肯定是调用了后端的某个servlet类
> - 假设为ServletDemo01.java文件中Servlet类。那么把http://localhost:8080/Hello/ServletDemo01 与ServletDemo01.java中的Servlet类绑定的过程就称为servlet映射

Servlet 注册时，`<servlet-name>` 是自定义的逻辑名称（别名），`<servlet-class>` 才是映射的具体 Java 类全限定名。两者通过相同的 `<servlet-name>` 在 `<servlet>` 和 `<servlet-mapping>` 中关联。

方案一：web.xml 配置（传统方式）

```xml
<web-app>
    <!-- 1. 注册 Servlet：将逻辑名称映射到具体类 -->
    <servlet>
        <servlet-name>MyServletAlias</servlet-name>
        <servlet-class>com.example.MyServlet</servlet-class>
    </servlet>

    <!-- 2. 映射 URL：将访问路径映射到逻辑名称 -->
    <servlet-mapping>
        <servlet-name>MyServletAlias</servlet-name>
        <url-pattern>/my-path</url-pattern>
    </servlet-mapping>
</web-app>
```

方案二：`@WebServlet` 注解（Servlet 3.0+ 推荐）

直接在类上标注，无需 web.xml 配置，容器自动将类与 URL 绑定。

```java
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;

// name 属性可选，默认为类全限定名；value/urlPatterns 指定访问路径
@WebServlet(name = "MyServletAlias", urlPatterns = "/my-path")
public class MyServlet extends HttpServlet {
    //...
}
```

Servlet 注册方式有传统和注解两种，可以看看web.xml 和注解哪种更推荐?或者name 和 urlPatterns 有什么区别?

## Servlet还在继续用吗

Servlet 依然在用，而且短期内不会消失，只是它的角色变了——从“直接写业务代码”变成“底层基础设施”。

现在很少有项目会直接用 Servlet 写接口，大家基本都用 Spring Boot、Spring MVC 这套。但 Spring MVC 的底层就是 Servlet，你启动一个 Spring Boot 项目，内置的 Tomcat 本质上就是一个 Servlet 容器。所以不是不用了，而是被“包”起来了。

### 现在 Servlet 主要出现在哪里

1. 框架底层：Spring MVC 的 `DispatcherServlet` 就是核心入口，所有请求都要经过它分发。
2. 遗留项目维护：很多银行、电信、政务系统还在跑老 Servlet 项目，这些系统短期不会重写。
3. 容器与规范：Tomcat、Jetty 这些服务器实现的就是 Servlet 规范，Spring Boot 内嵌的也是它们。
4. 定制场景：文件上传、自定义过滤器、监控端点等，有时还是会直接用到 Servlet API。

### 对你的实际意义

你之前问过 Java 8 和虚拟线程，说明你在关注 Java 生态的走向。结合来看：

- 学 Servlet 仍然值得，它帮你理解请求怎么进来、响应怎么出去、Filter 链怎么执行。这些搞懂了，用 Spring 时出问题才不慌。
- 但不用专门学它来写项目，直接用 Spring Boot 开发效率高得多，Servlet 更多是“必须懂但不必天天写”的东西。
- 另外，Servlet 规范本身还在更新，最新到 6.1（Jakarta EE 10），并未停止维护。

> 简单说：Servlet 就像 Java Web 的“地基”，你看不见它，但房子一直建在它上面。直接用的少了，但它的地位没变。

Servlet 的角色确实变了，要不要继续看看Servlet 6.1 新增了哪些功能?或者Filter 和 Servlet 的执行顺序?

# JSP

## jsp技术已经没用了

[jsp技术已经没用了吗_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=jsp%E6%8A%80%E6%9C%AF%E5%B7%B2%E7%BB%8F%E6%B2%A1%E7%94%A8%E4%BA%86%E5%90%97)  

JSP并没有完全“没用”，但在新项目里基本已经被淘汰了。它仍活跃在大量老系统维护场景中，但新开发几乎不再使用，更多作为理解 Java Web 演进的历史技术存在。

### 为什么说它“过时”了

JSP 的核心问题在于设计理念和现代 Web 开发范式冲突，不是单纯“老了”：

1. ==前后端分离成绝对主流==：JSP 是典型的“前后端不分离”，Java 代码和 HTML 混在一起。现在`主流是后端提供 REST API，前端用 Vue/React 等框架独立渲染`，JSP 模式让前端难参与、后端难专注。
2. 维护性差：JSP 里能随意写 Java 代码（Scriptlet），业务逻辑、页面逻辑、展示逻辑全搅在一起，代码像“意大利面条”，改一处容易炸一片。
3. Spring Boot 不推荐使用：Spring Boot 官方默认不支持 JSP（内嵌 Tomcat 需额外配置），官方文档推荐 Thymeleaf、FreeMarker 或前后端分离方案。
4. 性能与效率落后：JSP 每次请求都要编译成 Servlet，首次访问慢，热部署差，调试困难。现代模板引擎预编译或客户端渲染更快。

### 现在谁还在用 JSP

JSP 没彻底消失，主要集中在：

- 10 年以上老遗留系统：银行、政务、ERP、OA 等核心系统，稳定运行多年，代码逻辑复杂，改造风险大、成本高。
- 部分高校/培训机构的教学项目：作为 Java Web 入门内容仍在教。
- 极少数小公司/外包的内部工具：追求“快速上手”，不讲究架构先进性。

### 学习建议

结合你之前查过 Java 8、虚拟线程、微服务架构，说明你在系统梳理 Java 技术栈，这个判断很关键：

- 如果你在维护老项目：JSP 必须懂，能看懂、能改 bug 就有价值。
- 如果你在准备求职或做新项目：把时间花在 Spring Boot + 前端框架（Vue/React） 上回报率高得多。简历写 JSP 反而容易被认为技术栈老旧。
- 替代方案：服务端渲染场景用 Thymeleaf、FreeMarker；前后端分离场景后端只返回 JSON，页面完全交给前端。

### 学 JSP 的“隐藏价值”

JSP 不是白学的：

- 它是 MVC 思想的早期实践场，==理解 Servlet + JSP + JavaBean 模式==，能帮你搞懂 Spring MVC 的设计渊源。
- JSP 本质是 Servlet，搞懂它的编译和执行流程，对 HTTP 请求处理、生命周期理解更深。
- 面试官问“JSP 过时了还有什么价值”，考的是你对技术演进脉络的理解，不只是语法。

一句话总结：JSP 没“死”，但已退居二线。新项目别选它，老项目躲不开它，学习上“知道即可，不必深究”。

JSP虽然退居二线，但了解它的演进脉络很有价值，比如JSP和Servlet的关系或者Thymeleaf和JSP的区别

## 替代JSP做视图渲染

[既然现在不用jsp渲染servlet,那么用什么渲染servlet_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=%E6%97%A2%E7%84%B6%E7%8E%B0%E5%9C%A8%E4%B8%8D%E7%94%A8jsp%E6%B8%B2%E6%9F%93servlet%EF%BC%8C%E9%82%A3%E4%B9%88%E7%94%A8%E4%BB%80%E4%B9%88%E6%B8%B2%E6%9F%93servlet)  

==前后端分离成绝对主流==：JSP 是典型的“前后端不分离”，Java 代码和 HTML 混在一起。现在主流是==后端提供 REST API，前端用 Vue/React 等框架独立渲染==，JSP 模式让前端难参与、后端难专注

> 问题： 既然现在不用jsp渲染servlet,那么用什么渲染servlet？ 
>
> - ==前后端分离==：目前更主流。==Servlet 只负责提供 JSON 接口，页面由 Vue、React 等框架渲染==，后端不再管视图，实现前后端完全解耦。
> - 前后端分离除了用servlet：
>   - Spring MVC / Spring Boot： 最主流的 Java 后端方案。用 `@RestController` + `@RequestMapping` 定义 RESTful 接口，==返回对象自动序列化成 JSON==，配合 Jackson 等库处理数据。
>     - ==常规 Web 项目==：直接用 Spring Boot，生态完善，和 Vue、React 配合很成熟，毕设和企业项目都够用。
>     - ==多端复用==：后端数据同时给 Web、App、小程序用，RESTful API 是通用解，客户端按需接入。
>     - ==实时性要求高==：聊天、股票行情、在线协作，用 WebSocket 做双向推送。
>     - ==内部服务间调用==：微服务场景下，gRPC 性能更好，但对外仍建议用 REST 或 GraphQL 暴露接口

现在通常用模板引擎（如 Thymeleaf、FreeMarker）或前后端分离的前端框架（如 Vue、React）来替代 JSP 做视图渲染。 如果仍走服务器端渲染，Thymeleaf 是 Spring Boot 官方推荐的主流选择；如果追求前后端完全解耦，则直接让 Servlet 返回 JSON 数据，由前端框架负责渲染。

### 主流替代方案

1. ==Thymeleaf==：最常被提到的 JSP 替代品，Spring Boot 官方推荐。它支持 HTML 原型直接浏览器预览，语法自然，能处理 HTML、XML、JavaScript 等。 在纯 Servlet 项目里也能用，需引入 `thymeleaf` 依赖，配置 `ServletContextTemplateResolver` 解析模板，再通过 `TemplateEngine` 处理页面。

2. ==FreeMarker==：老牌模板引擎，与 Thymeleaf 类似，适合生成 HTML 文本，性能不错，但模板语法与 HTML 差异较大。

3. ==前后端分离==：目前更主流。==Servlet 只负责提供 JSON 接口，页面由 Vue、React 等框架渲染==，后端不再管视图，实现前后端完全解耦。

### 为什么 JSP 被替代

JSP 本质是 Servlet，首次访问时被编译成 `HttpJspPage` 类，HTML 输出靠 `out.write()` 完成。 主要问题：

- 页面与 Java 代码混杂，维护和阅读困难，可读性差。
- 前后端耦合严重，页面更新依赖后端渲染，灵活性低。
- 笨重过时，相比现代模板引擎和前端框架，开发体验和协作效率都落后。

### 怎么选

- 内网管理系统、简单页面渲染：选 Thymeleaf，服务端渲染直接、开发快。
- 对外面向用户的复杂应用：选前后端分离，Servlet 提供 API，前端负责交互和渲染，扩展性和团队协作更好。

> 若用 Spring Boot，Thymeleaf 整合成本极低，只需引入 `spring-boot-starter-thymeleaf`，配置前缀后缀即可。

Thymeleaf 是主流选择，要不要看看Thymeleaf 语法和 JSP 一样吗?或者前后端分离后，后端如何维护页面?

## servlet是如何提供json接口的

Servlet 提供 JSON 接口的核心步骤：设置响应头 `Content-Type` 为 `application/json;charset=UTF-8`，使用 JSON 库（如 Jackson）将对象序列化为字符串，通过 `response.getWriter()` 写入。

依赖引入 (Maven)
```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.15.2</version>
</dependency>
```

Servlet 实现代码
```java
import com.fasterxml.jackson.databind.ObjectMapper;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.util.HashMap;
import java.util.Map;

@WebServlet("/api/data")
public class JsonServlet extends HttpServlet {

    private final ObjectMapper objectMapper = new ObjectMapper();

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 1. 设置响应类型和编码，防止中文乱码及前端解析错误
        resp.setContentType("application/json;charset=UTF-8");
        
        // 2. 准备数据 (实际场景中通常从数据库查询并封装为对象)
        Map<String, Object> data = new HashMap<>();
        data.put("code", 200);
        data.put("message", "success");
        data.put("data", "Hello JSON");

        try {
            // 3. 将对象转换为 JSON 字符串
            String jsonStr = objectMapper.writeValueAsString(data);
                        // 4. 写入响应体
            resp.getWriter().write(jsonStr);
        } catch (Exception e) {
            resp.setStatus(HttpServletResponse.SC_INTERNAL_SERVER_ERROR);
            resp.getWriter().write("{\"code\":500,\"message\":\"Server Error\"}");
        }
    }
}
```

关键注意点：
1. 编码一致：必须显式指定 `charset=UTF-8`，否则中文可能乱码。
2. 流互斥：`getWriter()` 和 `getOutputStream()` 不能在同一请求中同时调用，否则会抛出 `IllegalStateException`。
3. JSON 库选择：严禁手动拼接 JSON 字符串（易出错且不安全），务必使用 Jackson、Gson 或 Fastjson 等专业库进行序列化。

JSON 接口开发中还有不少细节，比如Jackson 序列化时如何忽略空值字段?或者如何防止 JSON 中的 XSS 攻击?

## 前后端分离除了用servlet，还能用什么

[前后端分离除了用servlet提供json接口,还可以用什么?_百度搜索](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=%E5%89%8D%E5%90%8E%E7%AB%AF%E5%88%86%E7%A6%BB%E9%99%A4%E4%BA%86%E7%94%A8servlet%E6%8F%90%E4%BE%9Bjson%E6%8E%A5%E5%8F%A3%EF%BC%8C%E8%BF%98%E5%8F%AF%E4%BB%A5%E7%94%A8%E4%BB%80%E4%B9%88%EF%BC%9F&oq=servlet%25E6%2598%25AF%25E5%25A6%2582%25E4%25BD%2595%25E6%258F%2590%25E4%25BE%259Bjson%25E6%258E%25A5%25E5%258F%25A3%25E7%259A%2584&rsv_pq=e1f66c4d000970be&rsv_t=428avLTuFFSUX%2BvFWkStl0LhqbOzz5uslydOAhbILFFXswL8yOAoyASDNfA&rqlang=cn&rsv_enter=1&rsv_dl=tb_enter&rsv_sug3=52&rsv_sug1=19&rsv_sug7=100&rsv_btype=t&inputT=109087&rsv_sug4=109087)  

> 问题： 前后端分离除了用servlet提供json接口,还可以用什么?

除了直接用 Servlet 写 JSON 接口，更主流的做法是用 Spring Boot 的 `@RestController` 注解，它底层还是 Servlet，但把参数解析、响应转换、路由映射都封装好了，开发效率高很多。

### 常见替代方案

1. Spring MVC / Spring Boot：最主流的 Java 后端方案。用 `@RestController` + `@RequestMapping` 定义 RESTful 接口，==返回对象自动序列化成 JSON==，配合 Jackson 等库处理数据。
2. JAX-RS 规范：Java 标准 REST 接口规范，如 Jersey、RESTEasy 实现。通过注解定义资源类和方法，比 Servlet 更抽象，但不如 Spring 生态普及。
3. GraphQL：由 Facebook 提出的查询语言。前端可按需查询字段，解决接口返回过多或过少问题，适合复杂数据场景，Java 端可用 `graphql-java` 或 Spring GraphQL。
4. gRPC：高性能 RPC 框架，默认用 Protocol Buffers 二进制序列化，比 JSON 更轻量，适合内部微服务通信。但浏览器不能直接调用，需通过 gRPC-Web 或网关转接。
5. WebSocket：全双工通信协议，适合实时推送、在线聊天、协作编辑等场景，服务端可主动推送数据。
6. 传统 JSP + AJAX：JSP 页面内嵌 AJAX 请求，后端返回 JSON 片段或数据，属于半分离模式，现在用得少，但理解演进仍有价值。

### 怎么选

- ==常规 Web 项目==：直接用 Spring Boot，生态完善，和 Vue、React 配合很成熟，毕设和企业项目都够用。
- ==多端复用==：后端数据同时给 Web、App、小程序用，RESTful API 是通用解，客户端按需接入。
- ==实时性要求高==：聊天、股票行情、在线协作，用 WebSocket 做双向推送。
- ==内部服务间调用==：微服务场景下，gRPC 性能更好，但对外仍建议用 REST 或 GraphQL 暴露接口。

> 前后端分离本质是约定接口规范和数据格式，不绑定特定框架。Servlet 能实现，Spring Boot、JAX-RS、GraphQL 等也能，选型主要看团队技术栈、项目规模和维护成本。

除了主流框架，GraphQL 和 gRPC 也有不少细节，可以看看GraphQL 的查询语言怎么写?或者gRPC 的 Protocol Buffers 如何定义?

## JSP9大内置对象

[jsp内置对象有什么作用_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=jsp%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1%E6%9C%89%E4%BB%80%E4%B9%88%E4%BD%9C%E7%94%A8)  

JSP 共有 9 个内置对象，可直接在页面中使用，分别负责请求、响应、会话、输出等常见功能。
- request：代表客户端请求，用来获取表单参数、请求头等数据，作用域为一次请求。
- response：代表服务器响应，用来设置响应头、状态码或向客户端输出内容。
- session：代表用户会话，用来保存同一用户在多次请求之间的信息，如登录状态。
- application：代表整个 Web 应用，所有用户共享，常用于保存全局配置或在线人数。
- out：代表输出流，用来向浏览器输出文本内容。
- pageContext：代表当前页面上下文，可获取其他内置对象，管理页面范围的属性。
- config：代表 Servlet 配置，用来读取 web.xml 中的初始化参数。
- page：代表当前 JSP 页面本身，相当于编译后的 Servlet 实例，一般很少直接使用。
- exception：代表异常对象，只能在声明了 isErrorPage="true" 的错误页面中使用。

内置对象各有侧重，可以看看 request和session作用域有何区别？ 或者 out和JSP的输出语句有何不同？

## JSP标签和EL表达式

[JSP标签和EL表达式有什么作用和应用_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=JSP%E6%A0%87%E7%AD%BE%E5%92%8CEL%E8%A1%A8%E8%BE%BE%E5%BC%8F%E6%9C%89%E4%BB%80%E4%B9%88%E4%BD%9C%E7%94%A8%E5%92%8C%E5%BA%94%E7%94%A8)  

> 问题：JSP标签和EL表达式有什么作用和应用

JSP标签和EL表达式的核心作用，都是==为了让JSP页面摆脱Java代码，变得更干净、更易维护==。 简单说，EL负责“取数、算数”，JSP标签（尤其是JSTL）负责“逻辑控制”，两者配合，让页面只专注于显示数据。

### EL表达式：让取数变简单

EL（Expression Language）主要用来替代JSP里的表达式脚本 `<%=...%>`，从域对象中取数据并输出，语法是 `${表达式}`。

- 获取数据：从 `page`、`request`、`session`、`application` 四个域中按顺序查找，找到即输出。比如 `${user.name}` 会自动调用 `getName()` 方法，比写 `<%=((User)request.getAttribute("user")).getName()%>` 简洁得多。
- 处理 null 值：取不到值时输出空字符串，而不是“null”，对用户更友好。
- 支持运算：支持算术、关系、逻辑和三元运算，还能用 `empty` 判断集合或字符串是否为空。
- 内置对象：通过 `param` 获取请求参数、`sessionScope` 直接取会话域数据，非常方便。

### JSP标签（JSTL）：让逻辑变清晰

JSP标准标签库（JSTL）用标签形式替代页面里的Java逻辑代码，最常用的是核心标签库（前缀 `c`）。

- 条件判断：`<c:if>` 和 `<c:choose>` 替代 `if-else` 结构，比如根据性别显示不同内容。
- 循环遍历：`<c:forEach>` 遍历集合或数组，配合EL输出列表数据，比如商品列表、用户表格。
- 赋值与输出：`<c:set>` 设置变量，`<c:out>` 输出并支持默认值，比脚本更安全。

### 典型应用场景

两者通常搭配使用，在MVC模式里，JSP只当视图层，负责展示数据，不处理业务逻辑。

```jsp
<!-- 遍历用户列表 -->
<c:forEach items="${userList}" var="user">
    <tr>
        <td>${user.name}</td>
        <td>${user.age}</td>
        <td>
            <c:if test="${user.age >= 18}">成年</c:if>
            <c:if test="${user.age < 18}">未成年</c:if>
        </td>
    </tr>
</c:forEach>
```

> 这段代码里，`${userList}` 是EL从域中取数据，`<c:forEach>` 是JSTL做循环，`${user.name}` 是EL取对象属性，全程没有一行Java代码，页面结构清晰，前端人员也能看懂。

### ⚠️ 需要注意

- EL表达式只能读取数据，不能修改，也不支持复杂的控制流（如 `while`），所以需要和JSTL配合使用。
- 如果JSP页面里还大量出现 `<% %>` 脚本，说明没有充分利用EL和JSTL，代码会很难维护。

EL和JSTL的配合很关键，可以看看EL的empty运算符如何处理空值?或者JSTL的c:choose标签如何实现多选?

# 实体类

## Servlet+JSP+JavaBean模式

**[JavaBean](https://www.baidu.com/s?wd=JavaBean&usm=2&ie=utf-8&rsv_pq=b256cd6200080356&oq=JavaBean&rsv_t=0e29DqIjYeXsmECsld1RPIDqvmQhcsBqfiY9XtG%2B%2BMbh75LQxeImPp6H6b8&rsv_dl=re_dqa_generate&sa=re_dqa_generate) 是一种遵循特定规范的 Java 类，主要用于封装数据**‌，在 Java 语言中扮演着可重用组件的核心角色，广泛应用于 JSP、Servlet 及各类框架的数据传输与模型层构建 。它通过私有化属性并提供公共的访问方法，实现了内部状态的受控暴露，支持工具通过反射机制自动操作其属性 。‌‌

### 标准编写规范

编写一个标准的 JavaBean 需严格遵守以下约定，以确保其能被开发工具和框架正确识别与使用：

1. 类与构造器要求。
   - 类必须是具体的（非抽象）且公共的（public）。
   - 必须提供一个公共的无参数构造器，以便容器或框架通过反射实例化对象 。‌‌
2. 属性访问规范。
   - 属性应私有化（private），通过公共的 getter 和 setter 方法暴露 。
   - 方法命名遵循特定模式：获取属性值为 `get 属性名`，设置属性值为 `set 属性名`，布尔类型可用 `is 属性名` 代替 get。
   - 属性名称由 getter/setter 方法名中去除"get"、"set"或"is"后剩余部分的首字母小写形式决定 。‌‌‌
3. 序列化支持。
   - 通常建议实现 `java.io.Serializable` 接口，以支持对象状态的持久化和网络传输 。‌‌

### 核心作用与应用

JavaBean 的设计初衷是提高代码的可重用性和维护性，其主要应用场景包括：

1. 数据封装与传输。
   - 在 [MVC](https://www.baidu.com/s?wd=MVC&usm=2&ie=utf-8&rsv_pq=b256cd6200080356&oq=JavaBean&rsv_t=785fU14%2FZ3PXgJgfPzWdOz8F2FxyXhpXtQA%2BYFMbBlio7bvkKstkYLnZAkw&rsv_dl=re_dqa_generate&sa=re_dqa_generate) 架构中常作为模型层（[Model](https://www.baidu.com/s?wd=Model&usm=2&ie=utf-8&rsv_pq=b256cd6200080356&oq=JavaBean&rsv_t=62c1YyY%2BwlX43L11XIktSMtpVLHsrEBcWJo6kikTCOXtka7psemvjRLnlUs&rsv_dl=re_dqa_generate&sa=re_dqa_generate)），负责在各层之间传递数据，如表单数据封装 。
   - 通过合理的组织，可将业务逻辑、数据库操作等封装为不可视化 Bean，实现前后端分离 。‌‌
2. 组件化开发。
   - 作为可重用组件，可被 JSP 页面、Servlet 或其他 Java 程序调用，类似“黑盒子”使用 。
   - 可视化 JavaBean 拥有 GUI 界面（如按钮），不可视化 JavaBean 则专注于后台逻辑处理 。‌‌
3. 框架集成基础。
   - 其内省（Introspection）机制允许框架在运行时动态获取属性信息，是依赖注入、对象拷贝等功能的基础 。‌‌

### 进阶特性与 API 支持

JavaBeans 架构不仅限于基础规范，还提供了丰富的事件与元数据支持：

1. 属性类型扩展。
   - 支持简单属性（[Simple](https://www.baidu.com/s?wd=Simple&usm=2&ie=utf-8&rsv_pq=b256cd6200080356&oq=JavaBean&rsv_t=03d67XGugKRGLYzsxAOkMweSXR7IVvM2fHR5B4%2BR%2BzvYBk5jgnTHOGHf7rI&rsv_dl=re_dqa_generate&sa=re_dqa_generate)）、索引属性（[Indexed](https://www.baidu.com/s?wd=Indexed&usm=2&ie=utf-8&rsv_pq=b256cd6200080356&oq=JavaBean&rsv_t=03d67XGugKRGLYzsxAOkMweSXR7IVvM2fHR5B4%2BR%2BzvYBk5jgnTHOGHf7rI&rsv_dl=re_dqa_generate&sa=re_dqa_generate)）、绑定属性（[Bound](https://www.baidu.com/s?wd=Bound&usm=2&ie=utf-8&rsv_pq=b256cd6200080356&oq=JavaBean&rsv_t=03d67XGugKRGLYzsxAOkMweSXR7IVvM2fHR5B4%2BR%2BzvYBk5jgnTHOGHf7rI&rsv_dl=re_dqa_generate&sa=re_dqa_generate)）和约束属性（[Constrained](https://www.baidu.com/s?wd=Constrained&usm=2&ie=utf-8&rsv_pq=b256cd6200080356&oq=JavaBean&rsv_t=437coOJLMHPcQKKDnYkWhTkBlmxF8euTvqQBSq8WX232vDZ%2BABRLZjoRcR8&rsv_dl=re_dqa_generate&sa=re_dqa_generate)），满足不同交互需求 。
   - 绑定属性在值改变时会通知监听器，约束属性允许监听器否决修改 。‌‌‌
2. java.beans 包支持。
   - 该包提供了 `Introspector` 类用于动态获取 Bean 信息，`PropertyChangeEvent` 处理属性变更事件 。
   - 包含 `XMLEncoder` 和 `XMLDecoder` 支持基于 XML 的长期持久化 。‌‌‌
3. 注解增强。
   - 从 JDK 9 开始，引入 `@JavaBean` 注解，用于指定自动生成 [BeanInfo](https://www.baidu.com/s?wd=BeanInfo&usm=2&ie=utf-8&rsv_pq=b256cd6200080356&oq=JavaBean&rsv_t=8ecbel10KZasz88HgfAuQHo64ZqaNaJ4%2BreDCcHwkGsCUNXNDLuGNxtq4aE&rsv_dl=re_dqa_generate&sa=re_dqa_generate) 类时的元数据，如默认属性和事件集 。‌‌

JavaBean 的规范很清晰，要不要再看看 setter 方法是否必须？ 或者 没有无参构造器会怎样？

## 实体类如何映射数据库

[实体类如何映射数据库_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=%E5%AE%9E%E4%BD%93%E7%B1%BB%E5%A6%82%E4%BD%95%E6%98%A0%E5%B0%84%E6%95%B0%E6%8D%AE%E5%BA%93)  

实体类映射数据库的核心方式是通过 ORM 框架，用注解或 XML 配置把类、属性对应到表、字段，让开发者以操作对象的方式完成数据库增删改查。

### 映射的核心思想

1. 类 → 表：实体类对应数据库中的一张表，类名通常对应表名。
2. 属性 → 字段：类中的属性对应表中的列，属性名对应列名。
3. 对象 → 行：类的实例对应表中的一行记录。
4. 操作 → SQL：调用对象方法时，框架自动生成并执行 SQL 语句。

### 主流框架的映射方式

不同框架的映射写法略有差异，但原理相通。

#### JPA / Hibernate（注解方式）

```java
@Entity
@Table(name = "t_user")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "user_name")
    private String userName;
}
```

- `@Entity` 声明实体类
- `@Table` 指定表名
- `@Id` 标记主键
- `@GeneratedValue` 配置主键生成策略
- `@Column` 指定字段名及约束

#### MyBatis（XML 方式）

```xml
<resultMap id="userMap" type="User">
    <id column="id" property="id"/>
    <result column="user_name" property="userName"/>
</resultMap>

<select id="selectUser" resultMap="userMap">
    select id, user_name from t_user
</select>
```

MyBatis 也支持开启“下划线转驼峰”自动映射，简单查询无需手写 resultMap。

#### MyBatis-Plus（注解增强）

```java
@TableName("t_user")
public class User {
    @TableId(type = IdType.ASSIGN_ID)
    private Long id;

    @TableField("user_name")
    private String userName;
}
```

- `@TableName` 指定表名
- `@TableId` 配置主键及生成策略
- `@TableField` 指定字段名、自动填充、逻辑删除等

#### GORM（Go 语言）

```go
type User struct {
    ID       uint   `gorm:"primaryKey"`
    UserName string `gorm:"column:user_name"`
}
```

通过结构体标签（tag）完成映射，框架内部将结构体解析为表结构和字段信息。

### ⚠️ 需要特别注意的映射细节

1. 字段名不一致：数据库用下划线（`user_name`），Java 用驼峰（`userName`），需显式映射或开启全局下划线转驼峰配置。
2. 主键生成策略：数据库自增、雪花算法、手动输入等，需按业务场景配置。
3. 字段不落库：临时或运算字段用 `@Transient`（JPA）或 `@TableField(exist = false)`（MyBatis-Plus）标注不映射。
4. 关联关系映射：一对一、一对多、多对多需用 `@OneToOne`、`@OneToMany`、`@ManyToMany` 等注解，或 MyBatis 的 `<association>`、`<collection>` 标签。
5. 枚举与特殊类型：枚举默认存为字符串或序号，可用 `@Enumerated` 控制；大文本、二进制等用 `@Lob` 标注。

### 底层原理

ORM 框架启动时扫描实体类注解或配置文件，在内存中构建“类→表、属性→列”的元数据描述表。运行时通过反射读取对象状态，根据元数据动态生成 SQL，执行后把结果集封装回对象。 这也是为什么实体类字段名、类型必须与映射配置严格对应，否则会出现数据读写异常。

映射配置细节不少，可以看看下划线转驼峰配置方法或者主键自增和雪花算法区别

## 实体类通过什么把数据存入数据库

实体类通过==ORM框架==或==JDBC技术==把数据存入数据库，核心思路是把内存中的Java对象映射成数据库表中的记录。

### 主流方式

1. **ORM框架（最常用）**‌：通过对象关系映射，让实体类与数据库表对应，操作对象即操作数据。框架自动生成SQL并执行，如 `Hibernate、JPA、MyBatis、Spring Data JPA`
2. JDBC手动操作：用原生SQL配合占位符，把实体类属性取出填入SQL执行，如 `PreparedStatement` 的 `setString()` 等。
3. MyBatis Mapper：在XML或注解中写SQL，通过 `{属性名}` 自动把实体类字段填入参数。

### 关键机制

- 注解映射：实体类上用 `@Entity`、`@Table` 指定表，`@Id`、`@Column` 映射字段，框架据此建立对应关系。
- 持久化上下文：JPA/Hibernate 通过 `EntityManager` 或 `Session` 管理实体状态，调用 `persist()` 或 `save()` 后，框架生成 `INSERT` 语句写入数据库。
- 事务控制：保存操作需在事务中执行，成功提交，失败回滚，保证数据一致性。

> 数据库不能直接存对象，必须通过映射或序列化把对象拆成字段值，再交给SQL执行。

实体类和数据库的映射机制挺关键，要不要继续看看注解映射中@Table和@Entity有什么区别?或者JDBC手动操作和ORM框架有何区别?

# MVC架构

## MVC架构工作流程

[MVC架构工作流程_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=MVC%E6%9E%B6%E6%9E%84%E5%B7%A5%E4%BD%9C%E6%B5%81%E7%A8%8B)  

MVC架构的工作流程就是：==用户请求 → 控制器接收 → 模型处理业务和数据 → 控制器选择视图 → 视图渲染并返回==。核心是“各管一摊”，Model管数据和业务，View管展示，Controller居中调度。

### 一次完整请求的流转

以“查看商品详情”为例：

1. 用户发起请求：浏览器输入URL或点击按钮，向服务器发送HTTP请求。
2. 控制器接收请求：Controller根据URL和参数判断用户意图，但自己==不处理业务，只负责调度==。
3. 模型处理业务：Controller调用Model（通常再拆成Service和DAO层），Model查数据库、算价格、执行业务规则，完成后把结果返回给Controller。
4. 控制器选择视图：Controller拿到结果后，决定用哪个View展示，并把Model数据传过去。
5. 视图渲染响应：View只做展示，把数据填充进HTML/JSP/Thymeleaf模板，生成最终页面返回给浏览器。

> 数据流动方向是：Controller → Service → DAO → Database，返回后再交给View渲染，这就是完整链路。

### 各层职责边界

- Model（模型）：封装数据结构和业务规则，负责与数据库交互，包含实体类、DAO和Service。
- View（视图）：只负责界面渲染，不包含业务逻辑，可访问模型的读方法但不能写。
- Controller（控制器）：接收请求、调用业务、返回结果，是Model和View之间的唯一中介。

### 两个关键原则

- Controller里不要塞业务：Controller只做调度，业务逻辑放Service层，否则违反单一职责。
- Controller不要直接依赖数据库：应依赖Service接口或Repository接口，这样底层实现替换时上层不用改。

### 框架与变体

不同技术栈对MVC的实现略有差异：Java里Spring MVC通过DispatcherServlet做前端控制器统一分发请求；Python的Django叫MTV（Model-Template-View），本质一样；Go常用Gin；前端Vue、React也有自己的View+Store形态。 前后端分离后，View独立成前端项目，通过HTTP API通信，后端专注Controller、Service和数据库，这是现在企业更常见的形态。

前后端分离后View独立成前端项目，可以看看==前后端分离的MVC怎么分层==或者==前端View怎么和后端API对接==
