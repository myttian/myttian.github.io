# 编程的基本框架

视频： [通俗讲解编程的基本框架](https://www.bilibili.com/video/BV1FP4y1K7W5/?vd_source=7346303e5e18677d7261c2c0c109ecfd)	[代码是如何驱动硬件的？](https://www.bilibili.com/video/BV1b64y167kE/?vd_source=7346303e5e18677d7261c2c0c109ecfd)	 [机电编程原理](https://search.bilibili.com/all?vt=20236630&keyword=%E6%9C%BA%E7%94%B5%E7%BC%96%E7%A8%8B%E5%8E%9F%E7%90%86)	

[从底层汇编看显卡工作原理及编程方式](https://www.bilibili.com/video/BV1V34y1o7aj/?vd_source=7346303e5e18677d7261c2c0c109ecfd)	 [C语言怎么控制电路？单片机开发全过程](https://www.bilibili.com/video/BV1x441197Ye/?vd_source=7346303e5e18677d7261c2c0c109ecfd)	

# c语言开发演化

[c语言开发演化_百度搜索](https://www.baidu.com/s?wd=c%E8%AF%AD%E8%A8%80%E5%BC%80%E5%8F%91%E6%BC%94%E5%8C%96&rsv_spt=1&rsv_iqid=0x95a241ed001565f4&issp=1&f=3&rsv_bp=1&rsv_idx=2&ie=utf-8&tn=baiduhome_pg&rsv_enter=1&rsv_dl=ts_0&rsv_sug3=8&rsv_sug1=4&rsv_sug7=100&rsv_sug2=0&rsv_btype=i&prefixsug=c%25E8%25AF%25AD%25E8%25A8%2580&rsp=0&inputT=4379&rsv_sug4=5374&rsv_sug=1)	   [计算机编程语言的演变：从 C 语言到现代 Python 的发展历程与影响](https://baijiahao.baidu.com/s?id=1817012263420758977&wfr=spider&for=pc)	[C语言起源、特性和发展历程](https://baijiahao.baidu.com/s?id=1764426766975489445&wfr=spider&for=pc)	

[C语言的前世今生](https://zhuanlan.zhihu.com/p/687410274)	   [C语言家族：C、C++、C#](https://mbd.baidu.com/newspage/data/dtlandingsuper?nid=dt_4215324717571435680&sourceFrom=search_a)	 

[C语言历史与演化—C89、C99、C11、C17、C2x](https://www.jb51.net/program/330768ahq.htm) 	

COM编程： 组件对象模型，`Component Object Model`   [COM编程_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=COM%E7%BC%96%E7%A8%8B)	   [什么是COM编程](https://search.bilibili.com/all?vt=20146048&keyword=%E4%BB%80%E4%B9%88%E6%98%AFCOM%E7%BC%96%E7%A8%8B&search_source=5) 	 [com编程_百度百科](https://baike.baidu.com/item/com%E7%BC%96%E7%A8%8B/833430)	[com编程被什么取代了](https://worktile.com/kb/ask/2188292.html)  	[com编程是什么](https://worktile.com/kb/p/1507082)	 

## c c++ c#区别

[c c++ c#区别_百度搜索](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=c%20c%2B%2B%20c%23%E5%8C%BA%E5%88%AB&oq=c%2520c%252B%252B%2520c%2523&rsv_pq=95d666380008d158&rsv_t=25eazhLboh2ODBW6B%2FWxmjXDfXQFPyXQNKS8r1j0%2Bhf025lywm91JZcxqM4&rqlang=cn&rsv_dl=tb&rsv_sug3=5&rsv_sug1=3&rsv_sug7=100&rsv_btype=t&prefixsug=c%2520c%252B%252B%2520c%2523%25E5%258C%25BA%25E5%2588%25AB&rsp=10&inputT=6110&rsv_sug4=7823)	  [C语言、C++和C#区别](https://blog.csdn.net/m0_61505785/article/details/139731794)	[C＃和C++的区别](https://www.cnblogs.com/AIBigTruth/p/11947272.html)	 [C语言、C++和C#的对比表格_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=%E4%BB%A5%E4%B8%8B%E6%98%AFC%E8%AF%AD%E8%A8%80%E3%80%81C%2B%2B%E5%92%8CC%23%E7%9A%84%E5%AF%B9%E6%AF%94%E8%A1%A8%E6%A0%BC)	 

1. **编程范式**: 

- ‌**C**‌：C是一种‌**过程式编程语言**‌，着重于数据和函数的结合，程序由函数组成，所有操作和计算依赖于函数调用。C没有内置的面向对象支持，主要强调直接操作内存和硬件‌
- ‌**C++**‌：C++是基于C的一种扩展语言，支持‌**多范式编程**‌，包括面向对象编程（OOP）、泛型编程和过程式编程。C++增加了类、继承、多态等面向对象特性，并支持模板和异常处理‌
- ‌**C#**‌：C#是一种‌**完全面向对象的编程语言**‌，不支持过程式编程。它主要用于构建Windows应用程序、Web应用程序和游戏（通过Unity引擎）‌

2. **内存管理**

- ‌**C**‌：C语言允许程序员手动控制内存分配和释放，需要使用`malloc`、`calloc`等函数分配内存，并通过`free`释放内存。这种手动管理内存的方式虽然灵活，但容易出错，需要开发者小心避免内存泄漏或野指针的出现‌
- ‌**C++**‌：C++延续了C的手动内存管理方式，但提供了`new`和`delete`关键字用于动态内存分配和释放。此外，C++还引入了智能指针（如`std::unique_ptr`和`std::shared_ptr`），使得内存管理变得更安全，减少了内存泄漏的风险‌
- ‌**C#**‌：C#提供了自动的垃圾回收机制（GC），所有的内存管理都由.NET环境自动完成，开发者不需要手动释放内存，这大大降低了内存泄漏的风险。然而，垃圾回收也会带来一定的性能开销‌

# IDE

[Downloads - MinGW-w64](https://www.mingw-w64.org/downloads/#mingw-builds) 

[Win10必备工具（重装系统必备）](https://cloud.tencent.com/developer/article/1980569)  [前端开发在线工具](https://cloud.tencent.com/developer/article/1142656)  [什么是QT](https://cloud.tencent.com/developer/article/2084699)    [AI开发工具](https://cloud.tencent.com/developer/article/2345726) 

IDE:       [Code::Blocks官网](https://www.codeblocks.org/)  [codeblocks](https://www.baidu.com/s?ie=UTF-8&wd=codeblocks)   [Code Blocks安装](https://www.jb51.net/softjc/716994.html)  [Code::Blocks](https://c.biancheng.net/view/467.html)  [CodeBlocks入门](https://cloud.tencent.com/developer/article/1101731)   [Code::Blocks 学习助手](https://blog.csdn.net/hongwenjun/article/details/6269535)   [下载 Code::Blocks](https://appzip.cn/codeblocks/w/download)  [CodeBlocks-20.03下载安装及中文](https://developer.aliyun.com/article/1499650)   [中文编译提示 Code::Blocks SVN6988学习增强版(适合C/C++初学者)](https://bbs.csdn.net/topics/360090434)   [C语言学习——IDE软件Code::Blocks教程](https://developer.aliyun.com/article/1049155)   [Code::Blocks 自动格式化代码](https://blog.csdn.net/hnjzsyjyj/article/details/119518211) 

[好：C语言编译器大全](https://www.bilibili.com/opus/941751311433465857?jump_opus=1)	



[code blocks中汉字下方有红色波浪线](https://blog.csdn.net/weixin_41290863/article/details/119608446)   [查看windows系统默认编码](https://blog.csdn.net/weixin_49114503/article/details/127945397)  [codeblock输出中文乱码问题](https://blog.csdn.net/mantou_riji/article/details/123596205)   [Illegal byte sequence|_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=converting%20to%20execution%20character%20set%3A%20Illegal%20byte%20sequence%7C)    [CodeBlocks快捷键](https://blog.csdn.net/u010278698/article/details/105822037/)

[CLion](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=CLion&oq=%2526lt%253Bode%253A%253ABlocks&rsv_pq=e5ef426100edcdd1&rsv_t=b0b89u%2FPrslJFwBNyfaKmj3iEdlB%2BK%2F%2FEGevpmxbBRqXtcy2Dv%2B%2B6o%2B5kY0&rqlang=cn&rsv_enter=0&rsv_dl=tb&rsv_n=2&rsv_sug3=1&rsv_sug1=1&rsv_sug7=100&rsv_btype=t&inputT=1281&rsv_sug4=1282)  [CLion安装](https://blog.csdn.net/annesede/article/details/133940779)   [CLion：JetBrains 出品的 C 和 C++ 跨平台 IDE](https://www.jetbrains.com/zh-cn/clion/) 

[C-Free下载和安装图文教程 - 编译器](https://www.dotcpp.com/course/340) 

[知心编译器（中文版C语言编译器-基于TCC-Tiny C Compiler）+IDE（集成开发环境-gtk+3 + Scintilla+SQLite3）](https://gitee.com/zhiyuyan/zhi)	 

Qt: [Qt（跨平台应用程序开发框架）](https://baike.baidu.com/item/Qt/451743?fr=ge_ala)   [视频](https://www.bilibili.com/list/ml2581384607?oid=696483292&bvid=BV1km4y1k7CW)   [Windows环境下Qt6 C++开发环境的在线下载与安装](https://blog.csdn.net/SeaBiscuitUncle/article/details/126595329) 

- 1991年由Qt Company开发的[跨平台](https://baike.baidu.com/item/跨平台/8558902?fromModule=lemma_inlink)C++[图形用户界面](https://baike.baidu.com/item/图形用户界面/3352324?fromModule=lemma_inlink)[应用程序](https://baike.baidu.com/item/应用程序/5985445?fromModule=lemma_inlink)开发框架

Boost:  [Boost程序库完全开发指南：深入C++准标准库(第4版) ](https://www.jb51.net/books/692139.html) 

- **Boost** 是一个功能强大、构造精巧、跨平台、开源并且完全免费的C++程序库，有着“C++‘准’标准库”的美誉。Boost 由C++标准委员会部分成员所设立的Boost 社区开发并维护，使用了许多现代C++编程技术，内容涵盖字符串处理、正则表达式、容器与数据结构、并发编程、函数式编程、泛型编程、设计模式实现等许多领域，极大地丰富了C++的功能和表现力

[Dev-C++](https://www.baidu.com/s?ie=utf-8&wd=Dev-C%2B%2B)   [Dev C++的下载和使用](https://blog.csdn.net/qq_45772965/article/details/109366056) 

[c/c++开发工具哪个好](https://www.qtvcd.com/com/cjj-tool.html)   [ C/C++ 语言的常用开发工具下载 ](https://codebus.cn/bestans/ide-download)   [ C/C++ 开发工具下载](https://cloud.tencent.com/developer/article/1820971) 

编译：  [编译_百度百科](https://baike.baidu.com/item/%E7%BC%96%E8%AF%91/1258343?fr=ge_ala)   [编译器 ](https://www.zhihu.com/topic/19629384/top-answers)     [编译](https://blog.csdn.net/m0_52642997/article/details/113147006)  [GCC编译过程（预处理->编译->汇编->链接）](https://zhuanlan.zhihu.com/p/111500914) 

[不建议新手用IDE，而是用编辑器＋编译器，用命令行编译](https://www.zhihu.com/question/300147676/answer/1585151369)   

c语言参考： [c/c++ 中文手册](https://blog.csdn.net/liyankang/article/details/128530859) 



[10款 C/C++ 开发IDE](https://zhuanlan.zhihu.com/p/12572402528)	 [10款C++工具](https://mbd.baidu.com/newspage/data/dtlandingsuper?nid=dt_5145394774624411659&sourceFrom=search_a)	

[C语言中的常见编译器](https://www.cnblogs.com/wuseng/p/18488797)	

## Windows平台主流IDE/编译器‌

[好：主流C语言开发环境汇总（15款IDE推荐）](https://www.54benniao.com/a/yvvd2h.html)	

[Anjuta_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=Anjuta)	[Eclipse平台C/C++开发实战指南-CSDN博客](https://blog.csdn.net/weixin_42598278/article/details/146233539)	[Netbeans 适配C/C++、JAVA](https://blog.csdn.net/ccozkf/article/details/104713183/)	

gcc的windows移植版： [MinGW](https://cloud.tencent.com/developer/article/2055112)	

ARM编译器: [ARM编译器及IDE开发环境](https://cloud.tencent.com/developer/article/2093936?policyId=1004)	

- ‌**Visual Studio (VS)**‌：微软开发的“宇宙最强IDE”，支持多语言（C/C++、Python等），集成调试、版本控制等功能，最新版VS2022优化了Debug体验。社区版免费，但商用需注意许可证。
- ‌**Dev-C++**‌: 轻量级开源IDE，内置GCC编译器，NOIP比赛指定工具，适合教学和非商业开发。
- ‌**Code::Blocks**‌: 跨平台开源IDE，支持多编译器（GCC、Clang等），ACM竞赛推荐工具。
- CLion
- Anjuta
- Netbeans

## 跨平台编译器核心工具链‌

- ‌**GCC**‌: GNU编译器套件，支持多语言（C/C++等），Linux系统默认编译器，对C11/C17标准支持良好。
  - GCC 原本作为 GNU 操作系统的官方编译器，现已被大多数类 Unix 操作系统（如Linux、BSD、Mac OS X等）采纳为标准的编译器，GCC 同样适用于微软的Windows。GCC 是自由软件过程发展中的著名例子，由自由软件基金会以 GPL 协议发布
    - g++是gcc的c++编译器,  c语言的编译器程序名叫gcc
  - Windows下比较流行的GCC移植版主要有三个，他们是 ==MinGW，Cygwin 和 Djgpp== 
- ‌**Clang**‌: LLVM前端，编译速度快、诊断信息清晰，macOS默认编译器，Windows可通过VS集成使用。

## 其他推荐工具‌

- ‌**Xcode**‌: macOS官方IDE，需安装Command Line Tools支持C编译。
- ‌**Eclipse**‌: 通过插件支持C开发，适合Java开发者复用环境。

‌**选择建议**‌：

- ‌**初学者**‌：优先选择Dev-C++或VS社区版（平衡功能与复杂度）。
- ‌**Linux/macOS开发者**‌：直接使用系统默认的[GCC](https://www.baidu.com/s?wd=GCC&usm=4&ie=utf-8&rsv_pq=cf54d4b70018a4a0&oq=c语言编译器有哪些&rsv_t=6aeb4RVMpW2wrJN%2FCWuuamC%2BXrVgoWDndzldvV6jZ8poWm0IjEVF0hFwBaw&rsv_dl=re_dqa_generate&sa=re_dqa_generate)或[Clang](https://www.baidu.com/s?wd=Clang&usm=4&ie=utf-8&rsv_pq=cf54d4b70018a4a0&oq=c语言编译器有哪些&rsv_t=5797dGetwxEUHgqrka7zLJOdUbaAU3HzlGnmLp%2Bbdc0F55dMxM8HdmfnJEk&rsv_dl=re_dqa_generate&sa=re_dqa_generate)。
- ‌**嵌入式开发**‌：需考虑交叉编译工具链（如[MinGW](https://www.baidu.com/s?wd=MinGW&usm=4&ie=utf-8&rsv_pq=cf54d4b70018a4a0&oq=c语言编译器有哪些&rsv_t=a470WMqHN9t9IF0ryW6%2FUjI2n9TRKvaP1gxdZnJPBKEhJZPDCyDRozR0cFY&rsv_dl=re_dqa_generate&sa=re_dqa_generate)）。

‌**注意事项**‌：

- MSVC对C99/C11支持有限，但可通过Clang插件弥补。

# 桌面应用程序开发框架

[7款桌面应用程序开发框架](https://blog.csdn.net/weixin_51627076/article/details/132818008)	[2024年windows原生应用用什么框架开发?](https://www.zhihu.com/question/6328848898)	 [跨平台开发工具开发Windows，linux，mac以及安卓和iOS软件](https://www.zhihu.com/question/300750046)	 [Windows桌面应用开发框架_百度搜索](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=Windows%E6%A1%8C%E9%9D%A2%E5%BA%94%E7%94%A8%E5%BC%80%E5%8F%91%E6%A1%86%E6%9E%B6&oq=Windows%25E6%25A1%258C%25E9%259D%25A2%25E5%25BA%2594%25E7%2594%25A8%25E5%25BC%2580%25E5%258F%2591%25E7%25AC%25AC%25E4%25B8%2589%25E6%2596%25B9%25E6%25A1%2586%25E6%259E%25B6&rqlang=cn&rsv_enter=1&rsv_dl=tb&rsv_sug3=2&rsv_sug1=1&rsv_sug7=100&rsv_sug2=0&rsv_btype=t&inputT=358&rsv_sug4=565)	

[桌面客户端应用开发](https://cloud.tencent.com/developer/article/2513404)	[win32框架有哪些_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=win32%E6%A1%86%E6%9E%B6%E6%9C%89%E5%93%AA%E4%BA%9B)	

[用wxWidgets写跨平台UI界面](https://blog.csdn.net/ablo_zhou/article/details/1867480)	 

[Win32++:可替代MFC的Windows桌面应用开发框架](https://blog.csdn.net/Rongbo_J/article/details/45128777)  	

[c++开发的经典软件_百度搜索](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=c%2B%2B%E5%BC%80%E5%8F%91%E7%9A%84%E7%BB%8F%E5%85%B8%E8%BD%AF%E4%BB%B6&oq=c%2523%25E5%25BC%2580%25E5%258F%2591%25E7%259A%2584%25E7%25BB%258F%25E5%2585%25B8%25E8%25BD%25AF%25E4%25BB%25B6&rqlang=cn&rsv_enter=1&rsv_dl=tb&rsv_btype=t&inputT=933&rsv_sug3=14&rsv_sug1=11&rsv_sug7=100&rsv_sug2=0&rsv_sug4=1796)	

`WinForm、WPF、MFC、wxWidgets、Qt、GTK、 Electron`

| **开发框架**  | **支持语言**                                  | **支持平台**            | **特点**                                                     |      |      |
| :------------ | :-------------------------------------------- | :---------------------- | :----------------------------------------------------------- | ---- | ---- |
| **WinForm**   | C#                                            | windows                 | ==图形控件类库==,基于.NET Framework，拖放方式快速创建用户界面 |      |      |
| **WPF**       | C#、VB.NET                                    | windows                 | WPF 的核心是一个与分辨率无关且基于矢量的呈现引擎，旨在充分利用现代图形硬件，基于Direct3D技术创建 |      |      |
| **MFC**       | C++                                           | Windows、Linux和macOS   | MFC是Microsoft提供的C++库                                    |      |      |
| **wxWidgets** | C、C++、Python、.NET、Lua、Ruby等。           | Windows、Linux和macOS等 | C++构架库                                                    |      |      |
| **Qt**        | C、C++、Python、Javascript等                  | Windows、Linux和macOS等 | C++框架                                                      |      |      |
| **GTK**       | C、C++、 C#、 Python、 Java、 Perl、 .NET等。 | Windows、Linux和macOS等 | `The GIMP Toolkit`,  C语言图形界面库                         |      |      |
| **Electron**  | HTML、CSS 、 JavaScript等                     | Windows、Linux和macOS等 | 使用Node.js（作为后端）和Chromium（作为前端）完成桌面GUI应用程序的开发 |      |      |
| **UWP**       |                                               |                         | Windows 10中引入的平台                                       |      |      |

## WinForm、MFC、WPF

[winform wpf mfc_百度搜索](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=winform%20wpf%20mfc&oq=Windows%25E6%25A1%258C%25E9%259D%25A2%25E5%25BA%2594%25E7%2594%25A8%25E5%25BC%2580%25E5%258F%2591%25E6%25A1%2586%25E6%259E%25B6&rsv_pq=88d2a75f001a356f&rsv_t=fc696LwaYUTjE0jkGYpkarfzzHYemrMYF6%2FujNgjIbprMMJkaBQRMGmoSsk&rqlang=cn&rsv_enter=1&rsv_dl=tb&rsv_sug3=16&rsv_sug1=14&rsv_sug7=100&rsv_sug2=0&rsv_btype=t&inputT=18256&rsv_sug4=18257)	 [ WinForm、MFC、WPF](https://www.zhihu.com/question/435492936/answer/3524225135)     [MFC,WinForm,WPF](https://www.cnblogs.com/ranjiewen/p/5316899.html)	 [VS2022项目类型比较：控制台、MFC、WPF与WinForm](https://blog.csdn.net/weixin_42433809/article/details/134174135)	

[WinForm和WPF有什么区别 ](https://worktile.com/kb/ask/54691.html)	 [Winform和WPF的技术对比](https://blog.csdn.net/sixpp/article/details/142888188)	 

MFC: [MFC_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=MFC) [MFC_百度百科](https://baike.baidu.com/item/MFC/2236974)	   [MFC入门](https://www.cnblogs.com/yangyuqing/p/10283641.html)		  [MFC 快速入门](https://www.jianshu.com/p/0324359b567c)	 

WPF: [WPF](https://blog.csdn.net/qq_3517289697/article/details/141262770)	[WPF_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=WPF)	

WinForm： [WinForm_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=WinForm)	

1. **MFC** : `Microsoft Foundation Classes`, 微软基础类库
2. **WinForm**： 微软提供的一种图形用户界面（GUI）框架
3. **WPF** ： `Windows Presentation Foundation`，Windows呈现基础
   1. 基于Windows Vista的用户界面框架， 属于.NET Framework 3.0的一部分
   2. WPF被视为是WinForm的升级版本
   3. WinForm基于传统的Windows窗体应用程序设计，而WPF是基于XAML的应用程序框架，采用了更为现代化的设计理念。

## .NET框架

[.NET框架_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=.NET%E6%A1%86%E6%9E%B6)	

[.NET Framework 框架](https://cloud.tencent.com/developer/article/1455030?policyId=1003)	 

[.NET Framework 和 .NET Core 区别](https://blog.csdn.net/weixin_61361738/article/details/129866848) 	

​	

# GUI应用程序开发框架

[C++ GUI 框架大列表](https://zhuanlan.zhihu.com/p/5694948096)	

[Qt Creator](https://blog.csdn.net/bao_Heng/article/details/139523698)	

