##### 资料

[windows脚本概述](https://www.cnblogs.com/2018/archive/2010/09/18/1830407.html)   [Windows 脚本架构](https://blog.csdn.net/erix1991/article/details/14103253)  [VBScript 用法 ](https://www.runoob.com/vbscript/vbscript-howto.html) [VBScript 函数](https://www.runoob.com/vbscript/vbscript-ref-functions.html)  [VBScript详解](https://blog.csdn.net/slforeverlove/article/details/47048225)  [VB代码vb小程序：系统管理工具 WMI(winmgmts)](http://blog.sina.com.cn/s/blog_b1879bb401018jbi.html) [WMI系统管理工具](https://www.cnblogs.com/bclshuai/p/14235574.html)  [WMI技术介绍和应用](https://fangliang.blog.csdn.net/article/details/50644688?utm_medium=distribute.pc_relevant.none-task-blog-searchFromBaidu-3.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-searchFromBaidu-3.control)  [WMI技术介绍和应用](https://blog.csdn.net/breaksoftware/article/details/8424317)  

[跟我从头学WSH](https://www.cnblogs.com/starspace/archive/2009/01/06/1369934.html) [Wscript对象详解](https://www.cnblogs.com/aademeng/articles/12638537.html)  [WScript 对象的属性和方法](https://www.jb51.net/shouce/script56/Script56_chs/html/wsoriWScriptObjectPropMeth.htm) [在线手册 - 51windows.Net](http://doc.51windows.net/)

[自动运行Windows - Windows Sysinternals | Microsoft Docs](https://docs.microsoft.com/zh-cn/sysinternals/downloads/autoruns)

Wscrip对象是一个内在的对象，意思是当脚本执行的时候自动创建，而不需要明确的实例化.
支持以下的方法：Echo、Createobject、Quit等

[SWbemServices 方法 (Wbemdisp.tlb) - Win32 apps | Microsoft Docs](https://docs.microsoft.com/zh-cn/windows/win32/wmisdk/swbemservices-delete)   [VBS脚本编程（10）——编写WMI脚本 - 爱码网](https://www.likecs.com/show-135293.html)

例子里的get、ExecQuery、InstancesOf等方法是 WMI 脚本 API 的 SwbemServices对象的方法  

##### Windows 脚本架构

```
什么是对象模型： 一组实现了相关功能的对象的集合，常用的对象模型（WSH   WMI  ADSI  ADO CDO ），已经封装，会调用就行。
```

# VBscript

1. 变量：Dim、Public 或 Private 语句声明 ；数组变量用于在一个单一的变量中存储多个值，Dim names(2)，注释用单引号或rem,分行用_，使用 Option Explicit 语句后，必须使用 dim、public 或 private 语句来声明所有的变量。

1. 常量：const

3. 字符串

   ```
   用""包含起来，使用&或+连接字符串
   ```

   

2. 错误处理Err

2. vbscript程序：  

   ```
   子程序：封装在 Sub 和 End Sub 语句内，不会返回值，可带参数
   函数程序：封装在 Function 和 End Function 语句内
   ```

6. 条件语句

   ```
   四种条件语句：
   If 					条件为 true 时执行一系列的代码
   If...Then...Else 	 执行两套代码其中之一
   If...Then...ElseIf	 选择多套代码之一来执行
   Select Case 		 选择多套代码之一来执行
   ```

   ```
   条件为 true 时执行不止一条语句，必须在一行写一条语句，然后使用关键词 "End If" 来结束这个语句：
   If i=10 Then
   alert("Hello")
   i = i+1
   End If
   ```
   选择多套代码之一来执行，可以使用 If...Then...ElseIf 语句
   ```
   i=hour(time)
   If i = 10 Then
   document.write("Just started...!")
   ElseIf i = 11 Then
   document.write("Hungry!")
   ElseIf i = 12 Then
   document.write("Ah, lunch-time!")
   ElseIf i = 16 Then
   document.write("Time to go home!")
   Else
   document.write("Unknown")
   End If
   ```

   ```
   d=weekday(date)
   Select Case d
   Case 1
   document.write("Sleepy Sunday")
   Case 2
   document.write("Monday again!")
   Case 3
   document.write("Just Tuesday!")
   Case 4
   document.write("Wednesday!")
   Case 5
   document.write("Thursday...")
   Case 6
   document.write("Finally Friday!")
   Case else
   document.write("Super Saturday!!!!")
   End Select
   ```

   

7. 循环

   ```
   四种循环语句：通过 Exit For退出 For...Next 语句
   For...Next				运行一段代码指定的次数
   For Each...Next			针对集合中的每个项目或者数组中的每个元素来运行某段代码
   Do...Loop				运行循环，当条件为 true 或者直到条件为 true 时
   While...Wend			不要使用这个语句 - 请使用 Do...Loop 语句代替它
   ```

   ```
   For i=10 To 2 Step -2   '递减计数变量，使用负的 Step 值
   some code
   Next
   ```

   ```
   For Each x In cars    document.write(x & "<br />")   Next
   ```

   ```
   不知道重复多少次，使用 Do...Loop。
   Do...Loop 语句重复执行某段代码直到条件是 true [用while]或条件变成 true[用until]
   ```

   

8. 参数输入

   ```
   
   ```
##### windows脚本宿主(WSH)    [WSH脚本宿主Wscript脚本主对象](https://www.cnblogs.com/nemolog/archive/2006/02/03/324968.html)

```
    1.WSH架构
    2.WSH对象：分4个部分
    WScript
    WshShell
    WshNetwork
    WshController
```

##### 对象模型WMI    [系统管理工具 WMI新浪博客 ](http://blog.sina.com.cn/s/blog_b1879bb401018jbi.html)

WMI 的对象使用路径的形式表示，如：\\.\root\cimv2:win32_service，第一个元素是目标计算机的名字（. 代表是本地系统），第二个元素是相应的WMI命名空间，第三个元素是相应的类名(对象)

[WMI Windows 管理规范](https://www.cnblogs.com/gordensong/p/3863169.html)  [WMI 参考 - Win32 apps | Microsoft Docs](https://docs.microsoft.com/zh-cn/windows/win32/wmisdk/wmi-reference?view=vs-2019)

   ```
    WMI命名空间
   　 1、root          作为所有其他名字的占位符；
   　 2、root\default  与注册表操作有关的类；
   　 3、root\security 与系统安全有关的类；
   　 4、root\cimv2    从CIM派生的类，代表我们最常用的工作环境。
   　 
   WMI的查询语言:WQL数据查询　 Select pro1 , pro2 , pro3 from myclass（myclassevent）
   Select * from Win32_share where name=”Admin”     Where 用于限定查询的范围
   ```

   ```
   使用的三步骤
   　 1.建立一个到目标计算机上的 Windows 管理服务的连接　   Set WMI = GetObject("winmgmts:\\.\root\CIMV2")
   　 2.检索 WMI 托管资源实例					  　   Set Ps = WMI.InstancesOf("Win32_Processor")
   　 3.枚举检索得到集合的内容
   　    For Each P In Ps
   　        msgbox P.Name
   　    Next
   　 也可以将 1、2两步合并为一步：Set Ps = GetObject("winmgmts:\\.\root\CIMV2").InstancesOf("Win32_Processor")
   ```

   查看"WinMgmts:"的详细对象(子集)、属性和方法，用 WMI 测试器：wbemtest.exe   [MSFT 类](https://docs.microsoft.com/zh-cn/windows/win32/wmisdk/msft-classes)

   ```
   两个下划线为开头的是系统类。 系统类是预定义的 CIM 类，支持内部 WMI 配置与操作，例如提供程序注册、命名空间安全性及事件通知等。
   CIM_ 开头的类是由 DMTF 维护的核心与公共基类。
   Win32_ 开头的类是 Microsoft 扩展类，表示 Windows 特定的托管资源。
   ```

   WQL wmi查询语言：sql的一个子集，不支持更新、删除、排序等操作，可用于返回选定实例的选定属性。

```
WMI事件处理：例如cpu30秒内80%，给我发个Email。
```

用工具创建WMI脚本   

```
wmic：/？  上面是全局开关  下面是定义好的adsl别名
```

windows上下文命令 

[netsh | Microsoft Docs](https://docs.microsoft.com/zh-cn/windows-server/administration/windows-commands/netsh?view=vs-2015)   [Netsh](https://www.cnblogs.com/UmaruChan/p/13976378.html)

永久事件订阅：用事件过滤器描述关心的事件__EventFilter类，用事件消费者描述想做的动作__EventConsumer类，一开始动作和事件不相关，用关联绑定，将相应的事件和动作关联起来__FilterToConsumerBinding类。

[主页劫持](https://www.zhihu.com/question/55396610/answer/152584271)  [利用WMI打造完美“三无”后门-The Core | Demon's Blog](http://demon.tw/copy-paste/vbs-wmi-trojan-3.html)  [浏览器快捷方式被修改的元凶 - 心亦 - 博客园 (cnblogs.com)](https://www.cnblogs.com/szhx/p/5296822.html) [中招了——WMI脚本劫持浏览器 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/24216079) [跟我从头学WMI（一），介绍WMI - 覆雨翻云 - 博客园 (cnblogs.com)](https://www.cnblogs.com/railgunman/articles/1810593.html)

# Powershell

[为什么Windows PowerShell命令称为Cmdlet](https://blog.csdn.net/culunxun2863/article/details/108840523)

```
都是动词-名词，get-service; 
cmdlet都有参数，实参   cmdlet     parameter     actual parameter  例：get-service -name ALG   //查看名字为alg的服务
get-help        Update-Help -UICulture zh-cn  出错用Update-Help -ErrorAction SilentlyContinue
get-help start-service -full获取全部帮助信息
语法格式：-name <string> 必须，尖括号字符串类型；[-name <string>]可选，非必须；[-name <string[]> ]可接受多个类型为string的实参,string表实参，用[]表示多个。 

get-verb,名词任意组合。get-command *vm* 找关于vm的命令  get-member获得对象成员
Get-Service -Name ALG | Get-Member
Get-Service -Name ALG | Select-Object * 获取alg所有属性
get-vm | where-object {$_.name -like "*5*"}筛选名字里有5的虚拟机，$_一次获取管道传入所有对象。正常情况下管道一次传一个对象。
```

```
声明变量$var = get-vm
foreach-Object要写在管道后面
@()数组；环境变量$env:  `折行
get-help Get-Service -showwindow
Get-Alias别名 gal   get-alias -definition get-process 查命令别名
Get-Help Get-Event -Detailed
 Get-EventLog -LogName System -Newest 3 -EntryType Error -ComputerName dc1,dc2,dc3 3台电脑最新的3个系统错误信息
 cls ; 分号是语句分隔符，表有并行动作
 help about_*  help模块从3个帮助系统获取信息，commandlet帮助系统和about_help系统，catagory    get-help -category  Provider
 Export-Csv -Path d:\    out-file c:\1.txt   
 -whatif假设命令运行    Get-Module -ListAvailable可用的模块
 
```

