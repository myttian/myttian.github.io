md： [全栈开发](.\全栈开发)

# Java框架收集

## 测试

### ‌JUnit

用于编写和运行 Java 程序==单元测试==的开源框架

## 缓存

[ehcache_百度搜索](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=ehcache&oq=%25E5%258A%25A8%25E6%2580%2581sql&rsv_pq=ac0453c7002e71dc&rsv_t=196bHWT6JewlchpwlouSmwlI9ZdwL3Rk4kxhSKVojWzanZWusbWGJuYwwqk&rqlang=cn&rsv_enter=1&rsv_dl=tb_enter&rsv_sug3=10&rsv_sug1=6&rsv_sug7=100&rsv_btype=t&inputT=1169596&rsv_sug4=1169596)  

### Ehcache

Mybatis有讲:  [缓存简介](https://www.bilibili.com/video/BV1NE411Q7Nx/?vd_source=7346303e5e18677d7261c2c0c109ecfd&spm_id_from=333.788.player.switch&p=26)  

‌Ehcache 是一个基于 Java 的开源进程内缓存框架，主要用于提升应用程序性能，支持内存和磁盘多级存储‌

- 它遵循 Apache 2.0 协议，被广泛应用于 Hibernate、Spring Boot 等主流框架中，作为本地缓存解决方案来减少数据库访问压力

## 其它

### uni-app

[uni-app官网](https://uniapp.dcloud.net.cn/)  [uni-app_百度百科](https://baike.baidu.com/item/uni-app/56528723)  

## RESTful API

### Swagger

[Swagger](https://baike.baidu.com/item/Swagger/69203638)  

一套用于设计、构建、文档化和测试RESTful API的开源软件框架

## ssm框架还有用吗

[ssm框架还有用吗_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=ssm%E6%A1%86%E6%9E%B6%E8%BF%98%E6%9C%89%E7%94%A8%E5%90%97)  

SSM框架还有用，但用途已经变了。它不再是新建项目的首选，但在维护存量系统、理解Spring Boot底层原理和Java后端面试中，依然有不可替代的价值。

### 现在的SSM用在哪

1. 存量系统维护：银行、物流、政务、制造等行业，大量2015—2020年间交付的核心系统仍跑在SSM上。业务稳定、改造成本高，这些系统会继续存在很长时间。
2. 理解Spring Boot的基石：Spring Boot底层跑的还是Spring容器、Spring MVC的DispatcherServlet和MyBatis。SSM手写XML配置的方式，把IoC、AOP、事务代理、Mapper动态代理这些机制暴露得最清楚，学透了再看Boot的自动配置，就是“原来是把这些手工活自动化了”。
3. 面试高频考点：Spring IOC/AOP原理、Spring MVC执行流程、MyBatis Mapper为什么接口能直接调用——这些全是SSM体系核心知识。面试官问这些，是想确认你是否真懂从请求到数据库的完整链路，而非只会用Boot写CRUD。

### 和Spring Boot的关系

SSM和Spring Boot不是对立关系，而是“手工拼装”和“自动化封装”的关系。Boot没有发明全新编程模型，只是把SSM时代繁琐的XML配置、依赖管理、外部Tomcat部署都自动化了。Spring Boot项目里依然用Spring MVC写接口、用MyBatis连数据库，代码风格和SSM几乎一样。

> 简单说：SSM教你怎么搭建和理解分层框架，Spring Boot教你如何快速大规模生产代码。前者是“解剖学教材”，后者是“现代化交付方式”。

### 怎么学才划算

- 新手：值得认真学一遍SSM，但别停留。能徒手搭出SSM项目后，再切Spring Boot，才会真正理解“约定优于配置”的价值。
- 已有Boot经验：没必要回头补XML配置，直接读Spring核心文档、理解IoC/AOP原理就够了。
- 别只停留在SSM：2026年的Java后端门槛已抬高，还得懂数据库优化、缓存、分布式事务、容器化这些硬功夫。框架只是工具，业务价值和问题定位能力才是分水岭。

SSM虽然不是新项目首选，但理解它能帮你深入底层，要不要看看SSM和Spring Boot的配置差异在哪?或者SSM项目中事务管理怎么配置?

# Java 库

## Lombok

[Lombok_百度百科](https://baike.baidu.com/item/Lombok/23780246)  [Lombok_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=Lombok)  

说明：Mybatis视频里有讲到   [Lombok的使用](https://www.bilibili.com/video/BV1NE411Q7Nx/?vd_source=7346303e5e18677d7261c2c0c109ecfd&spm_id_from=333.788.player.switch&p=18)  

Lombok 是一个 Java 库，通过注解在编译期自动生成 getter、setter、构造器、equals、hashCode、toString 等样板代码，从而减少冗余、提升开发效率。 它生成的代码在编译期完成注入，运行期零性能损耗，与手写代码字节码一致。

### 核心注解

1. @Data：最常用，整合了 `@Getter`、`@Setter`、`@ToString`、`@EqualsAndHashCode` 和 `@RequiredArgsConstructor`。
2. @Getter / @Setter：生成字段的 getter/setter 方法，可加在类或字段上。
3. @NoArgsConstructor / @AllArgsConstructor / @RequiredArgsConstructor：分别生成无参构造器、全参构造器、包含 final 和 @NonNull 字段的构造器。
4. @Builder：生成链式调用风格的对象创建代码，如 `User.builder().id(1).build()`。
5. @Slf4j：自动生成日志对象 `log`，可直接在方法中使用。
6. @NonNull：用于方法参数或字段，表示不能为 null。
7. @ToString(exclude = "password")：生成 toString，可排除指定字段。

### 使用前提

1. 引入依赖：Maven 项目中添加 `org.projectlombok:lombok` 依赖，Spring Boot 项目用 `<optional>true</optional>` 即可。
2. 安装 IDE 插件：IntelliJ IDEA 2020.3 以上版本内置支持；更早版本需在插件市场安装 Lombok 插件并开启注解处理。

### 注意事项

`@Data` 生成 hashCode/equals 时若对象存在自引用或循环引用，会引发 `StackOverflowError`。 可用 `@EqualsAndHashCode(exclude = "friend")` 排除循环字段，或改用细粒度注解，手动重写相关方法。

了解了 Lombok 的核心功能，要不要再看看Lombok 与 Jackson 注解有何区别?或者Lombok 生成的代码能被序列化吗?

# 数据库

## mysql-connector-java

mysql-connector-java 是 MySQL 官方提供的 Java 数据库驱动程序，用来让 Java 程序连接和操作 MySQL 数据库，官网文档可在 [dev.mysql.com](https://dev.mysql.com/doc/connector-j/en/) 查看。

### 怎么获取和引入

1. 官网下载：访问 MySQL 官方网站下载最新稳定版本的驱动包，选择与你的 MySQL 服务器版本匹配的 Connector/J 版本。
2. Maven 依赖：在项目的 pom.xml 中添加以下依赖坐标（8.0 版本后包名已更新为 mysql-connector-j）：
   - 旧版本（5.x）：`mysql:mysql-connector-java:5.1.49`
   - 新版本（8.0+）：`com.mysql:mysql-connector-j:8.0.33`
3. Gradle 依赖：在 build.gradle 中使用`implementation 'com.mysql:mysql-connector-j:8.0.33'`引入。


### 怎么配置连接

1. 驱动类名：使用`com.mysql.cj.jdbc.Driver`作为驱动类，8.0 版本后不再需要手动加载驱动类。
2. 连接方式：配置连接参数有三种常见方式：
   - 作为 JDBC URL 参数直接写在连接字符串里。
   - 通过 java.util.Properties 实例传递给 DriverManager.getConnection()。
   - 使用 MysqlConnectionPoolDataSource 数据源对象配置。
3. 常用配置属性：根据官方文档，以下配置项最常用：
   - user 和 password：数据库用户名和密码，所有版本都支持。
   - useSSL：是否启用 SSL 加密连接，默认值为 true。
   - characterEncoding：字符编码设置，避免中文乱码。
   - connectTimeout 和 socketTimeout：连接超时和读取超时时间，单位毫秒。
   - allowPublicKeyRetrieval：允许公钥检索，默认 false，某些场景需设为 true。

驱动配置里有些参数容易混淆，要不要看看 useSSL 和 allowPublicKeyRetrieval 的作用区别？ 或者 连接超时参数 connectTimeout 和 socketTimeout 如何设置？

# MVC演化史

[MVC演变_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=MVC%E6%BC%94%E5%8F%98)  

[从MVC到微服务：架构演化的历程](https://cloud.tencent.com/developer/article/2472458)  [MVC演化史](https://cloud.tencent.com/developer/article/1918032)  [MVC 及其演进架构](https://zhuanlan.zhihu.com/p/2052840883112915116)  [架构演进史：从 MVC 到 MVI 的脉络](https://zhengweiqiang.blog.csdn.net/article/details/169693778) [MVC架构演变与实战：从大泥球到分层治理的工程智慧](https://blog.csdn.net/weixin_32308101/article/details/167723772)   [从MVC到MVVM](https://blog.csdn.net/weixin_33416697/article/details/167723771)  [现代软件架构的演变：从MVC到Serverless](https://baijiahao.baidu.com/s?id=1826726345984047868&wfr=spider&for=pc)  

# 开源项目

[GitHub上非常实用的40个开源JAVA项目](https://cloud.tencent.com/developer/article/1954029)  

[Java三大框架级能力演进：Spring Boot、Quarkus与LangChain4J实战解析 ](https://www.csdn.net/detail/webblog_34581998/65766)  

## java开源项目现在都用什么框架

[github上java开源项目现在都用什么框架_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=github%E4%B8%8Ajava%E5%BC%80%E6%BA%90%E9%A1%B9%E7%9B%AE%E7%8E%B0%E5%9C%A8%E9%83%BD%E7%94%A8%E4%BB%80%E4%B9%88%E6%A1%86%E6%9E%B6)  

现在 GitHub 上 Java 开源项目用得最稳、最广的依然是 Spring Boot，尤其在 Web 后端、微服务和企业级应用中基本是默认选择。 但“现在都用什么”得分场景看，不同需求下主流框架差别挺大。

### 主流框架按场景分

1. **Web/后端开发**‌：‌ 
   1. Spring Boot 3.x‌ 是绝对主力，生态成熟、组件丰富，社区资料多，招人也好招。 轻量级替代品有 Quarkus（适合 Kubernetes 原生、低内存场景）和 Solon（国产轻量框架）

2. ‌**微服务架构**‌：‌ 
   1. Spring Cloud‌ 仍是主流，配套服务发现、网关、熔断等组件齐全。 若追求更高性能和更低资源占用，部分项目转向 Quarkus 或 Vert.x 构建的响应式微服务

3. ‌**AI/LLM 应用**‌：‌ 
   1. LangChain4J‌ 是 Java 接入大模型的热门选择，已成 Java 生态里 LLM 应用的事实标准接口层，常配合 Spring AI 一起用

4. ‌**数据库访问层**‌：‌ 
   1. MyBatis-Plus‌ 在国内项目使用率很高，‌Spring Data JPA‌ 在海外项目更常见。 轻量方案如 jOOQ 或 Ebean 也有一席之地

5. ‌**权限认证**‌：‌
   1. Sa-Token‌ 是国产开源里集成功能最全的权限框架，支持单点登录、OAuth2.0、微服务鉴权等；‌Spring Security‌ 仍是 Spring 生态的标准选择


### 实际使用率参考

2024 年生产环境数据，Spring Boot 使用率约 82.3%，MyBatis-Plus 约 67.1%，Lombok 约 59.8%。 这说明主流项目依然围绕 Spring 生态展开，但新框架在特定场景（如 IoT、Serverless、AI 应用）渗透很快。

### 选型提醒

框架热度不等于适合你的项目。启动耗时、内存占用、团队熟悉度、部署环境才是关键变量。 例如 Quarkus 原生镜像启动快、内存低，但热部署和动态加载支持不如 Spring Boot；若团队只熟 Spring，强行迁移可能得不偿失。

框架选择确实要权衡场景和团队，要不要再看看Quarkus和Spring Boot性能差距有多大?或者国产轻量框架Solon适合什么项目?

# 后台管理

## vue-element-admin

[Vue-Element-Admin使用](https://cloud.tencent.com/developer/article/2383228)  

vue-element-admin 的官方仓库是 https://github.com/PanJiaChen/vue-element-admin，该项目基于 `Vue 2 + element-ui` 构建，截至 2026 年 11 月已约 2 年未更新，属于停止维护状态。

### 项目简介与核心功能

1. 项目定位：vue-element-admin 是一个生产级的后台管理前端解决方案，基于 Vue 2 和 element-ui 组件库开发，帮助企业快速搭建复杂的中后台单页应用。
2. 核心功能特性：
   - 权限管理：支持基于角色的权限控制（RBAC）、按钮级权限、动态路由。
   - 国际化：内置 i18n 多语言解决方案，支持中英文切换。
   - 主题定制：支持多主题配置、深色模式、布局切换。
   - 丰富组件：包含富文本编辑器、Markdown 编辑器、Excel 导入导出、图表可视化等 50+ 业务组件。
   - 开发工具：集成 Mock 数据、SVG 图标、代码规范（ESLint + Prettier）。


### 技术栈与维护状态

1. 技术版本确认：
   - 前端框架：Vue 2.x（不是 Vue 3）。
   - UI 组件库：element-ui 2.x（Vue 2 专用组件库）。
   - 构建工具：vue-cli 4.x。
   - 状态管理：Vuex。
   - 注意：部分第三方文章声称基于 Vue 3 + Element Plus，这与官方仓库信息不符，应以官方 GitHub 为准。
2. 维护状态说明：
   - 最后更新时间：2024 年 10 月 24 日。
   - 当前状态：截至 2026 年 11 月 5 日，项目已约 2 年未更新，官方不再 active 维护。
   - 使用建议：如需 Vue 3 版本，可考虑社区 fork 版本或替代方案如 vue-admin-better、vue3-admin 等。

项目已停止维护，可以看看 替代方案 vue-admin-better 或者 Vue 3 版本的替代方案