[微信 Markdown 编辑器](https://md.doocs.org/)	[WeChat Markdown Editor：微信Markdown编辑器](https://www.ahhhhfs.com/69322/)	

[Jekyll-yaml front matter](https://blog.csdn.net/FeeLang/article/details/127015390) [YAML front matter ——Obsidian](https://zhuanlan.zhihu.com/p/599096662) [YAML Front Matter](https://www.cnblogs.com/kaiye/archive/2013/04/24/3039346.html) [YAML 与 front-matter](https://www.cnblogs.com/mtcnn/p/9421015.html?ivk_sa=1024320u) 

[Typora 的 Markdown 语法](https://support.typoraio.cn/zh/Markdown-Reference/) [Typora Support](https://support.typoraio.cn/YAML/)

[obsidian](https://www.bilibili.com/video/BV1YB4y1q7PG/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd) [Hexo](https://www.bilibili.com/video/BV1Gt411z78z/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd) [在Markdown中处理纯文本属性与元数据](https://www.bilibili.com/video/BV1tN4y1m7hU/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd) 

[教你解锁Markdown高级用法](https://juejin.cn/post/7109762042147373063)  

Typora破解：

[2022年最新Typora的破解方法](https://www.jb51.net/article/262499.htm)   [Typora 授权解密与剖析](https://www.52pojie.cn/forum.php?mod=viewthread&tid=1553967)

typora+图床：[ Typora+PicGo图床配置](https://blog.csdn.net/weixin_50839420/article/details/123227203?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2~default~CTRLIST~Rate-1-123227203-blog-126279327.pc_relevant_multi_platform_whitelistv4&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2~default~CTRLIST~Rate-1-123227203-blog-126279327.pc_relevant_multi_platform_whitelistv4&utm_relevant_index=1) [优质图床](https://zhuanlan.zhihu.com/p/403554101)  [Markdown添加图床](https://zhuanlan.zhihu.com/p/110008873)  [pexels.com](https://www.pexels.com/search/beautiful girl/)

typora：[Typora字体颜色设置的3种方案](https://blog.csdn.net/liulei952413829/article/details/114670380?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-0-114670380-blog-125280276.pc_relevant_3mothn_strategy_and_data_recovery&spm=1001.2101.3001.4242.1&utm_relevant_index=3)  [autohotkey换颜色](https://blog.csdn.net/qq_37759113/article/details/125280276)  [AutoHotkey](https://blog.csdn.net/Netceor/article/details/119811861?spm=1001.2101.3001.6650.3&utm_medium=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-3-119811861-blog-125280276.pc_relevant_3mothn_strategy_and_data_recovery&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-3-119811861-blog-125280276.pc_relevant_3mothn_strategy_and_data_recovery&utm_relevant_index=6)  

autohotkey参考手册：[官方文档](https://wyagd001.github.io/zh-cn/docs/AutoHotkey.htm) [AutoHotkey中文手册](https://ahkcn.sourceforge.net/docs/AutoHotkey.htm) [autohotkey参考](https://www.jianshu.com/p/b430f59387e8)  [AutoHotkey 快速入门](https://www.bilibili.com/video/BV1Xk4y1q7EL/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd)  [AutoGUI来学习AutoHotkey](https://www.bilibili.com/video/BV1mU4y1A7FE/?spm_id_from=333.788.recommend_more_video.7&vd_source=7346303e5e18677d7261c2c0c109ecfd) [AutoAHK中文社区](https://www.autoahk.com/) [安装后文件说明](https://www.bilibili.com/video/BV1Z741177j8/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd) [autoit脚本编程办公自动化](https://www.bilibili.com/video/BV127411F75C/?spm_id_from=333.788.recommend_more_video.10&vd_source=7346303e5e18677d7261c2c0c109ecfd)  [河许人](https://space.bilibili.com/38020172/video) 

> 1. 基础
>    1. ; 注释	 win = #   ahk与窗口相关的命令大多win开头	Ctrl = ^	Alt = !	Shift = +	转义：反引号     逗号分隔命令不同参数
>    2. 运行程序: Run,{路径}\xx.exe           发送确认键(Enter)：Send,{ENTER}
>    3. 下一步（确认键）：Send,{ALTDOWN}n{ALTUP}         [下一步的快捷键是alt+n 所以点击alt+n再放开]
>    4. 打印特殊字符：比如感叹号,感叹号本身以及代表了Alt按键, 要打印感叹号可以这样: {raw}!
>    5. 热键 ^+1::            热字串hotstring  `::kiss::haha`输入kiss后按tab，kiss被替换成haha
> 2. 鼠标
>    1. ~LButton & WheelUP::        波浪符～代表当用左键作热键时，ahk不会屏蔽它本身功能(这样鼠标左键不会失效)
> 3. 文本替换
>    1. ::tt::
>       clipboard=这是要代替的内容
>       send ^v
>       return
> 4. 自动登录
>    1. ::cuser::
>       send username
>       send {tab}
>       send password{raw}!
>       send {enter}
>       return
> 5. 



图书

[github.com](https://github.com/lTbgykio/Books-Free-Books)

[typora自动排序标题](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=typora自动排序标题&rn=20&oq=typora%E6%9C%89%E5%BA%8F%E5%88%97%E8%A1%A8%E4%B8%8D%E8%83%BD%E7%94%A8%E6%A0%87%E9%A2%98&rsv_pq=a4deac6800080566&rsv_t=b9cbow%2F3DSnpxddfRTPUPYtgeoyGrHhkEupCLhR8RMdY9fQp%2BLS3F6yUt6w&rqlang=cn&rsv_enter=1&rsv_dl=tb&rsv_sug3=27&rsv_sug1=9&rsv_sug7=100&rsv_sug2=0&rsv_btype=t&inputT=9056&rsv_sug4=158662) [Typora 标题的自动编号](https://blog.51cto.com/u_2930144/3864611) [typora设置标题自动编号](https://blog.csdn.net/juluwangriyue/article/details/125467325) [Typora自动排序的标题](https://blog.csdn.net/cw616729/article/details/108877240) [Typora 设置标题自动编号](https://blog.csdn.net/u012318074/article/details/123948859) [Hexo + Butterfly 从零开始搭建个人博客](https://blog.csdn.net/qq_41356250/article/details/125830994)

# LaTeX

[Equation Editor for online mathematics - create, integrate and download](https://editor.codecogs.com/)	

[数学公式_全部_第1页 - LaTeX工作室](https://wenda.latexstudio.net/c-11)	[数学公式识别神器—Mathpix Snip - 知乎](https://zhuanlan.zhihu.com/p/63918634)	[MathType中文网站-MathType数学公式编辑器下载,MathType教程](https://www.mathtype.cn/)	[使用Markdown输出LaTex数学公式 - 知乎](https://zhuanlan.zhihu.com/p/59412540)	

[在线LaTeX公式编辑器-编辑器](https://www.latexlive.com/##)	[LatexEasy | 在线Latex数学公式编辑和渲染](https://latexeasy.com/zh)	



# 变量

系统变量 %CD%,set设置变量  

# 字符串操作

```
截取：echo %var:~n,k%  例：%str:~0,5%  	替换：%var:old_str=new_str%  例：%str:hello=good%
```

# dos命令

[重定向操作符](https://blog.csdn.net/noter16/article/details/52680101) [批处理延迟变量!var!](https://blog.csdn.net/zhangyang0402/article/details/4849053) [批处理之家 ](http://bbs.bathome.net/thread-39-1-1.html)   中国DOS联盟

```
批处理中的转义字符 ^
rem 注释符，也可以用两个冒号代替(::)
start 		启动一个单独的窗口以运行指定的程序或命令，程序继续向下执行。
errorlevel	程序执行结果返回码，执行成功返回0，失败返回为1
copy		文件复制	xcopy	目录复制
copy temp1 d:\temp2 /s /e /y 将temp1目录下的文件复制到temp2目录，包括temp1子目录下的文件
cd /d d:\temp1 切换到temp1目录，当前目录非d盘
rmdir d:\temp1 /s /q 删除temp1目录，包括子目录(/s)，并且删除时不提示(/q)

goto 跳到指定的标号(标号用:后跟标准字符串来定义)处，goto语句一般与if配合使用，根据不同的条件来执行不同的命令组。goto end         :end 

&  顺序执行多条命令，而不管命令是否执行成功  
&& 顺序执行多条命令，当碰到执行出错的命令后将不执行后面的命令
|| 顺序执行多条命令，当碰到执行正确的命令后将不执行后面的命令

> 清除文件中原有的内容后再写入
type nul > file1.txt #创建文件   <	从文件中而不是从键盘中输入
>>	将命令输出添加到文件末尾而不删除文件中的信息。
>&	将一个句柄的输出写入到另一个句柄的输入中。
<&	从一个句柄读取输入并将其写入到另一个句柄输出中, 重定向输入和复制， 例：句柄 2（即 STDERR）重定向到句柄 1（即 STDOUT） 1<&2
cmd > file 2>&1 把 stdout 和 stderr 一起重定向到 file 文件中
```

## 条件语句if/else

```
IF [NOT] ERRORLEVEL number command     最后运行的程序返回一个等于或大于指定数字的退出代码，指定条件为 true
IF [NOT] string1==string2 command      字符串匹配，指定条件为 true
IF [NOT] EXIST filename command        文件名存在，指定条件为 true

如果命令扩展被启用，IF 会如下改变:
IF [/I] string1 compare-op string2 command    /I 说明要进行的字符串比较不分大小写。
IF CMDEXTVERSION number command
IF DEFINED variable command

IF EXIST filename. (del filename.) ELSE echo filename. missing
```



## for语句

[批处理之 for/f 详解](http://blog.sina.com.cn/s/blog_6a7839530102uweu.html)   [bat脚本基础教程](https://www.cnblogs.com/linyfeng/p/8072002.html)

 [FOR参数/F之tokens详解](http://blog.sina.com.cn/s/blog_6a7839530102uvx8.html)  [BAT脚本编写](https://www.jb51.net/article/49627.htm)


```
FOR %variable IN (set) DO command [command-parameters]   4个参数: /d /r /l /f,批处理脚本中使用%%variable,(set)  指定一个或一组文件。可以使用通配符。
1. /d:打印C盘根目录下的目录名:for /d %%i in (c:/*) do (echo %%i)
2. /r:递归查询指定目录下的匹配文件。默认当前目录,打印D盘目录及子目录下的后缀为.txt和.py的文件:
	  for /r d:/temp %%i in ( *.txt *.py ) do (echo %%i)
3. /l:以增量形式从开始到结束的一个数字序列,打印10以内的奇数:for /l %i in (1,2,10) do (echo %i)
```

```
4. /f:一句话总结：提取列。通俗讲，共同提取每一行的第m小节的内容，因此，可以用该命令来指定提取文本信息。FOR %variable IN (set) DO command [command-parameters]
  FOR /F ["options"] %variable IN (file-set) DO command [command-parameters]
  FOR /F ["options"] %variable IN ("string") DO command [command-parameters]
  FOR /F ["options"] %variable IN ('command') DO command [command-parameters]

for /F "skip=4 eol=;  tokens=1,3* delims=,- " %%i in (temp.txt) do (  echo  i=%%i, j=%%j, k=%%k)
for /f "delims=" %%i in ('dir /a /b /on %WORK_DIR%\*.txt') do ( echo %%i) 
	tokens=有时表示提取全部。
	tokens=m表示提取第m列。
	tokens=m,n表示提取第m列和第n列。
	tokens=m-n表示提取第m列至第n列。
	Tokens=*表示删除每行前面的空格。忽略行首的所有空格。
	tokens=m*提取第m列以后的所有字符，星号表示剩余的字符。
	tokens=m,*提取第m列以后的所有字符，星号表示剩余的字符。
	输出变量的个数由定义了的tokens决定。
	在 FOR 语句中显式声明 %%i。使用tokens= 隐式声明%%j 和%%k。只要不会引起试图声明高于字母“z”或“Z”的某个变量，则使用tokens= 可以指定最多 26 个输出变量。
```

## 例子

[生成速查手册.bat](https://gitee.com/haujet/windows-batch-script/blob/master/生成速查手册.bat)

[解决.md文档传输丢图片的方法](https://blog.csdn.net/Origamitnl/article/details/126310777?spm=1001.2101.3001.6650.11&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-11-126310777-blog-142566935.235%5Ev43%5Epc_blog_bottom_relevance_base4)	

# cnblogs模板修改

[美化博客园](https://www.cnblogs.com/suanai/p/14495886.html)	

[修改CnBlogs博客园主题模板](https://blog.csdn.net/weixin_30872337/article/details/98443442)	

[博客园自定义鼠标美化](https://www.cnblogs.com/yyyzyyyz/p/15383875.html)	 [cnblog-mouse_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=cnblog-mouse)	

好的模板： [外部DirectX绘制实现 - lyshark](https://www.cnblogs.com/LyShark/p/17761931.html)	 
