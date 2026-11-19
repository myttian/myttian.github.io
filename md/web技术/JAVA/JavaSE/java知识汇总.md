# java运行机制

[java既有编译型又有解释型特点_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=java%E6%97%A2%E6%9C%89%E7%BC%96%E8%AF%91%E5%9E%8B%E5%8F%88%E6%9C%89%E8%A7%A3%E9%87%8A%E5%9E%8B%E7%89%B9%E7%82%B9)  

Java 被称为“编译与解释并存”的==混合型语言==，是因为其执行过程分为两个阶段：

1.  编译阶段：源代码（`.java`）通过 `javac` 编译器编译成平台无关的字节码（`.class`），这体现了编译型语言的特征。
2.  运行阶段：字节码由 JVM 加载执行。JVM 默认使用解释器逐条解释执行字节码（解释型特征）；同时，现代 JVM 内置 JIT（即时编译器），会将频繁执行的“热点代码”动态编译为本地机器码并缓存，以提升性能（编译型特征）。

```bash
# 编译：将源码编译为字节码
javac HelloWorld.java

# 运行：JVM 加载字节码，通过解释器或 JIT 执行
java HelloWorld
```

Java的混合特性挺有意思，要不要继续看看JIT编译的热点代码如何判断?或者解释执行和编译执行性能差异大吗?

# 构建工具

## java构建工具作用

[java构建工具作用_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=java%E6%9E%84%E5%BB%BA%E5%B7%A5%E5%85%B7%E4%BD%9C%E7%94%A8)  

[Lombok_百度百科](https://baike.baidu.com/item/Lombok/23780246)  [Java 构建工具 Gradle](https://www.runoob.com/java/java-gradle.html)  [Java构建工具对比](https://blog.csdn.net/KevinHuang2088/article/details/158702978)  [Gradle：构建自动化工具](https://cloud.tencent.com/developer/article/2422476)  [Java构建工具](https://blog.csdn.net/weixin_37097995/article/details/104787362)  

杂： [java构建器有什么用](https://docs.pingcode.com/insights/tzuam68skgkzl533davelpl4)  

Java构建工具的核心作用是自动化管理Java项目的==依赖、编译、测试、打包和发布==流程，省去手动下载jar包、敲命令行编译等繁琐易错的工作。

> 构建一个项目通常包含了依赖管理、测试、编译、打包、发布等流程，构建工具可以自动化进行这些操作

### 主要帮你做什么

1. 依赖管理：自动下载项目所需的第三方库（jar包）及其传递依赖。只需在配置文件声明依赖，工具自动从仓库拉取并放入本地缓存，避免手动寻找和版本冲突。
2. 编译打包：把 `.java` 源码编译成 `.class` 字节码，再打包成可运行的 `jar` 或 `war` 文件，一条命令搞定。
3. 自动化流程：标准化的项目结构和构建生命周期，可自动运行测试、生成报告、执行自定义任务（如代码扫描、静态检查）。

### 主流工具怎么选

- Maven：约定优于配置，用 `pom.xml`（XML）管理项目，结构标准、上手平缓，适合大多数传统项目。
- Gradle：用 `build.gradle`（Groovy/Kotlin）脚本配置，更灵活，支持增量构建和缓存，大型项目构建速度更快。
- Ant：老牌工具，灵活但缺乏依赖管理，现在用得较少。

> 简单说：Maven 规矩省心，Gradle 灵活快速，选哪个取决于项目规模和团队偏好。

构建工具各有侧重，要不要继续看看Maven和Gradle的依赖管理有何区别?或者为什么Maven用XML而Gradle用Groovy?

# java和c对比

## java实例相当于c语言结构体

[java实例相当于c语言结构体_百度搜索](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=java%E5%AE%9E%E4%BE%8B%E7%9B%B8%E5%BD%93%E4%BA%8Ec%E8%AF%AD%E8%A8%80%E7%BB%93%E6%9E%84%E4%BD%93&oq=java%25E5%25AE%259E%25E4%25BE%258B%25E7%259B%25B8%25E5%25BD%2593%25E4%25BA%258E%25E7%25BB%2593%25E6%259E%2584%25E4%25BD%2593&rsv_pq=800eddbb0008b6ea&rsv_t=2a8dLUa4PlIr8O5%2Br5QBNpEpRqJfyf7EVPjx%2BEz%2FVP4wzsH47lGD98hLDsI&rqlang=cn&rsv_enter=1&rsv_dl=tb_click&rsv_btype=t)  

Java实例和C语言结构体有相似之处，但不等同。Java实例（对象）可理解为“==升级版的结构体==”，==既包含数据（成员变量），也包含操作数据的方法（行为）==，而C结构体只能存数据，不能包含函数。

### 核心差异对比

| 对比维度   | C语言结构体            | Java实例（对象）         |
| ---------- | ---------------------- | ------------------------ |
| 数据成员   | 支持                   | 支持                     |
| 方法/函数  | 不支持，需外部函数操作 | 支持，方法属于类本身     |
| 访问控制   | 无，成员默认公开       | 支持private、public等    |
| 继承与多态 | 不支持                 | 支持                     |
| 内存管理   | 手动malloc/free        | JVM自动垃圾回收          |
| 变量语义   | 值语义，赋值即拷贝     | 引用语义，赋值只复制引用 |

### 关键区别

1. 行为封装：C结构体是“被动数据容器”，操作数据需写外部函数；Java类将数据和方法绑定，对象可“主动执行操作”。

2. 内存模型：C结构体变量存于栈，赋值拷贝整块内存；Java对象分配在堆，变量存的是引用（类似指针），赋值仅复制地址，两个引用指向同一对象。

3. 创建方式：Java用`new`关键字创建实例，类似C中`malloc`分配结构体内存，但JVM自动管理回收，无需手动free。

4. 编程范式：C是面向过程，结构体是组织数据的工具；Java是面向对象，类是抽象模板，实例是具体实体，支持继承和多态。

> 类比理解：若C结构体是“一袋零件”，Java实例就是“组装好的机器”——零件（数据）和说明书（方法）打包在一起，还能按图纸（类）批量生产，甚至通过继承扩展功能。

理解此差异，从C转向Java时，思维需从“如何操作数据”转为“对象能做什么”。

Java对象和C结构体差异不小，要不要继续看看Java中如何实现结构体的内存拷贝?或者Java中对象引用传递具体指什么?

## java变量和C变量

[java的类变量、实例变量、局部变量相当于c语言的什么存储类型_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=java%E7%9A%84%E7%B1%BB%E5%8F%98%E9%87%8F%E3%80%81%E5%AE%9E%E4%BE%8B%E5%8F%98%E9%87%8F%E3%80%81%E5%B1%80%E9%83%A8%E5%8F%98%E9%87%8F%E7%9B%B8%E5%BD%93%E4%BA%8Ec%E8%AF%AD%E8%A8%80%E7%9A%84%E4%BB%80%E4%B9%88%E5%AD%98%E5%82%A8%E7%B1%BB%E5%9E%8B) 

[Java中字段、属性、成员变量、局部变量、实例变量、静态变量、类变量、常量](https://www.cnblogs.com/shoshana-kong/p/10573474.html)  

[Java中的类，方法，成员变量相当于C语言中的什么](https://blog.csdn.net/m0_73739460/article/details/134692587)   

> 问题：java的类变量、实例变量、局部变量相当于c语言的什么存储类型

类变量相当于C语言的静态变量（static），实例变量相当于结构体成员（或全局变量），局部变量相当于自动变量（auto）。这是从存储位置、生命周期和作用域三个维度对应的。

### 对应关系详解

1. 类变量（static修饰）：对应C语言的静态变量（static）。两者都存储在静态存储区（Java中为方法区/元空间），在程序运行期间只分配一次内存，所有实例共享同一份数据，生命周期贯穿程序运行全程。

2. 实例变量（无static修饰）：最接近C语言的结构体成员变量。每个对象（结构体实例）拥有自己独立的副本，存储在堆内存中，随对象创建而分配、随对象回收而释放。

3. 局部变量：对应C语言的自动变量（auto）。两者都存储在栈内存中，在方法（函数）被调用时创建，执行结束后销毁，必须手动初始化后才能使用，作用域仅限于声明它的代码块内。

### 关键差异对照

| Java变量类型     | C语言对应          | 存储位置      | 生命周期            |
| ---------------- | ------------------ | ------------- | ------------------- |
| 类变量（static） | 静态变量（static） | 方法区/元空间 | 程序运行全程        |
| 实例变量         | 结构体成员         | 堆内存        | 随对象创建/回收     |
| 局部变量         | 自动变量（auto）   | 栈内存        | 随方法调用开始/结束 |

> 需要注意：Java的实例变量和C语言的全局变量在生命周期上有本质区别。实例变量属于每个对象独立持有，而C全局变量只有一份且被所有函数共享。更准确的类比是结构体成员，因为结构体成员也随实例独立分配。

类变量对应C的静态变量，要不要再看看Java类变量和C静态变量有何区别?或者C语言中结构体成员变量如何访问?

# 概念

## 实例变量

[java类里的变量叫做实例变量_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=java%E7%B1%BB%E9%87%8C%E7%9A%84%E5%8F%98%E9%87%8F%E5%8F%AB%E5%81%9A%E5%AE%9E%E4%BE%8B%E5%8F%98%E9%87%8F)  

> 问题：java类里的变量叫做实例变量

是的，Java类中定义在方法外部、且没有`static`修饰的变量称为实例变量（Instance Variable），也常被称为成员变量或非静态成员变量。

- 实例变量‌（Instance Variable）和‌==静态变量‌==（Static Variable，也==称类变量==）是两种核心的成员变量类型。它们在归属、内存分配、生命周期、访问方式以及线程安全性等方面存在显著差异

### 关键特性：

1. 归属：属于对象实例，每个对象拥有独立的副本。
2. 生命周期：随对象创建而存在，随对象被GC回收而销毁。
3. 默认值：无需显式初始化，JVM会自动赋予默认值（数值型为0，boolean为false，引用类型为null）。
4. 访问方式：必须通过对象实例访问（`对象名.变量名`）。

```java
public class Student {
    // 实例变量：每个Student对象都有独立的name和age
    private String name; 
    private int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void showInfo() {
        // 直接访问实例变量
        System.out.println("Name: " + name + ", Age: " + age);
    }

    public static void main(String[] args) {
        Student s1 = new Student("Alice", 20);
        Student s2 = new Student("Bob", 22);
        
        s1.showInfo(); // Name: Alice, Age: 20
        s2.showInfo(); // Name: Bob, Age: 22
        
        // 修改s1不影响s2，证明是独立副本
        s1.name = "Charlie";
        s2.showInfo(); // Name: Bob, Age: 22
    }
}
```

实例变量和静态变量是两个概念，可以看看==实例变量和静态变量==有何区别? 或者为什么实例变量需要显式初始化?

## 类变量

Java类变量就是用 `static` 关键字修饰的成员变量，属于类本身，所有对象共享同一份数据。 核心特点：类加载时就初始化，不依赖对象实例，推荐用“类名.变量名”访问。

- 类变量又叫静态变量

### 定义与访问

```java
public class Student {
    // 类变量（静态变量）
    public static int count = 0;
    
    // 实例变量（普通成员变量）
    private String name;
    
    public Student(String name) {
        this.name = name;
        count++;  // 每创建一个对象，count加1
    }
}

// 访问类变量：直接用类名，无需创建对象
System.out.println(Student.count);  // 输出：0
new Student("小明");
new Student("小红");
System.out.println(Student.count);  // 输出：2
```

### 关键规则

1. 定义语法：`访问修饰符 static 数据类型 变量名`，如 `public static int totalCount;` 
2. 访问方式：推荐`类名.变量名`，也可以用`对象名.变量名`，但不推荐（容易误导）
3. 初始化时机：类加载时自动初始化，即使没创建对象也能访问 
4. 默认值：有默认值（int→0，引用类型→null），不用手动赋值 
5. 生命周期：随类的加载而创建，随程序结束或类卸载而销毁 

### 注意事项

- 静态方法限制：静态方法只能访问静态成员，不能直接访问实例变量或使用 `this`、`super` 
- 线程安全：类变量是全局共享的，多线程同时修改需要同步控制 
- 命名规范：常量用全大写加下划线，如 `MAX_VALUE`；非常量静态变量用驼峰 
- 不要滥用：只有真正需要所有对象共享的数据才用类变量，比如计数器、全局配置 

### 典型使用场景

- 计数器：统计创建了多少个对象 
- 常量定义：`public static final double PI = 3.14159;` 
- 单例模式：用静态变量存储唯一实例 
- 工具类：如 `Math` 类中的静态方法和常量 

> 把计数器写成实例变量是常见错误，那样每个对象都从0开始计数，失去统计意义；用 `static` 修饰后，所有对象操作的是同一个计数器。

类变量的使用场景不少，要不要继续看看单例模式中静态变量如何保证唯一性?或者工具类中静态方法有哪些设计要点?

# 知识点理解

## ==in是静态成员变量==而不是常量

[public final static InputStream in = null为什么是静态成员变量而不是常量_百度搜索](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=public%20final%20static%20InputStream%20in%20%3D%20null%E4%B8%BA%E4%BB%80%E4%B9%88%E6%98%AF%E9%9D%99%E6%80%81%E6%88%90%E5%91%98%E5%8F%98%E9%87%8F%E8%80%8C%E4%B8%8D%E6%98%AF%E5%B8%B8%E9%87%8F&oq=%25E9%259D%2599%25E6%2580%2581%25E6%2588%2590%25E5%2591%2598%25E5%258F%2598%25E9%2587%258F&rsv_pq=a73910370010bddf&rsv_t=8edaSwgjIEsDfQK9ArGU3cwRTiqZHlxWASehe4uWpw0aeR32HGqS0dDWh4Q&rqlang=cn&rsv_enter=1&rsv_dl=tb_enter&rsv_sug3=37&rsv_sug1=1&rsv_sug7=100&rsv_n=2&rsv_btype=t&prefixsug=public%2520final%2520static%2520InputStream%2520in%2520%253D%2520null%25E4%25B8%25BA%25E4%25BB%2580%25E4%25B9%2588%25E6%2598%25AF%25E9%259D%2599%25E6%2580%2581%25E6%2588%2590%25E5%2591%2598%25E5%258F%2598%25E9%2587%258F%25E8%2580%258C%25E4%25B8%258D%25E6%2598%25AF%25E5%25B8%25B8%25E9%2587%258F&rsp=0&inputT=16435&rsv_sug4=16436)  

> 问题： `public final static InputStream in = null`为什么是静态成员变量而不是常量

因为 `in` 虽然被 `final` 修饰，但它的值在编译期并不能确定，运行时还会被 JVM 重新赋值，所以它本质上不是编译期常量，而是静态成员变量。

### 关键区别在哪

常量和静态成员变量的核心区别，不在于有没有 `final`，而在于值是否在编译期就能确定。

- 真正的常量：`static final` 修饰基本类型或字符串，且值在编译期已知时，编译器会做“常量折叠”，直接把值内联到使用处，不触发类加载。
- `System.in` 的情况：它被声明为 `public static final InputStream in = null`，但 `InputStream` 是引用类型，初始值 `null` 只是占位。实际运行时，JVM 通过本地方法 `setIn0()` 把它重新指向标准输入流，`final` 只保证引用不能再次改变，但引用指向的对象内容可以变，而且这个赋值过程发生在运行时，不是编译期。

### 为什么还要用 static 和 final

1. `static` 的必要性：`System` 类不能被实例化（构造方法私有），`in` 必须属于类本身，这样你才能直接用 `System.in` 访问，不需要创建对象。
2. `final` 的意义：保证 `in` 这个引用一旦被 JVM 初始化指向标准输入流后，不会再被其他代码重新赋值，防止外部意外篡改标准输入流。虽然 `final` 限制了引用，但 JVM 内部通过 native 方法依然可以修改它，这是虚拟机层面的特殊处理。

> 这里有个容易混淆的地方：`static final` 并不等于常量。只有编译期能确定值的 `static final` 变量才是常量，像 `System.in` 这种运行时才被赋值的引用类型，只能算作不可重新赋值的静态成员变量。

System.in 的特殊处理挺有意思，要不要继续看看JVM 为什么能修改 static final 的引用?或者编译期常量折叠对性能有什么好处?

## java是值传递

[Java中的参数传递](https://www.cnblogs.com/Sweetp/p/16610689.html)   [Java 是值传递：深入理解参数传递机制](https://blog.csdn.net/qq_57828911/article/details/155860308)  

> Java 中的传递，是值传递，而这个值，实际上是对象的引用。
>
> - 传递的值在栈中，直接拷贝一份值传递，改变的形参不会对实参造成影响
> - 传递的值在栈中存放的是地址（引用），先==根据栈中的地址找到在堆上的值，然后把地址拷贝一份（拷贝的地址是一个值）==，此时形参和实参指向堆上同一个地址，形参的修改导致了实参的改变。

**Java 通过引用来操作对象，但向方法传递引用时，是按值传递的**

- 对象本身存储在堆内存中。
- 变量（如 `List<String> list`）**不是对象本身**，而是**指向对象的引用（可理解为地址）**。
- 当你把 `list` 传给方法时，**传递的是这个“地址”的副本**，而不是地址本身

----

[java是值传递_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=java%E6%98%AF%E5%80%BC%E4%BC%A0%E9%80%92)  

==Java 中只有值传递==。

**基本数据类型**：传递的是数值的副本，方法内修改不影响外部变量。
**引用数据类型**：传递的是对象内存地址（引用）的副本。

- 通过副本地址修改对象属性（如 `obj.setName()`），会影响原对象，因为指向同一块堆内存。
- 修改形参指向（如 `obj = new Object()`），不会影响外部实参，因为只是改变了副本地址的指向，原实参地址未变。

```java
public class PassByValueDemo {

    static class User {
        String name;
        User(String name) { this.name = name; }
    }

    public static void main(String[] args) {
        // 1. 基本类型：值传递，修改副本不影响原值
        int num = 10;
        changeInt(num);
        System.out.println("Basic type: " + num); // 输出: 10

        // 2. 引用类型：传递地址副本
        User user = new User("Alice");
        
        // 2.1 修改对象内容：影响原对象（因为地址相同，操作的是同一对象）
        changeName(user);
        System.out.println("After changeName: " + user.name); // 输出: Bob

        // 2.2 修改引用指向：不影响原引用（因为只改了副本的地址指向）
        changeReference(user);
        System.out.println("After changeReference: " + user.name); // 输出: Bob (未被改为 Charlie)
    }

    static void changeInt(int n) {
        n = 20;
    }

    static void changeName(User u) {
        u.name = "Bob"; // 通过地址副本找到对象并修改属性
    }

    static void changeReference(User u) {
        u = new User("Charlie"); // 让形参指向新对象，实参不受影响
    }
}
```

Java的值传递机制确实有意思，要不要再看看为什么Java不采用引用传递?或者其他语言比如Python是值传递吗?

## ==对象作为参数==传递给一个方法

[通俗解释对象可作为参数传入另一个类的方法_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=%E9%80%9A%E4%BF%97%E8%A7%A3%E9%87%8A%E5%AF%B9%E8%B1%A1%E5%8F%AF%E4%BD%9C%E4%B8%BA%E5%8F%82%E6%95%B0%E4%BC%A0%E5%85%A5%E5%8F%A6%E4%B8%80%E4%B8%AA%E7%B1%BB%E7%9A%84%E6%96%B9%E6%B3%95)  

[从小学生视角解释对象可作为参数传递给一个方法_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=%E4%BB%8E%E5%B0%8F%E5%AD%A6%E7%94%9F%E8%A7%86%E8%A7%92%E8%A7%A3%E9%87%8A%E5%AF%B9%E8%B1%A1%E5%8F%AF%E4%BD%9C%E4%B8%BA%E5%8F%82%E6%95%B0%E4%BC%A0%E9%80%92%E7%BB%99%E4%B8%80%E4%B8%AA%E6%96%B9%E6%B3%95)  

[对象作为函数参数、类外定义成员函数](https://www.cnblogs.com/qlwy/archive/2011/08/09/2132120.html)  [对象作为参数传递给一个方法](https://blog.csdn.net/manchew/article/details/87085151)  

对象可以作为参数传入另一个类的方法，这是面向对象编程中非常基础且常用的操作。简单说，就是你把一个对象“递”给另一个类的方法，让那个方法能读取或修改这个对象的数据。

### 核心概念

1. 传递的是引用，不是对象本身：当你把对象传给方法时，方法拿到的是指向该对象的“地址”（引用），而不是把整个对象复制一份。所以方法内部修改对象的属性，会影响原对象。
2. 不同语言表现略有差异：
   - Java：严格是“值传递”，但对象类型传递的是“引用的副本”，所以可以修改对象内容，但不能让外部引用指向新对象。
   - Python：类似，传递对象引用，可变对象（如list、自定义类实例）在方法内修改会影响到外部。
   - C++：支持三种方式——值传递（复制对象）、指针传递、引用传递，后两种能直接修改原对象，效率更高。

### 简单示例（Java）

```java
class Student {
    String name;
    int age;
    
    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

class ScoreManager {
    // 接收Student对象作为参数
    void addBonus(Student s, int bonus) {
        s.age += bonus;  // 修改对象属性，外部可见
        System.out.println(s.name + " 年龄变为: " + s.age);
    }
}

public class Main {
    public static void main(String[] args) {
        Student stu = new Student("小明", 20);
        ScoreManager sm = new ScoreManager();
        
        sm.addBonus(stu, 5);  // 把stu对象传给另一个类的方法
        System.out.println("外部打印: " + stu.age);  // 输出25，被修改了
    }
}
```

### 需要注意的点

- 方法内重新赋值参数，不会影响外部原变量。比如 `s = new Student(...)` 只是让局部变量指向新对象，外部引用不变。
- 不可变对象（如Java的String、Python的tuple）作为参数时，看起来像“值传递”，因为无法原地修改。
- 传null要小心：方法内部若没做判空处理，直接访问对象属性会抛空指针异常。

### 为什么要这么设计

- 数据共享：多个方法可以操作同一个对象，避免重复创建和传递一堆零散变量。
- 代码复用：方法只需写一次，就能处理任意该类型的对象，配合多态还能接收子类对象。
- 性能好：只传引用（地址），不用复制整个对象，尤其对象大时优势明显。

想深入的话，可以看看Java值传递和C++引用传递的具体区别，或者Python可变对象与不可变对象的传参差异。

对象作为参数传递时，不同语言的处理方式有差异，可以看看Java中传入对象后，如何防止外部修改?或者Python中如何让方法无法修改对象属性?

## new Scanner(System.in)

`new Scanner(System.in)`

`System.in` 是 Java 的标准输入流，类型为 `InputStream`，默认关联键盘，用于从控制台读取用户输入的数据。

### 它的作用

`System.in` 是 `System` 类中的静态成员变量，由 JVM 启动时自动创建，本质是字节流。它只负责“提供原始字节”，读取时较繁琐，因此通常配合 `Scanner` 等工具类使用——`Scanner` 将字节流转换成易处理的字符串、整数等类型。

### 注意点

- 不要关闭它：`System.in` 是 JVM 管理的全局资源，调用 `scanner.close()` 会连带关闭它，导致后续无法再读取输入。
- 可重定向：通过 `System.setIn()` 可将输入源从键盘改为文件或网络流，增加程序灵活性。

System.in 是字节流，读取时确实不太方便，可以看看为什么需要配合Scanner等工具类?或者System.setIn()怎么把输入改成文件?

## 对象可作为参数

[new Scanner(System.in)是不是说明一个类的变量可作为另一个类的参数传入_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=new%20Scanner(System.in)%E6%98%AF%E4%B8%8D%E6%98%AF%E8%AF%B4%E6%98%8E%E4%B8%80%E4%B8%AA%E7%B1%BB%E7%9A%84%E5%8F%98%E9%87%8F%E5%8F%AF%E4%BD%9C%E4%B8%BA%E5%8F%A6%E4%B8%80%E4%B8%AA%E7%B1%BB%E7%9A%84%E5%8F%82%E6%95%B0%E4%BC%A0%E5%85%A5)  

Java中一个类的==对象可以作为另一个类方法的参数传入==。 在 `new Scanner(System.in)` 中，`System.in` 是 `InputStream` 类型的对象，而 `Scanner` 的构造方法接收这个对象作为参数，从而创建出一个能读取控制台输入的 `Scanner` 实例。

### 拆解一下这行代码

1. `System.in`：是 `InputStream` 类的静态成员变量，代表标准输入流（通常是键盘），它本身就是一个对象。
2. `Scanner` 的构造方法：`Scanner` 类中定义了接收 `InputStream` 类型参数的构造方法，所以可以把 `System.in` 传进去。
3. `new Scanner(System.in)`：调用构造方法创建 `Scanner` 对象，将 `System.in` 这个对象作为参数传入，让 `Scanner` 绑定到标准输入流上。

### 关键点

- 这里传递的是对象的引用，不是类本身。`System.in` 是 `InputStream` 的一个实例，`Scanner` 的构造方法接收的是 `InputStream` 类型的参数，两者类型匹配，所以可以传。
- 这属于通过方法/构造方法参数在不同类之间传递对象，是Java面向对象编程中很常见的做法。
- 同理，你也可以把 `Scanner` 对象本身作为参数传给其他方法或类，比如 `processData(Scanner sc)`，这样就能在别处复用同一个 `Scanner` 实例读取输入。

> 注意：不要重复创建多个 `Scanner` 实例来读取同一个 `System.in`，因为 `System.in` 的底层数据会被消费掉，多个 `Scanner` 可能导致读取异常，最好在 `main` 中创建一个然后传下去复用。

Java中对象传递是引用传递，可以再看看为什么Scanner不能重复创建?或者除了Scanner，还有哪些常见类用到对象传递?

## 对象作用

对象除了作为参数传递，==核心作用是把数据和操作数据的逻辑打包在一起==，让代码更贴近现实事物的组织方式。它远不止是“传数据的容器”，主要作用如下：

### 组织代码与状态管理

对象能把相关属性和方法封装在独立单元里，避免全局变量和散落函数乱成一团。比如`Student`对象同时持有`name`、`age`和`say_hi()`方法，状态和行为由对象自己管理，外部通过接口访问，而不是到处传一堆零散变量。

### 封装与信息隐藏

对象可控制内部数据访问权限，保护状态不被随意修改。比如`BankAccount`的`balance`设为私有，只能通过`deposit()`方法修改，防止外部直接篡改导致数据不一致，降低模块间耦合度。

### 代码复用（继承）

通过继承，子类自动获得父类的属性和方法，可扩展或覆写。比如`Car`继承`Vehicle`，不用重新写轮子、引擎相关逻辑，直接复用父类实现，只加自己特有的`doors`属性，减少重复代码。

### 灵活扩展（多态）

不同类的对象可响应同一接口调用，但各自实现不同。比如`Dog`和`Cat`都有`speak()`方法，用统一列表存起来遍历调用，程序运行时根据实际类型执行对应逻辑，新增类型时无需改动原有代码。

### 建模复杂业务与设计模式

对象适合模拟现实世界的实体和关系，比如订单、用户、角色。配合设计模式解决常见问题：单例模式保证一个类只出一个实例（如配置管理器），观察者模式实现对象间一对多通知，工厂模式封装创建逻辑，让系统结构更清晰。

### 作为命名空间与组织单位

对象可把相关功能归拢在一起，避免命名冲突。比如`MathUtils`对象提供`add`、`subtract`方法，通过`MathUtils.add()`调用，不用把工具函数散落全局，也方便查找和维护。

### 管理生命周期与资源

对象有创建和销毁过程，可控制资源释放时机。比如文件对象在析构时自动关闭句柄，或垃圾回收机制自动回收无引用的对象，避免手动管理内存带来的泄漏和野指针问题。

> 对象本质上是把“数据”和“行为”绑在一起，用封装{id="entity_1"}、继承{id="entity_2"}、多态{id="entity_3"}三大特性，让代码更易维护、扩展和复用。但也不是万能药，简单脚本或性能极端敏感场景，面向过程反而更直接高效。

==对象的核心价值在于封装==，要不要继续看看封装如何提升代码安全性?或者继承和多态如何协同工作?

## ==方法参数有哪些==

[java里面什么东西可作为方法参数使用_百度搜索](https://www.baidu.com/s?ie=utf-8&f=3&rsv_bp=1&tn=baidu&wd=java%E9%87%8C%E9%9D%A2%E4%BB%80%E4%B9%88%E4%B8%9C%E8%A5%BF%E5%8F%AF%E4%BD%9C%E4%B8%BA%E6%96%B9%E6%B3%95%E5%8F%82%E6%95%B0%E4%BD%BF%E7%94%A8&oq=%25E5%25AF%25B9%25E8%25B1%25A1%25E9%2599%25A4%25E4%25BA%2586%25E4%25BD%259C%25E4%25B8%25BA%25E5%258F%2582%25E6%2595%25B0%25E4%25BC%25A0%25E9%2580%2592%252C%25E8%25BF%2598%25E6%259C%2589%25E5%2593%25AA%25E4%25BA%259B%25E4%25BD%259C%25E7%2594%25A8&rsv_pq=82836c7e00108f48&rsv_t=a4aaqdnhA2lgPrE4n%2BGN0hKYoXBI%2BSGKk4h5ZfIBZkT6ymzbRyJf6jsL8Q0&rqlang=cn&rsv_enter=1&rsv_dl=ts_0&rsv_sug3=49&rsv_sug1=8&rsv_sug7=100&rsv_btype=t&prefixsug=java%25E9%2587%258C%25E9%259D%25A2%25E4%25BB%2580%25E4%25B9%2588%25E4%25B8%259C%25E8%25A5%25BF%25E5%258F%25AF%25E4%25BD%259C%25E4%25B8%25BA%25E6%2596%25B9%25E6%25B3%2595%25E5%258F%2582%25E6%2595%25B0%25E4%25BD%25BF%25E7%2594%25A8&rsp=0&inputT=21955&rsv_sug4=29076)  

在Java里，==几乎任何东西都能作为方法参数==，包括`基本数据类型、对象、数组、接口实现，甚至方法本身（通过函数式接口）`

### 常用参数类型

1. 基本数据类型：`int`、`double`、`char`、`boolean` 等8种，传的是值的副本，方法内改不影响原变量。
2. 类/对象：自定义类或JDK类，如 `String`、`List`、`Person`。传的是引用副本，改对象属性影响原对象，但重新赋值引用不影响外部。
3. 数组：`int[]`、`String[]` 等，本质是引用类型，方法内改数组元素会影响原数组。
4. 接口/抽象类：传接口类型，实参可为任何实现类对象，多态基础。
5. 可变参数（varargs）：`void print(String... names)`，编译后是数组，可传任意数量参数或不传。
6. 泛型参数：`<T> void process(T item)`，类型安全抽象，集合类常用。
7. 函数式接口：自Java 8起，可传Lambda表达式或方法引用，如 `Runnable`、`Function<T,R>`、`Consumer<T>`。

### 把方法本身当作参数

Java中方法不能直接作为参数，但可用以下方式实现“行为参数化”：

- Lambda表达式：`execute(() -> System.out.println("Hello"))`，最简洁。
- 方法引用：`this::add`，直接引用已有方法。
- 函数式接口：定义接口，用匿名内部类或Lambda实现。

> 关键点：Java只有值传递，传对象时传的是“引用地址的副本”，不是引用传递。方法内改对象属性会影响原对象，但重新赋值形参不影响外部引用。

Java参数传递机制挺有意思，要不要继续看看为什么Java是值传递而不是引用传递?或者可变参数和普通数组有什么区别?

## 方法参数

[参数：让方法接收外部的数据](https://blog.csdn.net/zjlovesms/article/details/169727150)  

方法参数就是==把外部数据传进方法里，让方法能读取或修改这些数据==。 但不同语言对“能不能改到外面”的规则不一样，这正是容易混淆的地方。

> 参数能让方法更灵活地接收和处理外部数据，这样代码的复用性和扩展性都会好很多

### 核心规则：传的到底是“副本”还是“本身”

1. 值传递（Pass by Value）：传递的是实参的副本。方法内改的是副本，外面原变量不受影响。Java 和 `C#`默认都是这种机制。
2. 引用传递（Pass by Reference）：传递的是实参的引用（地址）。形参和实参指向同一块内存，方法内修改会直接反映到外部。C++ 的引用、`C#`的 `ref` 属于此类。

### 各语言表现差异

- Java：严格只有值传递。基本类型传值的副本，改形参不影响原变量；引用类型传“地址的副本”，通过该地址修改对象属性会影响外部，但重新赋值形参指向新对象则不影响外部。
- `C#`：默认值传递，但可用 `ref`、`out`、`in` 关键字显式实现引用传递。`ref` 要求变量先初始化，`out` 不要求且方法内必须赋值，`in` 是只读引用。
- C++：三种方式并存——值传递（拷贝）、指针传递（传地址，通过解引用修改原值）、引用传递（形参是实参的别名，直接操作原变量）。
- Python：一切皆对象，传递的是对象引用。不可变类型（int、str、tuple）表现像值传递，改形参不影响外部；可变类型（list、dict、set）表现像引用传递，方法内修改对象内容会反映到外部。

### 最容易踩的坑

> 判断能否修改外部值，关键看修改的是“副本本身”还是“副本指向的对象”。若方法内重新给形参赋值（如 `p = new Person()`），改的只是形参的指向，外部变量不受影响；若通过形参修改对象属性（如 `p.name = "李四"`），因为形参和实参指向同一个对象，外部能感知到变化。

- 值类型（int、double 等）：改形参，外面不变。
- 引用类型改属性：外面跟着变。
- 引用类型重新赋值：外面不变。

### 想真正修改外部变量怎么办

1. `C#`：用 `ref` 关键字，如 `void Change(ref int x)`，调用时写 `Change(ref num)`。
2. C++：用指针（`int* p`）或引用（`int& r`），传地址或别名进去。
3. Java：没有直接办法修改基本类型原值，可改传数组或自定义包装类，通过修改对象属性来间接实现。
4. Python：传可变对象（如 list、dict），在方法内修改其内容即可。

不同语言的规则差异挺大，要不要继续看看Java中如何修改外部数组?或者Python中如何修改外部字典?

# 注解

## 注解

[注释与注解的区别](https://blog.csdn.net/xfwayz/article/details/47257495)  [Spring注释配置](https://blog.csdn.net/xyh820/article/details/7303330/)  

注释是给人看的，注解是给程序（编译器、虚拟机、框架）看的。简单说，注释是写代码时留下的说明文字，帮人理解逻辑；==注解是给代码贴的“标签”，程序运行时会读取并处理==。

> 注解：主要是给程序看的，告诉程序这个东东是干嘛的
>
> - 比如@Componet 就告诉spring框架这是个组件，仅仅如此
> - 告诉程序不能代表程序就要执行（比如加载）这个组件，只有配置到了扫描路径，spring看到了知道这是个bean，把你放进来，才能说这个组件加载完成。以后可以注入到其它bean中

### 核心区别

1. 注释：只存在于源码中，编译后会被擦除，不影响程序运行。作用是解释代码逻辑、方便维护和协作。
2. ==注解==：编译后保留在 class 文件中（取决于保留策略），能被编译器、框架或运行时反射机制读取，并据此执行操作。

### 注解的实际用途

- 编译检查：如 `@Override` 告诉编译器此方法重写父类方法，签名不对直接报错。
- 配置替代：如 Spring 的 `@Service`、`@Mapper`，框架通过反射扫描注解，自动注册 Bean、创建代理、实现依赖注入，替代 XML 配置。
- 运行时处理：自定义注解配合反射，可读取注解上的参数值并执行逻辑，如模拟 JUnit 的 `@Test` 自动运行标记方法。

> 注解本身不改变代码逻辑，真正起作用的是“读取注解的程序”。注解只是标签，框架或编译器看到标签后才做对应处理。

注解的用途很广，可以看看自定义注解怎么定义和使用?或者注解的保留策略有哪些?

# 反射

## 反射

好： [JAVA反射机制_百度百科](https://baike.baidu.com/item/JAVA%E5%8F%8D%E5%B0%84%E6%9C%BA%E5%88%B6/6015990)   [Java反射机制](https://cloud.tencent.com/developer/article/2467563)  

[Java反射机制](https://cloud.tencent.com/developer/article/2690637)  

> 
>
> 动态语言： 程序运行时，允许改变程序结构或变量类型，这种语言称为动态语言
>
> - 从这个观点看，Perl，Python，Ruby是动态语言，C++，Java，C#不是动态语言
>
> java的动态机制
>
> - 可以于运行时加载、探知、使用编译期间完全未知的classes。
>   - 换句话说，Java程序可以加载一个运行时才得知名称的class，获悉其完整构造（但不包括methods定义），并生成其对象实体、或对其fields设值、或唤起其methods
> - **运行时动态地获取和操作类、对象、方法和属性的能力**。
>   - 它允许程序在编译时不需要知道类的具体信息，而是在运行时通过反射机制来获取所需的信息。
>   - 通过反射，我们可以在运行时检查类的属性和方法，并且可以在运行时创建对象、调用方法和访问属性

Java 反射允许程序在运行时动态获取类信息，并创建对象、调用方法和访问属性，从而提高代码的灵活性与可扩展性。
- 获取类信息：读取类名、构造器、方法、字段等元数据。
- 动态创建对象：根据类名在运行时实例化对象。
- 调用方法与访问属性：包括公有、私有成员的读取与修改。
- 典型应用：框架依赖注入、动态代理、注解解析、序列化等。



反射也存在性能损耗和安全风险，业务代码中应谨慎使用，框架底层则广泛依赖。

反射虽然强大，但使用时也有不少细节，比如 反射能访问私有属性吗？ 或者 反射调用方法会丢失重载吗？

## 为什么用反射

[有对象就知道类的全部,为什么还要有反射机制_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=%E6%9C%89%E5%AF%B9%E8%B1%A1%E5%B0%B1%E7%9F%A5%E9%81%93%E7%B1%BB%E7%9A%84%E5%85%A8%E9%83%A8%EF%BC%8C%E4%B8%BA%E4%BB%80%E4%B9%88%E8%BF%98%E8%A6%81%E6%9C%89%E5%8F%8D%E5%B0%84%E6%9C%BA%E5%88%B6)  

问题： 有对象就知道类的全部,为什么还要有反射机制

“有对象就知道类的全部”这个前提，只在编译期类型已知、且你手头已经拿到具体对象时成立。反射解决的是编译期完全不知道类名、类还没加载、甚至要绕过访问权限的场景，这是直接调用做不到的。

### 🔍 核心区别：编译期 vs 运行期

- 直接调用：`Person p = new Student()`，编译时已确定类型，JVM 在编译期绑定好一切，运行时不需额外查探。
- 反射：编译时只拿到字符串 `"com.example.Student"`，类可能尚未加载到 JVM。运行时通过 `Class.forName()` 动态加载、解析结构、创建实例、调用方法。

> 关键点：若代码里写死 `new ClassName()`，编译期就必须知道类存在；反射则允许“类名在配置文件里、运行时才读出来”，此时编译期根本不知道要操作谁。

### 🛠️ 反射不可替代的场景

1. 框架的依赖注入：Spring 读取 XML 或注解里的类名字符串，用反射创建 Bean 对象，再注入依赖。它不可能在编译期写死所有用户自定义的类。
2. 动态代理与 AOP：代理对象在运行时生成，目标方法在编译期未知。反射的 `invoke` 可在方法前后织入事务、日志等逻辑。
3. 通用工具与序列化：Jackson、Gson 等 JSON 库无需你写 getter/setter 调用代码，反射读取对象字段名和值，自动完成序列化和反序列化。
4. 插件体系：程序运行时从外部加载 DLL 或 JAR，通过配置里的类路径调用插件功能。编码阶段根本不知道插件类名，只能靠反射。
5. 测试私有成员：单元测试需覆盖 private 方法或字段时，反射可绕过访问控制直接调用，保证覆盖率。

### ⚠️ 反射的代价

- 性能低：反射是解释型操作，比直接调用慢几十到几百倍。高频路径需缓存 `Method` 对象或改用方法句柄优化。
- 破坏封装：能访问 private 成员，绕过了访问控制，可能带来安全隐患，代码逻辑也更难追踪。
- 放弃编译期检查：类名写错、方法签名不匹配，编译期发现不了，运行时才抛异常。

简单说：日常业务代码用不到反射，但写框架、做通用工具、实现插件化时，没有反射就玩不转。它是“框架的灵魂”，牺牲一点性能和安全性，换来灵活性和扩展性。

反射虽然灵活，但代价不小，要不要看看反射性能低的根本原因是什么?或者方法句柄如何优化反射性能?

# IDEA

## IDEA打开和导入项目区别

[idea打开和导入项目区别_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=idea%E6%89%93%E5%BC%80%E5%92%8C%E5%AF%BC%E5%85%A5%E9%A1%B9%E7%9B%AE%E5%8C%BA%E5%88%AB)  

[idea打开项目和导入项目区别](https://worktile.com/kb/p/3888555)  

> - 打开项目针对已存在的IDEA项目文件（.idea目录），能快速还原完整开发环境
> - 导入项目则用于非IDEA创建或外部项目，需重新配置SDK、依赖等参数
> - 关键差异在于项目元数据的处理， 打开项目直接读取已有配置，导入项目可能触发重构或配置转换

打开项目适合已有 IDEA 配置的项目，导入项目则面向非 IDEA 项目或需重新构建配置的场景，核心差异在配置继承与文件处理方式。

### 核心区别

1. 操作对象不同：打开项目针对含 `.idea` 配置目录的完整 IDEA 项目，直接读取 `modules.xml`、`workspace.xml` 等文件，还原运行配置、代码索引和版本控制信息；导入项目面向 Eclipse 项目、纯源码或从 Git 克隆的代码，IDEA 会扫描结构并重新生成配置。
2. 配置处理方式不同：打开项目直接继承原有配置，开箱即用，但可能带入过时配置（如旧 JDK 路径）；导入项目会启动向导，重新分析项目结构、下载依赖、重建索引，可能覆盖或丢失部分原有定制设置（如代码模板、运行参数）。
3. 耗时差异明显：打开项目复用已有缓存，大型项目通常几秒到二十秒；导入需重新构建索引和依赖关系，中型项目可能耗时数分钟。

### 怎么选

- 直接用打开：项目之前用 IDEA 开发过，或从版本控制克隆的 IDEA 项目，`.idea` 目录存在且配置完整。
- 用导入：项目来自 Eclipse、VS Code 等其他 IDE，或只有源码目录和构建文件（如 `pom.xml`、`build.gradle`），没有 IDEA 配置。
- 换环境时优先导入：把项目从一台机器拷贝到另一台时，用导入重新生成配置，避免残留旧环境的 JDK 路径等设置。

> 单个 Maven 项目用打开或导入差别不大；但多模块项目同时导入时，`Import Project` 可能无法直接识别，需用打开后再通过 `File -> New -> Module from Existing Sources` 补充导入。

两种操作的耗时差异也挺关键，可以看看导入项目耗时多久算正常或者打开项目卡住怎么处理

# Java技术栈

## Java技术栈

[java技术栈_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=java%E6%8A%80%E6%9C%AF%E6%A0%88)  

Java 技术栈涵盖语言基础、Spring 生态框架、数据库与中间件、微服务架构组件，2026 年企业级应用以云原生和 AI 集成为主流方向。

### 核心组成部分

1. 语言与运行时基础：Java 语言核心包括面向对象编程、集合框架、并发包、Lambda 表达式等，JVM 提供跨平台运行能力，垃圾回收机制（G1、ZGC）和内存管理是高阶必备技能。
2. 主流开发框架：Spring 生态占据主导地位，Spring Boot 通过自动配置和 Starter 机制简化项目搭建，Spring Cloud 支持微服务分布式治理，ORM 框架包括 Hibernate（全自动）和 MyBatis（半自动）。
3. 数据与中间件：关系型数据库以 MySQL、PostgreSQL 为主，Redis 作为缓存广泛应用，消息队列包括 Kafka、RabbitMQ，搜索引擎使用 Elasticsearch。
4. 工程化与运维：构建工具采用 Maven 或 Gradle 管理依赖，版本控制使用 Git，部署运维涉及 Docker 容器化、Kubernetes 编排、==CI/CD 流水线（Jenkins）==，日志监控采用 ELK、Prometheus。


### 2026 年技术趋势

1. ==云原生架构==：`Spring Boot、Quarkus、Micronaut、Helidon` 等框架成为云原生 Java 微服务主流选择，支持容器优先默认配置，降低冷启动时间和内存占用。
2. ==AI 集成能力==：Java 技术栈向 AI 应用平台演进，包含应用平台、数据平台、AI 平台三层架构，`Spring AI、LangChain4j` 等库支持大语言模型、向量搜索、自然语言交互功能。
3. 多语言共存：Java 在金融、医疗、航空等受监管行业保持优势，与 Rust、Go、Kotlin 等语言形成多语言开发生态，62% 企业已将 Java 用于 AI 功能集成。


### 企业级应用标准

1. 采用率数据：2026 年 99% 的组织活跃使用 Java，近 70% 的企业应用中超过一半基于 Java 或运行在 JVM 上，62% 的财富 500 强企业使用 Java。
2. 行业分布：Java 在金融、电信、制造和互联网行业仍是主流后端开发语言，每日处理万亿美元级别的金融交易量。
3. 迁移趋势：81% 的企业正将 Oracle Java 环境迁移至 OpenJDK 发行版，TIOBE 指数中 Java 排名前列，虽开发者关注度被 Python 超越但企业部署足迹更深。

Java 技术栈涉及面很广，要不要继续看看 Spring Boot 和 Spring Cloud 的区别 或者 JVM 垃圾回收机制有哪些类型

# 未分类

## 三、重构

[参数对象如何简化方法参数](https://www.bilibili.com/read/cv17207985/)

*Introduce* *Parameter* Object (引入*参数*对象)



## 四、插件

[String Manipulation](https://blog.csdn.net/qq_41489540/article/details/119394122)  [UML类图插件Diagram](https://baijiahao.baidu.com/s?id=1728907866202978067&wfr=spider&for=pc) [Idea的diagram](https://zhuanlan.zhihu.com/p/545768127)  [diagrams线条的含义](https://zhuanlan.zhihu.com/p/131390048?utm_id=0) [AJCG](https://www.cnblogs.com/mq0036/p/11824191.html) [阿里规范检测工具](https://www.jianshu.com/p/162cee372bb1?ivk_sa=1024320u)

1. String Manipulation  字符串处理
1. UML类图插件Diagram 
1. Alibaba Java Coding Guidelines： 处理方式仅限Blocker，其他需手动修正

## 五、工具库

[Java工具库](https://www.cnblogs.com/mahoshojo/p/15262192.html) [Java中好用的工具包](https://linuxcpp.0voice.com/?id=31527)  [ Java 开发网络爬虫工具包](https://www.zhihu.com/question/20960372)

[常用开发库-Apache Common包](https://www.pdai.tech/md/develop/package/dev-package-x-apache-common.html)  [Java的commons包](https://www.cnblogs.com/javahr/p/8275934.html) [Java开发工具](https://baijiahao.baidu.com/s?id=1701186881379549136&wfr=spider&for=pc) [Commons包的使用](https://www.cnblogs.com/duguangming/p/10610003.html)

## 六、学习网站

[推荐网站](https://www.bilibili.com/video/BV1aH4y117DN/?spm_id_from=333.1007.tianma.1-1-1.click&vd_source=7346303e5e18677d7261c2c0c109ecfd)

[大学资源网](https://www.dxzy163.com/)  [Stack Overflow](https://stackoverflow.com/)  [Learn Computer Science](https://studio.code.org/courses)  [力扣](https://leetcode.cn/) [freecodecamp](https://www.freecodecamp.org/chinese/)   [cppreference](https://en.cppreference.com/w) [牛客网](https://www.nowcoder.com/) [中国大学MOOC(慕课)](https://www.icourse163.org/) [慕课网](https://www.imooc.com/) [Coursera](https://www.coursera.org/) [Pluralsight + Code School](https://www.pluralsight.com/codeschool) 

医学：

[A+医学百科](http://www.a-hospital.com/index.php?direction=prev&oldid=414959)

[设127.0.0.1为了实现本地代理](https://zhuanlan.zhihu.com/p/668244570)

## 七、框架

[2023年Web开发的5个最佳Java框架](https://baijiahao.baidu.com/s?id=1763381342526254067&wfr=spider&for=pc)

java安全框架：

[SpringSecurity](http://i0921.cn/blog/5dc52b0aba304f6314a9229f/65c80e406b52af7adc795071) [java安全框架](https://blog.csdn.net/di101cipaqi/article/details/135680363)

[Jenkins 持续集成系统](https://market.aliyun.com/products/55530001?spm=5176.730005.filter.55530001&page=1)

## 八、云市场

云市场：

[阿里云市场](https://market.aliyun.com/products/53400005?k=&spm=5176.730005.filter.53400005&page=1&scene=market) 

桌面云：

[阿里无影云](https://www.aliyun.com/product/wuying/download?spm=5176.730005.0.0.6c7a77c6DwKvS2)  [桌面云架构讲解（VDI、IDV、VOI/TCI、RDS）](https://blog.csdn.net/m0_49864110/article/details/134375545)  

应用技术架构：

- [单体架构 & 垂直架构 & SOA 架构](https://cloud.tencent.com/developer/article/1957268)  [RPC框架有哪些](http://www.mobiletrain.org/about/BBS/115318.html) [SOA五种基本架构模式](https://zhuanlan.zhihu.com/p/651754019) [什么是SOA](https://cloud.tencent.com/developer/article/1361060)  [面向服务的软件架构SOA](https://blog.csdn.net/johnpub/article/details/127812255)  [SOA接口测试 ](https://zhuanlan.zhihu.com/p/527025085) 
- 面向服务的架构（SOA）： 有两种，==以企业服务总线（ESB）为代表的 SOA== 和==以 RPC 为代表的 SOA==
  - RPC
    - [Dubbo(远程过程调用)+ZooKeeper(分布式协调服务)](https://blog.csdn.net/m0_66689823/article/details/127710458)  [Dubbo上云](https://bp.aliyun.com/detail/132?spm=5176.730005.0.0.6c7a77c6DwKvS2) 

云市场应用：

[VR视频影院](https://market.aliyun.com/products/55530001/cmfw00059806.html?spm=5176.730005.result.18.6c7a77c6DwKvS2&innerSource=search#sku=yuncode5380600001)

新的架构：

[Kubernetes 的istio可以完全替代 Spring Cloud](https://www.zhihu.com/question/451313635?utm_id=0)  [Nomad 真的会替代 Kubernetes 吗？](https://zhuanlan.zhihu.com/p/577309655?utm_id=0)   [Nomad](https://www.oschina.net/p/nomad?hmsr=aladdin1e1)   

[可以替代Spring Boot的微服务框架](https://maimai.cn/article/detail?fid=1739158284&efid=yCZezXX2mTGk6-GXwrVYww)  [k8s替代springcloud](https://www.sparktry.com/2017/22561.html)  [Spring Cloud 2022.0.4发布](https://www.qinglite.cn/doc/524364c47cb842e53)  

[容器编排与调度工具除了k8s之外还有哪些](https://www.zhihu.com/question/323689729/answer/2977059149)  [容器编排工具的比较：Kubernetes、Docker Swarm、Nomad ](https://baijiahao.baidu.com/s?id=1774745731731727889&wfr=spider&for=pc)  [Nomad 会替代 Kubernetes ](https://blog.csdn.net/m0_37723088/article/details/130835523)  

[一个Spring Boot Admin 监控多个Nacos集群](https://itsaysay.blog.csdn.net/article/details/136099768?spm=1001.2101.3001.6650.16&utm_medium=distribute.pc_relevant.none-task-blog-2~default~BLOGTAG~default-16-136099768-blog-135707841.235^v43^pc_blog_bottom_relevance_base9&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BLOGTAG~default-16-136099768-blog-135707841.235^v43^pc_blog_bottom_relevance_base9&utm_relevant_index=17)  

[SpringBoot整合dubbo+zooker搭建分布式服务](https://blog.csdn.net/weixin_45344924/article/details/124113843) 