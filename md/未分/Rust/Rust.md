视频： [Rust入门](https://www.bilibili.com/video/BV1hp4y1k7SV/?vd_source=7346303e5e18677d7261c2c0c109ecfd)   [Rust Web 全栈开发](https://www.bilibili.com/video/BV1RP4y1G7KF/?vd_source=7346303e5e18677d7261c2c0c109ecfd)   [Rust](https://www.bilibili.com/video/BV15y421h7j7/?vd_source=7346303e5e18677d7261c2c0c109ecfd)  [Rust](https://www.bilibili.com/video/BV1xJ411B79h/?vd_source=7346303e5e18677d7261c2c0c109ecfd)  [2024 Rust](https://www.bilibili.com/video/BV15y421h7j7/?vd_source=7346303e5e18677d7261c2c0c109ecfd) 

[Rust-菜鸟教程](https://www.runoob.com/rust/rust-tutorial.html)   [Rust 官网](https://www.rust-lang.org/zh-CN/tools)   [rust权威指南](https://kaisery.github.io/trpl-zh-cn/foreword.html)  [Rust权威指南阅读笔记](https://www.cnblogs.com/Kroot/p/17948096) 

系统编程： [Linux系统编程](https://zhuanlan.zhihu.com/p/682540040)   [C++后台开发开源项目](https://www.zhihu.com/question/39169728/answer/3549867456)   [操作系统与内核、系统编程与应用编程](https://zhuanlan.zhihu.com/p/646371522) 

*Rust 语言由 Mozilla 开发，最早发布于 2014 年 9 月* 

# 搭建环境

[Windows上安装Rust开发环境](https://zhuanlan.zhihu.com/p/689630360)  [Rust学习](https://www.cnblogs.com/liufu627/p/12562646.html)  [Win7 VSCode 在线安装Rust语言及环境配置](https://www.cnblogs.com/kileyi/p/11374829.html)   

[Platform Support](https://doc.rust-lang.org/nightly/rustc/platform-support.html) [Microsoft C++ 生成工具](https://visualstudio.microsoft.com/zh-hans/visual-cpp-build-tools/)   [Other Installation Methods - Rust Forge](https://forge.rust-lang.org/infra/other-installation-methods.html)     [在Windows中安装MinGW-w64最新版本](https://blog.csdn.net/orangebench11/article/details/126111356) 

[Rust语言中文社区](https://rustcc.cn/) 

1. 下载 `mingw64`， `sysdm.cpl`环境变量path里添加 `mingw64\bin`     [MinGW-w64](https://www.mingw-w64.org/downloads/) 
2. 让 Rust使用`mingw64`编译   [RUST语言mingw-64开发环境安装和设置](https://zhuanlan.zhihu.com/p/556088822)   [Rust](https://www.cnblogs.com/Starsdust/p/17580173.html)  
   1. 卸载 `rustup self uninstall` 
   1. 更新 `rustup update`
   1. 本地文档 `rustup doc`

开发工具： vscode rust插件；   Clion rust插件

**Ubuntu**

[vscode 远程编译rust](https://blog.csdn.net/luckbin/article/details/134113003)   [如何使用VSCode进行Python远程开发](https://developer.baidu.com/article/details/3235396) 

```bash
# 要安装gcc
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh

# .bashrc
. "$HOME/.cargo/env" 
```



# 1、入门指南

## helloworld

```ruby
mkdir hello_world
cd h*
code .		// vscode新建项目

// 编译： rustc main.rs
```

变量

```ruby
let a = 123;			// 不可变变量
let mut a = 123;		// mut使变量可变

// 重影
// 数组 [ ]
// 元组 ( )

// 注释
```

-  

# 2、猜数字游戏

[crates.io: Rust Package Registry](https://crates.io/) 

```rust
use rand::Rng;
use std::cmp::Ordering;
use std::io;
fn main() {
    println!("猜数字游戏！");
    let secret_number = rand::thread_rng().gen_range(1, 101);
    // println!("神秘数字是:{}",secret_number);

    loop {
        println!("Please input your guess.");

        let mut guess = String::new();
        // 用户的输入放入字符串(guess)中，需要是可变的
        // &取地址符号，表示参数是引用，通过引用在代码不同地方，访问同一块数据； 方法的参数按引用进行传递； 指向同一块内存地址，同一块数据
        io::stdin().read_line(&mut guess).expect("无法读取行");

        let guess: u32 = match guess.trim().parse() {
            Ok(num) => num,
            Err(_) => continue,
        };
        println!("You guessed: {}", guess);

        match guess.cmp(&secret_number) {
            Ordering::Less => println!("Too small!"),
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal => {
                println!("You win!");
                break;
            }
        }
    }
}
```

# 3、常见编程概念

[文档注释 ](https://kaisery.github.io/trpl-zh-cn/ch03-04-comments.html) 

## 变量与可变性

默认情况下，变量是不可变的

- 常量永远不可变，不能使用mut
- 声明常量用const，类型必须被标注
- 常量可在任何作用域进行声明，包括全局作用域
- 常量命名：全大写，单词间用下划线隔开 `const MAX_POINTS:u32 = 100_000;`

**Shadowing(隐藏)**

可以==用相同的名字声明新的变量==，新变量会`shadow`之前声明的同名变量； 

后声明的变量，会隐藏前面声明的变量

- 后续代码中，变量名代表的是新的变量
- 使用let声明的同名新变量，类型可以与之前的不同

## 数据类型

2种：标量、复合类型

- 标量类型：代表一个==单个的值==
  - 整数型 : 有符号 `i32`   无符号 `u32`，占32位空间
    - arch： isize、usize ==位数由==程序运行的计算机==架构==决定，64位计算机，就是64位
    - 整数字面量： 所有数值字面量都允许使用类型后缀； `57u8` u8就是57的类型
  - 浮点数 : `f32`  32位浮点数， f64
  - 布尔： 占1个字节
  - 字符类型： char类型，描述单个字符，==占4字节==
    - 字符类型的字面量使用单引号
- 复合类型： 将==多个值放在一个类型里==
  - 元组：Tuple，`多个类型`多个值，放在一个类型里； 元组长度固定
    - 小括号，值逗号分开    `let tup:(i32,f64,u8) = (500,6.4,1)`
    - 获取元素值： 可以使用==模式匹配==解构Tuple，来获取元素值
    - 访问元素： 在tuple变量使用点标记法，后接元素索引号
  - 数组: 多个值，放在一个类型里,元素的`类型必须相同`； 数组长度固定
    - 中括号，逗号隔开
    - 用处： 让数据存放在栈上，而不是堆上，或者想保证有固定数量的元素； 数组没有==Vector==灵活
    - Vector由标准库提供，长度可以改变；  数组由 `prelude`模块提供
    - 数组类型： `[类型;长度] 例： let a:[i32;5] = [1,2,3,4,5];`  
    - 访问元素：数组是栈上分配的单个块的内存   `let first = arr[0];`

```rust
let tup:(i32,f64,u8) = (500,6.4,1);

// 使用模式匹配解构Tuple，来获取元素值
let(x,y,z)=tup;
println!("{},{},{},", x, y,z)

// 访问tuple元素: 使用点标记法，后接元素索引号
println!("{},{},{},", tup.0, tup.1,tup.2)

//声明数组
let  a:[i32;5] = [1,2,3,4,5];
// 如果元素值相同，可以指定初始值 + ； + 数组长度   let a=[3,3,3,3,3];
let a=[3;5];  
```



- 切片： Slice； 对数据值的部分引用   `&str`  
- 取地址符号： `&`  取变量地址，取引用地址       [rust取地址](https://www.baidu.com/s?ie=UTF-8&wd=rust%E5%8F%96%E5%9C%B0%E5%9D%80) 
- 集合与字符串

## 函数

rust使用 `snake case` 命名规范 : 字母小写，单词之间下划线分开

形参叫 `parameters`， 实参叫 `arguments`；

函数签名里，必须声明每个参数类型，参数用逗号分开

[rust语句和表达式_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=rust%E8%AF%AD%E5%8F%A5%E5%92%8C%E8%A1%A8%E8%BE%BE%E5%BC%8F)     [rust语句和表达式_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=rust%E8%AF%AD%E5%8F%A5%E5%92%8C%E8%A1%A8%E8%BE%BE%E5%BC%8F)   [Rust的语句与表达式 ](https://www.cnblogs.com/Davirain/p/13097120.html)  [语句和表达式](https://zhuanlan.zhihu.com/p/581091362) 

- 函数体中的语句与表达式  
  -  Rust 是一门基于表达式（expression-based）的语言
  - **语句**（*Statements*）是执行一些操作但不返回值的指令。 **表达式**（*Expressions*）计算并产生一个值； 
    - ==表达式的结尾没有分号==， 加上分号，它就变成了语句，而语句不会返回值。
    - 语句不返回值。因此，不能把 `let` 语句赋值给另一个变量， `let x = (let y = 6);` 错误
    - 表达式可以是语句的一部分,反过来,语句也可以是表达式的一 部分

```ruby
fn <函数名> ( <参数> ) { 函数体 }

// 参数声明之后用 -> 来声明函数返回值的类型
fn add(a: i32, b: i32) -> i32 {
    return a + b;
}
```



| ![](./Rust.assets/Snipaste_2024-07-22_20-37-55.jpg) | ![]() |
| --------------------------------------------------- | ----- |

[点 . 单冒号 : 双冒号::](https://zhuanlan.zhihu.com/p/636118997)    

[Turbofish之函数后面双冒号(::)用法](https://blog.csdn.net/hbuxiaofei/article/details/110855673)   [turbo.fish](https://blog.csdn.net/gitblog_00017/article/details/139037695)   [Rust Turbofish 的由来](https://blog.csdn.net/aggresss/article/details/138357709)   

- 双冒号： 函数引用的标志，代码`String::from("hello");`即： ==引用String类型下的from函数==，这个函数通常用来构建一个字符串对象  `:: 表示 from 是string 类型下的函数； 或from 是string命名空间下的函数`
  - 用于访问命名空间中的项，例如模块、枚举、常量、函数等
  - 还可以用于表示关联类型
- 单冒号： 用于==类型注解==或表示==函数返回类型== `:` 
- 点： 用于==访问==结构体、枚举、实例的==成员或方法== `.` 

```rust
//	..y  等价于   0..y
//	x..  等价于   x 到数据结束
//	.. 	 等价于   0 到结束
```



**闭包**

## ==控制流==

### 条件

```rust
// 1、if
fn main() {
    let number = 3; 
    if number < 5 { 
        println!("条件为 true"); 
    } else { 
        println!("条件为 false"); 
    } 
}
```

**使用else if处理多重条件**

如果使用了多于一个else if，最好使用 `match ` 重构代码

match： 根据不同的匹配模式执行不同的代码 

```rust
match guess.cmp(&secret_number) {
    Ordering::Less => println!("Too small!"),
    Ordering::Greater => println!("Too big!"),
    Ordering::Equal => {
        println!("You win!");
        break;
    }
}
```

因为 `if` 是一个表达式，可以放在let语句中等号右边   `let number = if a > 0 { 1 } else { -1 };`

### 循环

```rust
// 1、 for...in
fn main() { 
    let a = [10, 20, 30, 40, 50]; 
    for i in a.iter() { 
        println!("值为 : {}", i); 
    } 
}

// 2、 while: 每次执行循环体之前判断一次条件
let mut i = 0; 
while i < 10 { 
    i += 1; 
}

// 3、 loop 无限循环
fn main() { 
    let s = ['R', 'U', 'N', 'O', 'O', 'B']; 
    let mut i = 0; 
    loop { 
        let ch = s[i]; 
        if ch == 'O' { 
            break; 
        } 
        println!("\'{}\'", ch);
        i += 1; 
    } 
}
```

**Range**

标准库提供，指定一个开始和结束数字，生成它们之间的数字(不含结束数字)； `rev` 反转 Range

`for num in (1..4).rev() { }`

# 4、所有权

rust最独特的特性，让rust无需 GC（垃圾回收器）就可以保证内存安全

程序必须在运行时==管理==它们所使用的==内存资源==；  大多数的编程语言都有管理内存的功能

- C/C++ 主要通过手动方式管理内存，开发者需要==手动的申请和释放==内存资源
- Java 程序在虚拟机（JVM）中运行，JVM 具备自动回收内存资源的功能
  - 会降低运行时效率，所以 JVM 会尽可能少的回收资源，这样也会使程序占用较大的内存资源
- 所有权： Rust为高效使用内存而设计的语法机制
  - 让 Rust ==在编译阶段==更有效地==分析内存资源的有用性==以实现内存管理

## stack和heap

- ==存储数据==：heap会返回一个指针，即这个空间的地址（找足够大的空间、并作记录）；  stack不需要分配，挨着放就可以了； 数据压到stack不需要寻找存储空间，那个位置永远在stack顶端
- ==访问数据==：heap中访问数据，要通过指针跳转，属于间接访问； 而stack

| ![](./Rust.assets/Snipaste_2024-07-23_10-38-02.jpg) | ![](./Rust.assets/Snipaste_2024-07-23_10-38-57.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-23_10-43-04.jpg) | ![](./Rust.assets/Snipaste_2024-07-23_10-44-13.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-23_10-52-58.jpg) | ![](./Rust.assets/Snipaste_2024-07-23_10-54-53.jpg) |

## 所有权解决的问题

- 跟踪代码中分配的heap空间
- 最小化heap上的重复数据
- 清理heap上未使用的数据

==管理heap数据==是所有权存在的原因

| ![](./Rust.assets/Snipaste_2024-07-23_10-57-42.jpg) | ![变量作用域](./Rust.assets/Snipaste_2024-07-23_11-03-36.jpg) |
| --------------------------------------------------- | ------------------------------------------------------------ |

## 所有权规则 

所有权有三条规则

- Rust 中的每个值都有一个变量，这个变量是该值的所有者。
- 每个值同时只能有一个所有者。
- 当所有者超出作用域时，该值将被删除。

**变量作用域**

string类型的值存储在heap； 可以使用 `from` 函数从字符串字面值创建出 `String` 类型

```rust
// :: 表示 from 是string 类型下的函数； 或from 是string命名空间下的函数
let s = String::from("hello");
```

为什么string类型的值可以修改，而字符串字面量值却不能修改？

- 当变量超出作用域时，rust自动调用drop函数

变量与数据交互的方式

- 移动：简单值压入栈
  - String类型：3部分入栈， 字符串内容的部分，存在heap上
  - 当s1赋给s2，string数据被复制一份（指针、长度、容量）； heap数据没有复制； 当s1、s2离开作用域时，会引起二次释放
  - s1赋给s2， s1就应该失效； s1被移动到s2了
- 克隆
  - 对heap上的String数据进行深度拷贝，而不是仅仅拷贝stack上的数据， 可用clone方法

```rust
// 克隆
fn main() {
    let  s1 = String::from("Hello");
    let s2 = s1.clone();
    println!("{},{}",s1,s2);
}
```



| ![](./Rust.assets/Snipaste_2024-07-23_18-00-35.jpg) | ![](./Rust.assets/Snipaste_2024-07-23_18-01-40.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-23_18-04-18.jpg) | ![](./Rust.assets/Snipaste_2024-07-23_18-05-55.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-23_18-06-49.jpg) | ![](./Rust.assets/Snipaste_2024-07-23_18-08-55.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-23_18-10-43.jpg) | ![](./Rust.assets/Snipaste_2024-07-23_18-12-46.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-23_18-14-14.jpg) | ![](./Rust.assets/Snipaste_2024-07-23_18-15-19.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-23_18-17-15.jpg) | ![](./Rust.assets/Snipaste_2024-07-23_18-18-05.jpg) |



```rust
fn main() {
    // 简单数
    let x = 5;
    let y = x;

    // String版本 (移动)
    let a1 = String::from("hello");
    let a2 = a1;
    println!("{}", a2);

    // 深拷贝 heap-copy
    let s1 = String::from("Hello");
    let s2 = s1.clone();
    println!("{},{}", s1, s2);

    // stack上的数据，不需要克隆，复制就行
    let b1 = 5;
    let b2 = b1;
    println!("{},{}",b1,b2);
}
```



## 所有权与函数

**难懂**

- ==值传递给函数==也会发生移动或复制
- 函数在返回值过程中，也会发生所有权转移
  - 返回值移动到调用它的函数中
  - 例：调用takes..back函数时，把s2传递进去，然后返回值绑定到s3变量
  - 如何让函数使用某个值，但不获取其所有权？  作为参数传进去，又作为结果返回，这样太笨了，rust用 `引用` 解决

| ![](./Rust.assets/Snipaste_2024-07-24_00-32-08.jpg)       | ![](./Rust.assets/Snipaste_2024-07-24_00-34-43.jpg)          |
| --------------------------------------------------------- | ------------------------------------------------------------ |
| ![返回值](./Rust.assets/Snipaste_2024-07-24_17-30-29.jpg) | ![作为参数传进去，又作为结果返回](./Rust.assets/Snipaste_2024-07-24_17-37-33.jpg) |

## 引用和借用

[rust解引用是星号*](https://www.baidu.com/s?ie=UTF-8&wd=rust%E8%A7%A3%E5%BC%95%E7%94%A8)

**难懂** 

没有转移s1所有权，而是把==s1的引用== (&s1)作为参数传给函数; 引用走出作用域时，s1就不会drop被清理掉

- s是一个指针，指向s1，s1也是指针，指向heap上的内容

| ![](./Rust.assets/Snipaste_2024-07-24_18-05-26.jpg) | ![](./Rust.assets/Snipaste_2024-07-24_18-10-47.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-24_18-16-19.jpg) | ![](./Rust.assets/Snipaste_2024-07-24_18-18-08.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-24_18-19-50.jpg) | ![](./Rust.assets/Snipaste_2024-07-24_18-22-05.jpg) |



```rust
fn main() {
    let mut s1 = String::from("hello");
    let len = calculate_length(&mut s1);

    println!("The length of '{}' is {}.", s1, len);
}

fn calculate_length(s: &mut String) -> usize {
    s.push_str(",world");
    s.len()
}
```



## slice切片

rust提供不支持所有权的数据类型：切片

- 指向字符串中一部分内容的引用
- 字符串切片类型 ： `&str`
- 其它类型的切片

```rust
let s = String::from("Hello world");
let hello = &s[0..5];
// 3个语法糖
let h = &s[..5];
let e = &s[6..];
let o = &s[..];
```



# 5、结构体组织关联的数据

- 自定义的数据类型
- ==为相关联的值命名，并打包组成有意义的组合==
- ==定义struct==
  - 使用struct关键字，并为整个struct命名
  - 在花括号内，为所有字段定义名称和类型
- ==实例化struct==
  - 要使用struct，需要创建struct实例
    - 为字段指定具体值，无需按声明顺序进行指定 



结构体（Struct）与元组（Tuple）都可以将若干个类型不一定相同的数据捆绑在一起形成整体

- 结构体的每个成员和其本身都有一个名字，这样访问它成员的时候就不用记住下标了
- 元组常用于非定义的多值传递，  而结构体用于规范常用的数据结构。结构体的成员叫做"字段"

```rust
struct Site {
    domain: String,
    name: String,
    found: u32
}
//实例化struct
fn main(){
    println!("Hello, world!");
    let mut st = Site{
        name: String::from("wang"),
        domain: String::from("www.163.com"),
        found: 33,        
    };
}
// 取得struct里面的值: 使用点标记法
st.name = String::from("zhang");	//赋新值
// struct作为函数返回值
fn build(email:String,name:String) -> User{
    User{
        email:email,	// 值对应参数里面的变量
        name:name,
        active:true,
    }
}
// 字段初始化简写：当字段名与字段值对应的变量名相同时，可以使用字段初始化简写
fn build(email:String,name:String) -> User{
    User{
        email,	// 值对应参数里面的变量
        name,
        active:true,
    }
}

// struct更新语法：基于某个struct实例创建一个新实例，可使用更新语法  ..user1

```

**元组结构体**

更简单的定义和使用结构体的方式：**元组结构体**；   与元组的区别是有名字和固定的类型格式

- Tuple struct整体有名，但里面元素没有名
- struct关键字 + 名字 + 里面元素类型
- 可以使用模式匹配解构

| ![](./Rust.assets/Snipaste_2024-07-26_13-00-38.jpg) | ![](./Rust.assets/Snipaste_2024-07-26_13-04-24.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-26_13-06-50.jpg) | ![](./Rust.assets/Snipaste_2024-07-26_13-07-52.jpg) |

**空结构体**

没有任何字段； trait可以当作接口

- `impl Rectangle{ }`
- 关联函数
  - impl块里，不但能定义方法，还能定义函数，它不把self作为第一个参数，叫关联函数
  - 关联函数通常用于构造器：创建被关联类型的一个实例

**struct的方法**

| ![](./Rust.assets/Snipaste_2024-07-26_14-54-56.jpg) | ![](./Rust.assets/Snipaste_2024-07-26_14-58-05.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-26_14-59-28.jpg) | ![](./Rust.assets/Snipaste_2024-07-26_15-01-43.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-26_15-07-48.jpg) | ![](./Rust.assets/Snipaste_2024-07-26_15-08-24.jpg) |



## 数据结构



# 6、枚举和模式匹配

[枚举 变体_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=%E6%9E%9A%E4%B8%BE%20%E5%8F%98%E4%BD%93) 

- 列举所有可能的值来定义一个类型
- 里面所有可能的值叫==枚举的变体==
- **定义枚举**
- **为枚举定义方法** : impl

```rust
//定义枚举
enum IpAdd {
    v4,
    v6,
}

fn main() {
    // 枚举值
    let four = IpAdd::v4;
    let six = IpAdd::v6;
    route(four);
    route(six);
    route(IpAdd::v6);
}

fn route(ip_kind: IpAdd) {}
```



| ![](./Rust.assets/Snipaste_2024-07-26_18-12-39.jpg) | ![](./Rust.assets/Snipaste_2024-07-26_18-14-53.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |

## Option枚举

- 定义与标准库中
- 在Prelude（预导入模块)中
- 描述：某个值可能存在（或是某种类型）或不存在

rust没有null

| ![](./Rust.assets/Snipaste_2024-07-26_18-20-38.jpg) | ![](./Rust.assets/Snipaste_2024-07-26_18-21-31.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |

## 模式匹配

match： 控制流运算符

- 绑定值的模式： 匹配的分支可以绑定到，被匹配对象的部分值

match： 根据不同的匹配模式执行不同的代码   [匹配模式match](https://baijiahao.baidu.com/s?id=1764111595548760280&wfr=spider&for=pc)    [Rust控制流运算符match](https://www.jb51.net/program/314385bey.htm) 

```rust
//
match value {
    pattern1 => {
    // code1
    }
    pattern2 => {
    // code2
    }
    _ => {
    // 没有任何匹配
    }
}
```

## if let

相对match，简单的控制流

- 处理只关心一种匹配而忽略其它匹配的情况



# 7、包、Crate和模块

[crates.io: Rust Package Registry](https://crates.io/) 

[ Rust中的prelude](https://zhuanlan.zhihu.com/p/611201537)  [Prelude ](https://www.kancloud.cn/zzrdark/rustprimer/1829258) [rust prelude模块](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=rust%20prelude%E6%A8%A1%E5%9D%97&oq=rust%2520%25E6%2595%25B0%25E7%25BB%2584%25E7%2594%25B1%25E5%2593%25AA%25E4%25B8%25AA%25E6%25A8%25A1%25E5%259D%2597%25E6%258F%2590%25E4%25BE%259B&rsv_pq=e4068ed20058d940&rsv_t=75dbPDk87jiI6kOYaDNb6E5zv3sIQtcuN7FJprCai3QM%2FVWWURZxgrwQElc&rqlang=cn&rsv_enter=1&rsv_dl=tb&rsv_btype=t&inputT=4764&rsv_sug3=36&rsv_sug1=25&rsv_sug7=100&rsv_sug2=0&rsv_sug4=5840)   

prelude预导入模块，是标准库的一部分

==使用包、Crate和模块管理不断增长的项目== 

Cargo 是 Rust 的官方构建系统和包管理器， 可以构建代码、下载依赖库、构建库等，主要有两个作用

- 项目管理
- 包管理器

如果创建项目没使用cargo，可把项目转化为使用cargo

- 源代码移动到src
- 创建Cargo.toml

```rust
cargo --version
cargo new hello				// 创建项目		
cd hello
code .						// vscode打开

cargo build 				// 构建cargo项目
cargo run					// 构建并运行cargo项目： 编译 + 执行;k 
cargo check					// 检查代码，比cargo build快得多，提高效率
cargo build --release		// 为发布构建

// rust里，代码的包称为crate，例如安装一个第三方库，在rust里就叫crate
// Cargo.toml在项目顶层下，源代码在src目录下
// 顶层目录可放置： README、许可信息、配置文件和其它与源码无关的文件
// cargo.lock负责追踪项目依赖的精确版本，不要手动修改该文件
```

## 组织管理

[Rust之包、单元包及模块](https://blog.csdn.net/a_qwq_a/article/details/131888761)  [Rust中箱、包和模块](https://www.jb51.net/program/317705x93.htm) 

对于一个工程来讲，组织代码是十分重要的。

Rust 中有三个重要的组织概念：箱、包、模块

- 箱： 二进制程序文件或者库文件，存在于"包"中
- 包
  - 工程的实质就是一个包，包必须由 Cargo.toml 管理，该文件描述了==包的基本信息以及依赖项==
  - `cargo new` 创建完包之后，src 目录下会生成一个 main.rs 源文件，Cargo 默认这个文件为二进制箱的根，编译之后的二进制箱将与包名相同
- 模块
  - 组织模块的主要结构往往是树。Java 组织功能模块的主要单位是类，而 JavaScript 组织模块的主要方式是 function

文件系统中，目录结构以斜杠在路径字符串中表示对象的位置，Rust 中的路径分隔符是 `::` 

```rust
// 路径分为绝对路径和相对路径。绝对路径从 crate 关键字开始描述。相对路径从 self 或 super 关键字或一个标识符开始描述
crate::nation::government::govern();
nation::government::govern();
```

**访问权限**

Rust 中有两种简单的访问权： 公共（public）和私有（private）

默认模块中的成员访问权将是私有。   公共权限，需要使用 pub 关键字。

对于私有的模块，只有在与其==平级的位置或下级的位置==才能访问，不能从其外部访问

**引入模块**

use 关键字将模块标识符==引入当前作用域==

```rust
// 有些情况存在两个相同的名称，且同样需要导入，可以使用 as 关键字为标识符添加别名
// 用 as 将 nation 下的取别名 nation_govern。两个名称可以同时使用
use crate::nation::government::govern;
use crate::nation::govern as nation_govern;

// use 关键字可以与 pub 关键字配合使用
pub use government::govern;
```

**引用标准库**

```rust
use std::f64::consts::PI;

fn main() {
    println!("{}", (PI / 2.0).sin());
}
```

## Pacakge

- 定义module： `mod 名字 { }` 

| ![](./Rust.assets/Snipaste_2024-07-26_20-06-01.jpg) | ![](./Rust.assets/Snipaste_2024-07-26_20-07-28.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-26_20-13-56.jpg) | ![](./Rust.assets/Snipaste_2024-07-26_20-16-53.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-26_20-17-35.jpg) | ![](./Rust.assets/Snipaste_2024-07-26_20-18-44.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-26_20-21-10.jpg) | ![](./Rust.assets/Snipaste_2024-07-26_20-22-20.jpg) |

## 路径

- 路径：多个标识符之间由 `::` 分隔
- super：用来访问父级模块路径中的内容，类似文件系统中的 `..`
- pub 放在 struct前：struct是公共的，但字段默认是私有的，字段需单独设置pub来变成公有
- 枚举变成公共：pub 放在 enum前，变体也都变成公共的

| ![](./Rust.assets/Snipaste_2024-07-27_10-40-15.jpg) | ![](./Rust.assets/Snipaste_2024-07-27_10-46-06.jpg)      |
| --------------------------------------------------- | -------------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-27_10-46-50.jpg) | ![super](./Rust.assets/Snipaste_2024-07-27_10-49-06.jpg) |

## use

- 使用use将路径导入到作用域内,仍遵循私有性规则
- 使用 `*` 通配符把路径中所有的公共条目引入作用域
- 将模块拆分为不同文件

| ![](./Rust.assets/Snipaste_2024-07-27_14-48-29.jpg) | ![](./Rust.assets/Snipaste_2024-07-27_14-49-30.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-27_14-52-41.jpg) | ![](./Rust.assets/Snipaste_2024-07-27_14-53-25.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-27_14-55-35.jpg) | ![](./Rust.assets/Snipaste_2024-07-27_14-57-01.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-27_15-00-38.jpg) |                                                     |



# 8、常见集合

heap上的数据，所以集合的数据大小，无需在编译时就确定，在运行时，可以动态变大或变小

## Vector

- 创建Vector： `Vec::new`
- 更新Vector： 添加元素，`push`
- 删除Vector： Vector离开作用域后，被清理掉，所有的元素也被清理
- 读取Vector元素
  - 索引
  - get方法

- 所有权和借用规则： 不能再同一作用域内同时拥有可变和不可变引用
- 遍历Vector中的值 ： `for`
- 

```rust
fn main() {
    // let v:Vec<i32> = Vec::new();
    // let mut v = Vec::new();
    // v.push(1);
    // v.push(2);
    // 通常指定初始值来创建Vec<T>, 使用vec!宏
    // let v = vec![1, 2, 3];

    // 读取Vector元素
    let mut v = vec![1, 2, 3, 4, 5];
    let third: &i32 = &v[2];
    println!("The third ele is {}", third);

    match v.get(2) {
        Some(third) => println!("The third ele is {}", third),
        None => println!("There is no third ele"),
    }
    for i in &mut v {
        *i += 50;   // 解引用
    }

    for i in &v {
        println!("{}", i);
    }
}
//cargo run
```



| ![](./Rust.assets/Snipaste_2024-07-27_15-55-34.jpg) | ![]() |
| --------------------------------------------------- | ----- |



## String

- 字符串是基于字节的集合，提供一些方法，可以将字节解析为文本
- 通常说的字符串是String和&str（字符串切片）两种类型
- String结尾的可获得所有权，Str结尾的可借用
- 创建新字符串：String是vet的集合，string是对`Vec<u8>`的包装

| ![](./Rust.assets/Snipaste_2024-07-28_10-47-08.jpg) | ![](./Rust.assets/Snipaste_2024-07-28_10-49-37.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-28_10-52-43.jpg) | ![](./Rust.assets/Snipaste_2024-07-28_10-55-23.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-28_10-57-27.jpg) | ![](./Rust.assets/Snipaste_2024-07-28_10-58-36.jpg) |



| ![](./Rust.assets/Snipaste_2024-07-28_12-44-27.jpg) | ![](./Rust.assets/Snipaste_2024-07-28_12-46-11.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-28_12-46-32.jpg) | ![](./Rust.assets/Snipaste_2024-07-28_12-47-07.jpg) |

## HashMap

- 键值对； HashMap用的少，所以不在Prelude中
- 访问HashMap中的值： `get方法`
- 遍历HashMap： `for循环`

| ![](./Rust.assets/Snipaste_2024-07-28_12-48-53.jpg) | ![](./Rust.assets/Snipaste_2024-07-28_12-50-44.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-28_12-52-04.jpg) | ![](./Rust.assets/Snipaste_2024-07-28_12-54-12.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-28_12-55-29.jpg) | ![](./Rust.assets/Snipaste_2024-07-28_12-57-48.jpg) |

- 更新HashMap
  - 大小可变：即键值对数量可变

| ![](./Rust.assets/Snipaste_2024-07-28_13-01-09.jpg) | ![](./Rust.assets/Snipaste_2024-07-28_13-02-58.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-28_13-04-00.jpg) |                                                     |



# 9、错误处理



Rust 有一套独特的处理异常情况的机制，它并不像其它语言中的 try 机制那样简单

可恢复错误用 `Result<T, E>` 类来处理，对于不可恢复错误使用 `panic!` 宏来处理 

| ![](./Rust.assets/Snipaste_2024-07-28_15-04-11.jpg) | ![](./Rust.assets/Snipaste_2024-07-28_15-08-53.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-28_15-10-12.jpg) | ![](./Rust.assets/Snipaste_2024-07-28_18-41-57.jpg) |

## Result枚举与可恢复的错误

| ![](./Rust.assets/Snipaste_2024-07-28_23-08-37.jpg) | ![](./Rust.assets/Snipaste_2024-07-28_23-09-31.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-28_23-11-10.jpg) | ![](./Rust.assets/Snipaste_2024-07-28_23-12-08.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-28_23-12-41.jpg) | ![](./Rust.assets/Snipaste_2024-07-28_23-14-26.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-28_23-15-10.jpg) | ![](./Rust.assets/Snipaste_2024-07-28_23-17-13.jpg) |

## 何时使用panic!

| ![](./Rust.assets/Snipaste_2024-07-28_23-20-59.jpg) | ![](./Rust.assets/Snipaste_2024-07-28_23-22-04.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |



# 10、泛型与特性、Trait和生命周期

C++ 中用"模板"来实现泛型，而 C 语言中没有泛型的机制，这也导致 C 语言难以构建类型复杂的工程

特性（trait）概念接近于 Java 中的接口（Interface），但两者不完全相同。特性与接口相同的地方在于它们都是一种行为规范，可以用于标识哪些类有哪些方法。

**提取函数以消除重复代码**

| ![](./Rust.assets/Snipaste_2024-07-28_23-27-52.jpg) | ![](./Rust.assets/Snipaste_2024-07-28_23-28-34.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |

## 泛型

- 函数定义中使用泛型
- struct定义中使用泛型
- 枚举定义中使用泛型
- 方法定义中使用泛型

| ![](./Rust.assets/Snipaste_2024-07-28_23-53-02.jpg) | ![](./Rust.assets/Snipaste_2024-07-28_23-56-46.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-28_23-58-11.jpg) | ![](./Rust.assets/Snipaste_2024-07-28_23-59-06.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-29_00-00-33.jpg) | ![](./Rust.assets/Snipaste_2024-07-29_00-01-17.jpg) |

## Trait

- 其它语言的接口
- `Trait bounds` : 要求泛型实现某些trait
- 定义trait
  - 类型的行为，由该类型所调用的方法组成，有时不同的类型有相同的方法

- trait作为参数

| ![](./Rust.assets/Snipaste_2024-07-29_06-54-16.jpg) | ![](./Rust.assets/Snipaste_2024-07-29_06-58-52.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-29_07-01-06.jpg) | ![](./Rust.assets/Snipaste_2024-07-29_07-06-02.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-29_07-08-58.jpg) | ![](./Rust.assets/Snipaste_2024-07-29_09-03-28.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-29_09-04-38.jpg) | ![](./Rust.assets/Snipaste_2024-07-29_09-06-53.jpg) |
## 生命周期

- 生命周期： 让引用保持有效的作用域
  - 存在的意义：避免悬垂引用（dangling reference）
- 借用检查器： 比较作用域，从而判断所有的借用是否合法
- 函数中的泛型生命周期
- 生命周期标注语法

| ![](./Rust.assets/Snipaste_2024-07-29_09-08-46.jpg) | ![](./Rust.assets/Snipaste_2024-07-29_09-18-20.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-29_10-01-04.jpg) | ![](./Rust.assets/Snipaste_2024-07-29_10-01-51.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-29_10-03-16.jpg) | ![](./Rust.assets/Snipaste_2024-07-29_10-48-53.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-29_10-50-02.jpg) | ![](./Rust.assets/Snipaste_2024-07-29_10-51-29.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-29_10-51-50.jpg) | ![](./Rust.assets/Snipaste_2024-07-29_10-52-25.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-29_10-53-08.jpg) | ![](./Rust.assets/Snipaste_2024-07-29_10-54-27.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-29_10-55-14.jpg) |                                                     |
# 11、编写自动化测试

- rust中，测试就是函数
- 测试函数： `cargo test`运行测试函数
- `assert!`宏检查测试结果
- 自定义错误消息
- `should_panic` 检查是否发生恐慌 

| ![](./Rust.assets/Snipaste_2024-07-29_10-58-17.jpg) | ![](./Rust.assets/Snipaste_2024-07-29_11-00-01.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-29_11-01-18.jpg) | ![](./Rust.assets/Snipaste_2024-07-29_13-24-16.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-30_08-20-39.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_08-22-07.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-30_08-23-27.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_08-25-03.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-30_08-26-07.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_08-27-00.jpg) |

- 控制测试如何运行

| ![](./Rust.assets/Snipaste_2024-07-30_08-29-00.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_08-29-54.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-30_08-30-31.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_08-30-54.jpg) |

- 按名称运行测试
- 忽略某些测试： 太耗时

| ![](./Rust.assets/Snipaste_2024-07-30_08-33-18.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_08-34-15.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |

- 测试分类
  - 单元测试
    - 将小段代码单独隔离出来，从而确定这段代码是否符合预期
    - 通常将单元测试和被测试代码放在src目录下，同一文件中； 
    - 代码建立test模块来放测试函数，并用 `#[cfg(test)]`标注测试模块
  - 集成测试
    - 验证被测试库的多个部分，在一起是否能正确工作

| ![](./Rust.assets/Snipaste_2024-07-30_08-36-55.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_08-42-39.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-30_11-20-34.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_11-23-00.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-30_11-23-28.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_11-25-36.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-30_11-26-41.jpg) |                                                     |

# 12、项目实例

**命令行程序**

| ![](./Rust.assets/Snipaste_2024-07-30_11-29-25.jpg) | ![]() |
| --------------------------------------------------- | ----- |
| ![]()                                               | ![]() |

## 测试驱动开发

[TDD（测试驱动）调研](https://blog.csdn.net/mlongquan/article/details/136377378)    [测试驱动开发（开发方法）_百度百科](https://baike.baidu.com/item/%E6%B5%8B%E8%AF%95%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91/3328831?fr=ge_ala) 

| ![](./Rust.assets/Snipaste_2024-07-30_12-02-48.jpg) | ![]() |
| --------------------------------------------------- | ----- |

# 13、函数式编程

## 闭包

函数作为参数，或返回值; 或把函数赋值给变量

- 闭包类型推断和标注
- 使用泛型参数和 `FnTrait` 存储闭包
- 使用闭包捕获环境

| ![](./Rust.assets/Snipaste_2024-07-30_13-42-22.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_13-45-53.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![]()                                               | ![]()                                               |

## 迭代器

- `Iterator trait`  和 `next` 方法
- 消耗和产生迭代器的方法

| ![](./Rust.assets/Snipaste_2024-07-30_13-49-37.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_13-52-05.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-30_13-52-43.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_13-53-37.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-30_13-58-58.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_13-59-34.jpg) |

- 使用闭包捕获环境，配合迭代器使用
- 创建自定义迭代器： 要提供一个 `next` 方法的实现
- 比较 循环 和 迭代器 的性能

| ![](./Rust.assets/Snipaste_2024-07-30_14-01-50.jpg) | ![]() |
| --------------------------------------------------- | ----- |
| ![]()                                               | ![]() |

# 14、 cargo，crates.io

- release profile : 发布的配置

| ![](./Rust.assets/Snipaste_2024-07-30_14-34-18.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_14-36-11.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-30_14-37-05.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_14-40-10.jpg) |

发布crate 到 crates.io

| ![](./Rust.assets/Snipaste_2024-07-30_14-40-36.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_14-41-47.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-30_14-42-21.jpg) | ![]()                                               |

- pub use
- 

| ![](./Rust.assets/Snipaste_2024-07-30_14-46-07.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_14-47-18.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-30_14-48-02.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_14-49-14.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-30_14-49-47.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_14-50-47.jpg) |

- Cargo 工作空间
- 从`Crates.io` 安装二进制 crate

| ![](./Rust.assets/Snipaste_2024-07-30_14-52-15.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_14-53-25.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-30_14-54-45.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_14-55-20.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-30_14-56-19.jpg) |                                                     |

# 15、智能指针

提供了额外的功能和安全性保证，以帮助管理内存和数据

智能指针是一种封装了==对动态分配内存的所有权==和==生命周期管理==的数据类型 

标准库提供了几种常见的智能指针类型，例如 Box、Rc、Arc 和 RefCell

- 智能指针： ==有额外的元数据和功能==  
  - 引用只是借用数据
  - 智能指针：很多时候拥有它所指向的数据

| ![](./Rust.assets/Snipaste_2024-07-30_17-00-38.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_17-01-06.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-30_17-01-48.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_17-02-15.jpg) |
| ![](./Rust.assets/Snipaste_2024-07-30_21-24-48.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_21-25-21.jpg) |

- 使用 `Box<T>` 指向堆内存上的数据

| ![](./Rust.assets/Snipaste_2024-07-30_21-26-16.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_21-36-31.jpg) |
| --------------------------------------------------- | --------------------------------------------------- |
| ![](./Rust.assets/Snipaste_2024-07-30_21-37-22.jpg) | ![](./Rust.assets/Snipaste_2024-07-30_21-39-39.jpg) |

Deref Trait

| ![](./Rust.assets/Snipaste_2024-07-30_21-42-50.jpg) | ![]() |
| --------------------------------------------------- | ----- |
| ![]()                                               | ![]() |

Drop Trait

| ![](./Rust.assets/Snipaste_2024-07-30_21-45-07.jpg) | ![]() |
| --------------------------------------------------- | ----- |
| ![]()                                               | ![]() |

`Rc<T>` 引用计数智能指针

| ![]() | ![]() |
| ----- | ----- |
| ![]() | ![]() |

`RefCell<T>` 和内部可变性

| ![]() | ![]() |
| ----- | ----- |
| ![]() | ![]() |

循环引用可导致内存泄漏

# 16、无畏并发

- Concurrent： 并发
- Parallel： 并行
- 使用消息传递来跨线程传递数据
- 共享状态的并发
- 通过send和sync Trait 来扩展并发

| ![](./Rust.assets/Snipaste_2024-07-30_22-10-07.jpg) | ![]() |
| --------------------------------------------------- | ----- |
| ![]()                                               | ![]() |



# 17、面向对象编程

面向对象的编程语言通常实现了数据的封装与继承并能基于数据调用方法。

Rust 不是面向对象的编程语言，但这些功能都得以实现。

## 封装

## 继承

# 宏

[好：声明宏](https://cloud.tencent.com/developer/article/2338834)  [好：过程宏](https://cloud.tencent.com/developer/article/2338833)   [rust宏并不类似注解_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=rust%E5%AE%8F%E7%B1%BB%E4%BC%BC%E6%B3%A8%E8%A7%A3)  [Rust宏](https://cloud.tencent.com/developer/article/2338833) 

[宏 rust](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=%E5%AE%8F%20rust&oq=%25E5%25AE%258F&rsv_pq=9c4e5b8d00279515&rsv_t=7baeLbjaK8GSFzRgbikPB%2FvWnN3Tr5n0DqdQMQuUYTJyMKQGSqwab27xjNc&rqlang=cn&rsv_enter=1&rsv_dl=tb&rsv_sug3=7&rsv_sug1=5&rsv_sug7=100&rsv_sug2=0&rsv_btype=t&inputT=1951&rsv_sug4=11422)  [rust宏编程](https://zhuanlan.zhihu.com/p/694127734)  [声明宏](https://www.jb51.net/program/31897723y.htm)  [宏](https://xie.infoq.cn/article/a144762979b4af964359965b4) 

> 注解（‌Annotation）‌通常指的是在源代码中添加的一些元数据，‌用于提供额外的信息给编译器或其他工具，‌但不直接影响程序的执行逻辑。‌注解通常不会改变代码的结构或行为，‌而是为编译器或分析工具提供额外的上下文信息
>
> 
>
> 虽然Rust宏和注解都是源代码处理的一种形式，‌但它们的目的和使用方式有本质的区别。‌Rust宏更侧重于在编译时改变代码的结构和行为，‌而注解主要是为了提供额外的信息给工具使用，‌不直接影响程序的运行

宏是Rust中的一种特殊函数，它可以==接受代码片段作为输入==，并根据需要生成代码片段作为输出

用来在编译时生成代码，  允许==在编写代码时==创建自定义语法扩展

- 宏（Macro）是一种在代码中进行元编程（Metaprogramming）的技术
- **‌[Rust宏](https://www.baidu.com/s?word=Rust宏&sa=re_dqa_zy)是一种编译器扩展，用于在编译时生成代码**  
- 它允许在编译时生成代码，宏可以帮助简化代码，提高代码的可读性和可维护性，同时允许开发者在编译时执行一些代码生成的操作。

宏在 Rust 中有两种类型：==声明式宏==（Declarative Macros）和==过程宏==（Procedural Macros） 



**元编程工具，它允许程序员在编译时生成或修改代码**, 分两种类型

- **声明宏**，也称为`macro_rules!`宏，是Rust中最基本的宏形式
  - 使用`macro_rules!`关键字定义，==基于模式匹配==进行文本替换
  - 声明宏在编译期展开，用匹配的代码片段替换宏调用处的代码
- **过程宏**，更高级的宏形式，它通过编写Rust代码来处理输入的代码，并在编译期间生成新的代码；  过程宏又分为派生宏，类属性宏，类函数宏
  - ==属性宏==： 附加到函数、结构体、枚举等声明之前，并在编译期间对其进行处理
    - `#[derive]`，可以为目标结构体或枚举派生指定的代码，例如 Debug 特征
      - 为结构体和枚举实现一些通用的trait
    - 自定义属性宏， ==类属性宏==用于为目标添加自定义的属性
  - ==类函数宏==： 看上去就像是函数调用， 可以像函数一样接受参数并返回代码片段
  - ==派生宏：==  特殊的函数宏,  用于自动实现Rust trait或其他通用功能
    - `#[derive]`
    - 自定义派生宏

Rust中的宏概念与‌[C语言](https://www.baidu.com/s?wd=C语言&usm=1&ie=utf-8&rsv_pq=9c79684300d35d3d&oq=宏 rust&rsv_t=8662gBQiMAdbtf2cWDEmzitPx8rtKIrfTnpnvE0U6bSG6wVNadRo4DEzB8k&sa=re_dqa_zy)中的宏类似，都是面向编译器制定的一种源代码扩展、替换的方法和规则

## 声明式宏

[声明宏](https://cloud.tencent.com/developer/article/2338834)    

声明宏使用`macro_rules!`关键字定义，基于==模式匹配的文本==替换宏，类似于C语言中的宏定义，在编译期展开，==用匹配的代码片段==替换宏调用处的代码。

- 声明宏的基本语法包括： 声明宏的`名称定义`、`模式匹配`部分和`声明宏返回`的部分 

```rust
// 使用 macro_rules!  定义声明式宏
macro_rules! my_macro {
    // 模式匹配和展开
    ($arg:expr) => {
        // 生成的代码
        // 使用 $arg 来代替匹配到的表达式
    };
}


// 宏规则是一系列模式匹配和替换的规则，用于匹配输入的代码片段并生成相应的代码片段
macro_rules! macro_name {
    // 宏规则
    // ...
}
```

## 过程宏

[rust宏_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=rust%E5%AE%8F)   [Rust中的过程宏](https://cloud.tencent.com/developer/article/2031390)

过程宏则更为高级，通过编写Rust代码来处理输入的代码，并在编译期间生成新的代码，主要用于属性宏、类函数宏和派生宏等场景。

更为灵活和强大的宏，允许在编译时通过自定义代码生成过程来操作抽象语法树（AST）。过程宏在功能上更接近于函数，但是它们在编写和使用上更加复杂。

- **派生宏（Derive Macros）**：用于自动实现trait（比如`Copy`、`Debug`）的宏。
- **属性宏（Attribute Macros）**：用于在声明上附加额外的元数据，如`#[derive(Debug)]`。

过程宏的实现通常需要使用 proc_macro 库提供的功能，例如 TokenStream 和 TokenTree，以便更直接地操纵源代码。



过程宏通过编写Rust代码来处理输入的代码，并在编译期间生成新的代码，例如`#[derive(Serialize, Deserialize)]`就是基于过程宏实现的。过程宏的使用更加灵活，但也需要对Rust编译器的工作原理有更深入的理解

# 其它

[renpy引擎_百度搜索](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=renpy%E5%BC%95%E6%93%8E&oq=renpy%25E6%25B8%25B8%25E6%2588%258F&rsv_pq=9081cebd02a984df&rsv_t=1897pPaQ8NZB64LFQUBdBl%2BxaBXDDRHM8RhfKFlisaEuQ23NGsjszQ03Bbg&rqlang=cn&rsv_enter=1&rsv_dl=tb&rsv_btype=t&inputT=1731&rsv_sug3=28&rsv_sug1=11&rsv_sug7=100&rsv_sug2=0&rsv_sug4=4107)   [工程部署（二）：PicoDet网络结构在YOLOv5-Lite上的复现](https://zhuanlan.zhihu.com/p/446787775)

[microsoft/monaco-editor: A browser based code editor](https://github.com/microsoft/monaco-editor?tab=readme-ov-file)  [ Monaco Editor微软开源的基于 VS Code 的代码编辑器](https://gitee.com/mirrors/monaco-editor/)   [Monaco Editor](https://blog.csdn.net/weixin_45855469/article/details/136456755)   [Monaco Editor](https://microsoft.github.io/monaco-editor/)

## 软件开发方法 

[5种常见软件开发方法](https://blog.csdn.net/weixin_62182040/article/details/138219631)   [四大软件开发方法](https://blog.csdn.net/qq_29607687/article/details/137122955)  [软件开发方法_百度百科](https://baike.baidu.com/item/%E8%BD%AF%E4%BB%B6%E5%BC%80%E5%8F%91%E6%96%B9%E6%B3%95/971447?fr=ge_ala)  

[测试驱动开发（开发方法）_百度百科](https://baike.baidu.com/item/%E6%B5%8B%E8%AF%95%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91/3328831?fr=ge_ala) 

## 软件设计原则

[DRY(Dont Repeat Yourself)和KISS( Keep It Simple, Stupid)](https://cloud.tencent.com/developer/article/1160415)    [DRY，KISS, YAGNI-轻量化设计原则](https://www.51cto.com/article/743568.html) 

[设计原则](https://blog.csdn.net/erge353729094/article/details/107552308) 

简单、不要过度设计、减少重复

## DSL领域特定语言

[好： DSL](https://cloud.tencent.com/developer/article/2405677)   [DSL](https://zhuanlan.zhihu.com/p/551787676)  [DSL 解析器_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=DSL%20%E8%A7%A3%E6%9E%90%E5%99%A8)      

[BNF_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=BNF)  [BNF范式（巴科斯范式） - 知乎](https://zhuanlan.zhihu.com/p/627568812) 