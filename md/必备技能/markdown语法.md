[微信 Markdown 编辑器](https://md.doocs.org/)	[WeChat Markdown Editor：微信Markdown编辑器](https://www.ahhhhfs.com/69322/)	

[Jekyll-yaml front matter](https://blog.csdn.net/FeeLang/article/details/127015390) [YAML front matter ——Obsidian](https://zhuanlan.zhihu.com/p/599096662) [YAML Front Matter](https://www.cnblogs.com/kaiye/archive/2013/04/24/3039346.html) [YAML 与 front-matter](https://www.cnblogs.com/mtcnn/p/9421015.html?ivk_sa=1024320u) 

[Typora 的 Markdown 语法](https://support.typoraio.cn/zh/Markdown-Reference/) [Typora Support](https://support.typoraio.cn/YAML/)

[obsidian](https://www.bilibili.com/video/BV1YB4y1q7PG/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd) [Hexo](https://www.bilibili.com/video/BV1Gt411z78z/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd) [在Markdown中处理纯文本属性与元数据](https://www.bilibili.com/video/BV1tN4y1m7hU/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd) 

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
