[手抓动态基址教程](https://www.bilibili.com/video/BV1r4421Z7Gk/?vd_source=7346303e5e18677d7261c2c0c109ecfd)  

[特征码定位](https://www.bilibili.com/video/BV1Bb4y1i7M1/?vd_source=7346303e5e18677d7261c2c0c109ecfd)	 [特征码定位基地址](https://www.bilibili.com/video/BV1Dj411F7Z2/?vd_source=7346303e5e18677d7261c2c0c109ecfd)   [搜索特征码定位64位游戏基址及call地址](https://www.bilibili.com/video/BV1Vt4y177cZ/?vd_source=7346303e5e18677d7261c2c0c109ecfd)	[动态定位基址](https://www.bilibili.com/video/BV1JF411M72E/?vd_source=7346303e5e18677d7261c2c0c109ecfd)   [查找基址](https://www.bilibili.com/video/BV1hY411g7mG/?vd_source=7346303e5e18677d7261c2c0c109ecfd)  

[基址和动态地址的含义](https://www.bilibili.com/video/BV15uYqeMEEP/?vd_source=7346303e5e18677d7261c2c0c109ecfd)	 [理解CE追基址的过程](https://www.bilibili.com/video/BV14H4y1R7v4/?vd_source=7346303e5e18677d7261c2c0c109ecfd)  			  		

[游戏逆向](https://www.bilibili.com/video/BV1FF4neUEdq?spm_id_from=333.788.recommend_more_video.1&vd_source=7346303e5e18677d7261c2c0c109ecfd)	

视频： [好：CE](https://www.bilibili.com/video/BV1zwLizQE3K?vd_source=7346303e5e18677d7261c2c0c109ecfd&p=2&spm_id_from=333.788.videopod.episodes)   [CE](https://www.bilibili.com/video/BV1GY411J7hy?vd_source=7346303e5e18677d7261c2c0c109ecfd&spm_id_from=333.788.videopod.sections)	[实现自瞄+透视](https://www.bilibili.com/video/BV1CYZtYTEXc?spm_id_from=333.788.recommend_more_video.0&vd_source=7346303e5e18677d7261c2c0c109ecfd)	  [ce生成修改器](https://www.bilibili.com/video/BV1Eg4y1X7ey?vd_source=7346303e5e18677d7261c2c0c109ecfd&p=15&spm_id_from=333.788.videopod.episodes)		 [CE](https://www.bilibili.com/video/BV1R4421S7YT?spm_id_from=333.788.recommend_more_video.0&vd_source=7346303e5e18677d7261c2c0c109ecfd) 	[CE](https://www.bilibili.com/video/BV1f54y1i71W/?vd_source=7346303e5e18677d7261c2c0c109ecfd)	 [CE入门](https://www.bilibili.com/video/BV1Eg4y1X7ey/?vd_source=7346303e5e18677d7261c2c0c109ecfd)	[CE](https://www.bilibili.com/video/BV1J94y1D7aA/?vd_source=7346303e5e18677d7261c2c0c109ecfd)	

[内存](https://www.bilibili.com/video/BV1W154zqE8p?spm_id_from=333.788.recommend_more_video.5&vd_source=7346303e5e18677d7261c2c0c109ecfd)	

[Tutorial Game学习](https://www.52pojie.cn/thread-1222346-1-1.html)	

# 初阶

| ![](./CE教程.assets/Snipaste_2025-04-25_14-34-57.jpg) | ![](./CE教程.assets/Snipaste_2025-04-25_14-38-11.jpg) |
| ----------------------------------------------------- | ----------------------------------------------------- |
| ![](./CE教程.assets/Snipaste_2025-04-25_15-18-30.jpg) | ![](./CE教程.assets/Snipaste_2025-04-25_15-20-10.jpg) |
| ![](./CE教程.assets/Snipaste_2025-04-25_15-21-24.jpg) | ![](./CE教程.assets/Snipaste_2025-04-25_15-22-05.jpg) |
| ![](./CE教程.assets/Snipaste_2025-04-25_15-31-46.jpg) | ![](./CE教程.assets/Snipaste_2025-04-25_15-39-11.jpg) |
| ![](./CE教程.assets/Snipaste_2025-04-25_15-40-15.jpg) | ![](./CE教程.assets/Snipaste_2025-04-25_15-41-20.jpg) |
| ![](./CE教程.assets/Snipaste_2025-04-25_15-42-15.jpg) | ![]()                                                 |

## 找出看不到数值的内存地址

自带游戏3: 

float， 角色右移，数值增加

找到内存地址，右键 `浏览相关内存区域` ^+B, 右键显示类型，4字节十进制

跳跃是Y坐标,左右移是X坐标

内存单元从0变1的，是角色死亡等状态改变

# ==指针路径==

[指针路径和虚拟地址区别_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=%E6%8C%87%E9%92%88%E8%B7%AF%E5%BE%84%E5%92%8C%E8%99%9A%E6%8B%9F%E5%9C%B0%E5%9D%80%E5%8C%BA%E5%88%AB)	[动态内存管理_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=%E5%8A%A8%E6%80%81%E5%86%85%E5%AD%98%E7%AE%A1%E7%90%86)	

[好：C语言动态内存管理](https://cloud.tencent.com/developer/article/2479567)	[动态内存管理](https://blog.csdn.net/jupangMZ/article/details/131924266)	

[linux内核中 逻辑地址、虚拟地址、线性地址和物理地址](https://zhuanlan.zhihu.com/p/586987392)	

1. **指针路径**‌：指针是一个变量，它存储的是内存地址。在C语言中，指针用于存储和管理内存地址，是实现间接访问和动态内存管理的关键。指针存储的是虚拟地址，而不是直接的物理内存地址‌12。
2. ‌**虚拟地址**‌：虚拟地址是程序运行时使用的地址空间，由操作系统提供。每个进程都有自己独立的虚拟地址空间，这些空间的大小取决于系统的位数（如32位系统的虚拟地址空间为4GB，64位系统则更大）。虚拟地址是抽象的，程序不需要关心实际的物理内存布局‌

> 静态地址： 每次打开游戏，`静态指针的内存地址不变`, ==静态指针的数值是随机的==,重开游戏，或进入新的区域等会改变; 所以每次打开游戏，想找到==想修改的数值==的内存地址，要找到表格中标为黄色的数值，需要反过来，从目标数值入手。
>
> 从内存中的数值，找出内存地址，找出偏移量
>
> 1. 从数值找到内存地址
> 2. 根据内存地址，找到偏移量，偏移量保存在操作码中
> 3. 根据`偏移量`和`下级的内存地址`，可以计算出`上级的数值`
> 4. 以此类推，找出各级的偏移量
> 5. 最终找到静态地址
>
> 各级指针的`偏移量也不变`

**指针路径**：各级指针，以及它们最终指向的内存地址的关系链条 ; 各级指针的偏移量是不变的

- 手动整理法
- 指针地图法

| ![](./CE教程.assets/Snipaste_2025-04-25_15-44-53.jpg) | ![](./CE教程.assets/Snipaste_2025-04-25_16-10-05.jpg) |
| ----------------------------------------------------- | ----------------------------------------------------- |
| ![](./CE教程.assets/Snipaste_2025-04-25_16-12-07.jpg) | ![](./CE教程.assets/Snipaste_2025-04-25_16-14-48.jpg) |
| ![](./CE教程.assets/Snipaste_2025-04-25_16-44-16.jpg) | ![](./CE教程.assets/Snipaste_2025-04-25_16-45-32.jpg) |
| ![](./CE教程.assets/Snipaste_2025-04-25_16-46-26.jpg) | ![](./CE教程.assets/Snipaste_2025-04-25_16-47-20.jpg) |
| ![](./CE教程.assets/Snipaste_2025-04-25_16-47-44.jpg) | ![](./CE教程.assets/Snipaste_2025-04-25_17-01-00.jpg) |
| ![](./CE教程.assets/Snipaste_2025-04-25_17-03-11.jpg) | ![]()                                                 |

## 手动查找

1. **目标数值**： 首先找到数值的地址，然后再查找是什么改写了这个地址（最低部的目标数值用写入） 
2. 再次改变数值，CE 便可以列出找到的汇编代码， 如果看到方括号，那很可能表示我们已经==找到需要的指针==
   1. `mov [rsi+18],eax` ,add: 08b2e318 , value: 500
   2. `rsi+18` 必定是这个内存地址 `08b2e318`， rsi有可能是上一级指针的数值, 18应该是偏移量
3. ==找出上级指针数值==： 搜索 `ox08b2e318-0x18`, 搜出来的value不像是个内存地址，改为十六进制显示
   1. 根据内存地址，找出当前级和上级指针的偏移量, 右键：什么读取了这个地址
      1. 用什么改写（读取），是为了在操作码查看==偏移量==
      2. `lv=1,Offset=0`
4. 最后找到绿色的，就是静态地址: 每次打开地址不变，数值随机
5. 点击"手工添加地址"按钮，并勾选"指针"选项
   1. 用==手动添加地址==写： 动态==找目标内存地址==的公式 ，这样重新打开，改变数值和地址列表里的数值，是同时改变的
   2. 最后找到的静态地址 加 偏移量 等于 地址 : `[01bc8a40+10]->01b4b100` 左边是地址，箭头右边是数值
   3. `[EAX*2+EDX+00000310] , eax=4C 并且 edx=00801234`   
   4. 这种情况下 EDX 便是数值的指针，而 `EAX*2+00000310` 则是它的偏移量, 所以你要填在"Offset (Hex)"的将是 `2*4C+00000310=3A8`

| ![](./CE教程.assets/Snipaste_2025-04-27_12-18-19.jpg)        | ![一级指针数值](./CE教程.assets/Snipaste_2025-04-27_12-30-32.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![二级指针数值](./CE教程.assets/Snipaste_2025-04-27_12-42-22.jpg) | ![](./CE教程.assets/Snipaste_2025-04-27_13-06-50.jpg)        |

## 指针地图法

更省事

1. 搜到地址
2. 右键`Generate pointermap`： 指针映射集, 保存
3. `Change pointer`，相当于游戏中重新开始，或读档等,游戏重置指针路径, 数值和地址列表里的数值就不关联了
4. 根据新的数值，搜到新的地址
5. 右键重新扫描指针地图： 可以不用`Generate pointermap`， 用 `pointer scan for this address`
   1. 勾选： 与其它保存的指针地图结果对比
   2. 底部最大偏移量：4095,4k  level: 最大指针层级7
6. 如果对比后有很多
   1. 改变指针，指针扫描器=>重新扫描内存，数值


# 高阶

自动汇编、共享代码

| ![](./CE教程.assets/Snipaste_2025-04-25_18-55-49.jpg) | ![](./CE教程.assets/Snipaste_2025-04-25_18-57-05.jpg) |
| ----------------------------------------------------- | ----------------------------------------------------- |
| ![](./CE教程.assets/Snipaste_2025-04-25_18-58-02.jpg) | ![](./CE教程.assets/Snipaste_2025-04-25_18-59-02.jpg) |
| ![](./CE教程.assets/Snipaste_2025-04-25_19-00-28.jpg) | ![](./CE教程.assets/Snipaste_2025-04-25_19-01-52.jpg) |
| ![](./CE教程.assets/Snipaste_2025-04-25_19-02-30.jpg) | ![](./CE教程.assets/Snipaste_2025-04-25_19-03-23.jpg) |
| ![](./CE教程.assets/Snipaste_2025-04-25_19-05-00.jpg) | ![](./CE教程.assets/Snipaste_2025-04-25_19-06-06.jpg) |

## 汇编指令

[二的补码表示负数_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=%E4%BA%8C%E7%9A%84%E8%A1%A5%E7%A0%81)	

标签用来指代内存地址，汇编之后，汇编器会将标签转换为具体的内存地址

xor：不同时返回1，否则返回0; `同为0,异为1`  [什么是异或](https://www.cnblogs.com/fantyovo/p/14787250.html) 	

- xchg : 将2个操作对象数值互换
- lea : `load effective address`， 加载有效地址
  - `lea rax,[rax+0xFF]`:  将内存地址本身放到 `rax`
- imul: 有符号数乘法
- jg : jng `greater大于`

| ![](./CE教程.assets/Snipaste_2025-04-25_19-08-09.jpg)        | ![](./CE教程.assets/Snipaste_2025-04-25_19-11-37.jpg)     |
| ------------------------------------------------------------ | --------------------------------------------------------- |
| ![标签简写类似变量](./CE教程.assets/Snipaste_2025-04-27_16-12-49.jpg) | ![符号](./CE教程.assets/Snipaste_2025-04-27_16-17-07.jpg) |
| ![二的补码](./CE教程.assets/Snipaste_2025-04-25_19-27-00.jpg) | ![]()                                                     |

## ==共享代码==

[ce](https://www.bilibili.com/video/BV1FT411H79U/?vd_source=7346303e5e18677d7261c2c0c109ecfd) 	

一条操作码，会写入多个内存地址

找到我方，跳过伤害

- 找到谁改写了这个地址，然后再`memory viewer`中右键，"找出指令访问的地址", 让后在游戏中改变数值
- 给我方分组，右键 `find commonalities between address`,分为第1组
- 然后全选，右键 `find commonalities between address`， `scan for commonalities`, 找出地址之间的共同性
  - 原指令中是 `rax`，所以这里选 `rax`，双击，结构对比，扫描，保存
  - 偏移是十六进制，分组里的是十进制

| ![](./CE教程.assets/Snipaste_2025-04-28_14-07-02.jpg) | ![](./CE教程.assets/Snipaste_2025-04-28_14-15-31.jpg)        |
| ----------------------------------------------------- | ------------------------------------------------------------ |
| ![](./CE教程.assets/Snipaste_2025-04-28_14-16-56.jpg) | ![找到我方，跳过伤害](./CE教程.assets/Snipaste_2025-04-28_14-17-38.jpg) |
| ![](./CE教程.assets/Snipaste_2025-04-28_14-19-15.jpg) | ![](./CE教程.assets/Snipaste_2025-04-28_14-21-35.jpg)        |
| ![](./CE教程.assets/Snipaste_2025-04-28_14-22-52.jpg) | ![]()                                                        |



```assembly
[ENABLE]
alloc(newmem,2048,"gtutorial-x86_64.exe"+43F70) 
label(returnhere)
label(originalcode)
label(exit)

label(skip_here_if_player) //加标签
//加额外对敌伤害
alloc(extra_damage,4,"gtutorial-x86_64.exe"+43F70)
registerSymbol(extra_damage)
newmem:

originalcode:

//找出我方，跳过伤害
cmp qword [rdx+698],14
jz skip_here_if_player
//加个额外对敌伤害
sub eax,dword [extra_damage]
mov [rdx+60],eax
lea rsp,[rbp+00]

skip_here_if_player:

exit:
jmp returnhere

"gtutorial-x86_64.exe"+43F70:
jmp newmem
nop 2
returnhere:
 
 
[DISABLE]
dealloc(*)
unregisterSymbol(*)

dealloc(newmem)
"gtutorial-x86_64.exe"+43F70:
mov [rdx+60],eax
lea rsp,[rbp+00]
```



## 浮点数

| ![](./CE教程.assets/Snipaste_2025-04-28_15-27-33.jpg) | ![](./CE教程.assets/Snipaste_2025-04-28_15-42-40.jpg) |
| ----------------------------------------------------- | ----------------------------------------------------- |
| ![](./CE教程.assets/Snipaste_2025-04-28_15-44-42.jpg) | ![](./CE教程.assets/Snipaste_2025-04-28_15-46-32.jpg) |
| ![](./CE教程.assets/Snipaste_2025-04-28_15-47-12.jpg) | ![]()                                                 |



## 其它

| ![](./CE教程.assets/Snipaste_2025-04-25_20-36-18.jpg) | ![](./CE教程.assets/Snipaste_2025-04-25_20-37-10.jpg) |
| ----------------------------------------------------- | ----------------------------------------------------- |

# ==自动汇编==

[CE的三种注入方式与区别](https://blog.csdn.net/qq_50749602/article/details/116456771)	[CEAA自动汇编脚本常用命令](https://blog.csdn.net/qwq1503/article/details/103031668/)	 [CEAA脚本_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=CEAA%E8%84%9A%E6%9C%AC)	

一般不在 `Memory Viewer`里直接改代码，因为是一次性的，而是用 `auto assemble`里的模板

先添加`Cheat Table framework code`， 再添加 `Code injection`

## 什么是AOB注入	

[不找指针AOB注入快速修改代码](https://cntworld.cn/17449.html)	[CE自动汇编之AOB注入](https://blog.csdn.net/qiuqiuit/article/details/128768039)	

[Search](https://cn.bing.com/search?q=%E5%86%99%E5%9C%A8%E5%89%8D%E9%9D%A2%E6%88%91%E6%98%AF%E8%A6%81%E8%AE%B2%E8%BF%B0%E4%B8%80%E4%B8%AA%E5%85%B3%E4%BA%8EAOB%E6%B3%A8%E5%85%A5%E5%8E%9F%E7%90%86%E7%9A%84%E6%96%87%E7%AB%A0%EF%BC%8C%E5%9B%A0%E4%B8%BA%E6%B2%A1%E6%9C%89%E7%9B%B8%E5%85%B3%E7%9A%84%E6%95%99%E7%A8%8B%EF%BC%8C%E6%89%80%E4%BB%A5%E6%88%91%E6%9D%A5%E7%BB%99%E5%A4%A7%E5%AE%B6%E8%AF%A6%E7%BB%86%E7%9A%84%E8%AE%B2%E8%A7%A3%E4%B8%80%E4%B8%8B%EF%BC%8C%E5%BD%93%E7%84%B6%EF%BC%8C%E4%BB%BB%E4%BD%95%E8%AF%AD%E8%A8%80%E6%9C%80%E9%87%8D%E8%A6%81%E7%9A%84%E8%BF%98%E6%98%AF%E5%8A%A8%E6%89%8B%E8%83%BD%E5%8A%9B%EF%BC%8C%E5%B8%8C%E6%9C%9B%E5%A4%A7%E5%AE%B6%E8%83%BD%E5%A4%9F%E8%B7%9F%E7%9D%80%E6%88%91%E7%9A%84%E6%AD%A5%E4%BC%90%EF%BC%8C%E4%B8%80%E6%AD%A5%E6%AD%A5%E6%8F%AD%E5%BC%80AOB%E6%B3%A8%E5%85%A5%E7%9A%84%E7%A5%9E%E7%A7%98%E9%9D%A2%E7%BA%B1%EF%BC%8C%E7%AF%87%E5%B9%85%E5%8F%AF%E8%83%BD%E8%BE%83%E4%B8%BA%E9%95%BF%EF%BC%8C%E6%88%91%E4%B9%9F%E8%BF%9B%E8%A1%8C%E4%BA%86%E4%B8%80%E4%B8%8B%E6%8E%92%E7%89%88%E6%96%B9%E4%BE%BF%E5%A4%A7%E5%AE%B6%E9%98%85%E8%AF%BB%E4%BB%A5%E5%8F%8A%E7%90%86%E8%A7%A3%EF%BC%8C%E4%BB%A5%E4%B8%8B%E6%88%91%E5%B0%86%E4%B8%BB%E8%A6%81%E4%BB%A5%E5%9B%9B%E4%B8%AA%E9%83%A8%E5%88%86%E4%B8%BA%E4%B8%BB&form=QBLHCN&sp=-1&lq=0&pq=&sc=0-0&qs=n&sk=)	[不找指针AOB注入快速修改代码](https://cntworld.cn/17449.html)	   [CE自动汇编之AOB注入](https://blog.csdn.net/qiuqiuit/article/details/128768039)    [AOB注入原理深入浅出分析](https://www.52hb.com/thread-52588-1-2.html) 	 

修改汇编后执行是有效果的，但是下次再次进入后它的地址会发生改变的，还要再次寻找指针找汇编并修改。如果是修改汇编代码可以使用AOB注入，这样下次进入的时候AOB来定位这一段汇编代码段。AOB很高效是不需要像找指针那样一步步找基址，再找到每一级的偏移。AOB是==通过搜索特征码来定位==的。



AOB（`Array of byte Injection 字节数组注入`）是一系列唯一的字节数组，除了我们的指令能在内存中生成这些字节数组外，内存中的其它任何地方都不会再有这样的字节。这将有助于作弊者在游戏重新启动后，通过查找这些字节码，再次准确的提取那些动态地址, 更快的捕捉到想要的代码行，实现动态调试修改



| ![](./CE教程.assets/aob.jpg)                          | ![](./CE教程.assets/Snipaste_2025-04-28_10-43-06.jpg) |
| ----------------------------------------------------- | ----------------------------------------------------- |
| ![](./CE教程.assets/Snipaste_2025-04-28_10-47-02.jpg) | ![](./CE教程.assets/Snipaste_2025-04-28_10-47-43.jpg) |

# LUA脚本

查看lua脚本.md

# 创建窗体

[Tutorial - Creating a Form - GUI](https://wiki.cheatengine.org/index.php?title=Tutorial:LuaFormGUI)	

# 作弊表格

# D3D

# CE自带教程

## 游戏

### step1



[CE6.8 STEP 1,2,3](https://www.52pojie.cn/thread-828602-1-1.html)	

每次修改要打开模板，麻烦，申请一个符号作为全局变量：

- 注释掉 `sub edx,15`, 取消注释： `sub edx,dword [Extra_Damage]`, 符号`Extra_Damage`可作为全局变量，在ce其它地方使用
- `add address manually`里添加 `Extra_Damage`改变数值，还可以添加下拉菜单：右键 `set/change dropdown selection options`, 0:zero  5:five

最后加上 `dealloc(*) unregisterSymbol(*)` 释放内存和符号

| ![](./CE教程.assets/Snipaste_2025-04-28_11-00-31.jpg) | ![](./CE教程.assets/Snipaste_2025-04-28_11-01-59.jpg) |
| ----------------------------------------------------- | ----------------------------------------------------- |
| ![](./CE教程.assets/Snipaste_2025-04-28_11-12-01.jpg) |                                                       |



```assembly
[ENABLE]
alloc(newmem,2048,"gtutorial-x86_64.exe"+3F497) 
label(returnhere)
label(originalcode)
label(exit)

//自定义额外伤害的符号
alloc(Extra_Damage,4,"gtutorial-x86_64.exe"+3F497)
registerSymbol(Extra_Damage)

newmem:
originalcode:
//mov [rdx+70],eax 原代码
//mov rax,[rbp-10] 原代码

sub eax,45    //攻击增加45伤害

//分析：敌人最大血量100，[rdx+70]血量，eax新的血量
mov [rdx+70],eax
mov rax,[rbp-10]


exit:
jmp returnhere

"gtutorial-x86_64.exe"+3F497:
jmp newmem
nop 2
returnhere:
 
[DISABLE]
dealloc(*)
unregisterSymbol(*)

dealloc(newmem)
"gtutorial-x86_64.exe"+3F497:
mov [rdx+70],eax
mov rax,[rbp-10]
```

### step2

[Tutorial Games](https://www.52pojie.cn/thread-915447-1-1.html)	 [游戏step2](https://blog.csdn.net/qq_39580609/article/details/129188321)	 [游戏](https://blog.csdn.net/kinghzking/article/details/130074260) 	[Step 2](https://www.bilibili.com/opus/392192357361215271)	[游戏](https://blog.csdn.net/peng1874/article/details/107453166)	

==代码共享==： 敌人和玩家相关联，“共用代码”（Shared Code），敌人和我们减血的代码是共用的

前面章节有

## Tutorial

[Cheat Engine 教程（ 1 - 9 通关 ）](https://blog.csdn.net/freeking101/article/details/101107489)	 [Tutorial实战 ](https://www.bilibili.com/opus/557055321270157326)	[使用CE查找指针](https://blog.csdn.net/czkct/article/details/82251111)	

[Cheat Engine7.4 训练教程](https://blog.csdn.net/qiuqiuit/article/details/128732599)	 [heat Engine Tutorial](https://www.bilibili.com/opus/557055321270157326)	

- 扫描`双浮点数`类型建议禁用 "快速扫描"

第2关：健康

```assembly
[ENABLE]
alloc(newmem,2048,"Tutorial-i386.exe"+25AEF)
label(returnhere)
label(originalcode)
label(exit)

//自定义额外伤害的符号
alloc(Extra_Damage,4,"Tutorial-i386.exe"+25AEF)
registerSymbol(Extra_Damage)

newmem:
originalcode:

//sub [ebx+000004B0],eax   原汇编指令

//我们的指令：start
//要用到rcx，所以原数据先暂存到stack
push rcx

mov ecx,dword [ebx+000004B0]
add [ebx+000004B0],ecx

pop rcx
//我们的指令：end


exit:
jmp returnhere

"Tutorial-i386.exe"+25AEF:
jmp newmem
nop
returnhere:
 
 
[DISABLE]
dealloc(*)
unregisterSymbol(*)
//作弊列表中，勾上并取消时，DISABLE下面的代码就执行
//释放内存，操作码还原

dealloc(newmem)
"Tutorial-i386.exe"+25AEF:
sub [ebx+000004B0],eax
```



### 5代码查找

某些游戏重新开始时，==数据会存储在与上次不同的地方==, 甚至游戏的过程中数据的存储位置也会变动。

数值每次启动时都会存放在内存不同的位置，所以ce地址列表中的固定地址是不起作用的

1. 先找到这个数值当前的存储地址
2. 右健选择"找出是什么改写了这个地址"
3. 选中代码并点击"替换"按钮，将它替换成什么也不做的代码（空指令）

### 6指针

就是前面章节的 `指针路径` 

"代码查找"对付变化位置的数据地址，往往不能达到预期的效果，需要学习如何利用指针

在本关的 Tutorial.exe 窗口下面有两个按钮，一个会改变数值，另一个不但能改变数值而且还会`改变数值在内存中存储的位置`。

### 7代码注入
