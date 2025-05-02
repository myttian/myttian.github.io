### 一、Linux

[安装CentOS7.9](https://www.bilibili.com/video/BV1a34y1s7Ja?spm_id_from=333.337.search-card.all.click)  [老男孩Linux初级运维教程](https://www.bilibili.com/video/BV1rJ411M7S1?p=6&spm_id_from=pageDriver)  [birtney - 博客园 ](https://www.cnblogs.com/birtney/)    [黑科技还得谷歌 ](https://www.163.com/dy/article/H75V4HRA0511DSSR.html?clickfrom=w_tech) [下一代监控：Prometheus ](https://baijiahao.baidu.com/s?id=1689945188583938997&wfr=spider&for=pc) [prometheus](https://blog.csdn.net/youmatterhsp/article/details/106792059?spm=1001.2014.3001.5502)  [ XShell破解版](https://www.cnblogs.com/bowendown/p/11937159.html)  [ xshell无法启动无法](https://blog.csdn.net/qq_34231823/article/details/120260491) 关FlexNet Licensiing service服务   [Beyond Compare 使用笔记](https://www.cnblogs.com/xjnotxj/p/12890957.html)

[linux软件包管理](https://zhuanlan.zhihu.com/p/374502538)   [Linux 包管理基础：apt、yum、dnf 和 pkg](https://linux.cn/article-8782-1.html)  [APT、apt-get、apt-cache  ](https://juejin.cn/post/7028510908175351816)  [技术|Linux 包管理基础：apt、yum、dnf 和 pkg](https://linux.cn/article-8782-1.html)   [Linux包管理 ](https://www.cnblogs.com/chaoge-666/p/15459918.html)  [yum软件包组 ](http://c.biancheng.net/view/826.html) [linux yum](https://bbs.huaweicloud.com/blogs/302732)  [yum 软件组（grouplist）](http://www.w3capi.com/mcms/content/id/91/cid/26.html) [Linux 目录结构 ](https://www.runoob.com/linux/linux-system-contents.html)[跟老男孩学LINUX运维 核心基础篇](http://www.java1234.com/a/javabook/javabase/2020/1217/18598.html)   

[yum源中$releasever不能被系统识别 ](https://www.jianshu.com/p/925960eaeb21)  [yum组管理](https://blog.csdn.net/baidu_41388533/article/details/107761343)   [yum 命令详解](https://www.jianshu.com/p/a258ebd0df94)   [yum缓存](https://blog.51cto.com/lvwencheng/845237)

yum源配置：[Centos7 中修改yum源（三种方法）](https://www.cnblogs.com/jiufang/p/13043103.html) [安装dnf](https://segmentfault.com/a/1190000041468762)  [阿里镜像站](https://developer.aliyun.com/mirror/?spm=a2c6h.25603864.0.0.51ce4ccathzRGp)

EPEL源：[epel镜像阿里](https://developer.aliyun.com/mirror/epel?spm=a2c6h.13651102.0.0.2d101b11Xme5KR) 

 DNF：[Centos7 python ascii编码错误解决](https://www.jianshu.com/p/8514de2b1edc)  [CentOS 7中的系统语言包及UTF-8、en_US.UTF-8和zh_CN.UTF-8](https://www.cnblogs.com/guanbin-529/p/12846345.html)   [dnf管理RPM包 ](https://segmentfault.com/a/1190000041468762)  [中文乱码:en_US.utf8](https://www.jianshu.com/p/5d4ce368a411)
```bash
1. 下载repo 到/etc/yum.repos.d/    #yum配置文件/etc/yum.conf
2. 安装dnf yum install dnf       //安装后python ascii编码错误解决 LANG=en_US   /etc/locale.conf LANG="en_US.UTF-8"
```

```
yum [options][cmd][package...]    install、update、erase(remove是它别名)、search查找
check-update：列出可更新包； list列出可安装软件； info包信息、history、deplist:列出软件的依赖； distribution-synchronization安装的包更新到最新；yum help list；provides包提供者、
repolist列出可用库；repo-pkgs、upgrade只升级包，不升软件和内核

清缓存：
yum clean package:清缓存目录下的软件包；clean headers：清目录下的headers；oldheaders清旧的headers
yum clean,yum clean all等于packages+oldheaders(清包和旧headers)


禁用库：
1、临时：yum update --disablerepo=remi-safe；多个库用逗号，yum --disablerepo=remi-safe,updates install httpd； yum --disablerepo=* --enablerepo=epel update 只更新epel； yum install nginx --enablerepo=epel安装软件指定 repo
2、改配置/etc/yum.repos.d/；enabled=1 打开

组管理:
grouplist； groupinfo查组内包含的软件；groupinstall、groupremove
```

```
默认情况下，yum客户端在成功下载和安装软包后会把下载的文件删掉而不进行缓存。这样可以减少磁盘空间的占用。需要时可以启用缓存功能，这样yum可以将rpm数据缓存到YUM的缓存目录中。
缓存的好处：提高YUM的性能；可以离线运行YUM操作，只使用缓存；也可以复制缓存中的软件包以备用。

存放下载的软件包、仓库信息等数据:/var/cache/yum/$basearch/$releasever; 打开缓存后，每个yum操作都可从仓库下载软件包数据。启用cache: /etc/yum.conf中的keepcache=1
```

```
repo配置文件：baseurl:仓库位置;enabled 1开启；gpgcheck检查签名；gpgkey 签名认证信息的路径
```

学习方法：设定目标、寻找方法、勤奋努力、坚持不懈

EmEditor   Beyond-Compare(比较)    linux比较：diff  vimdiff

##### 1.编译_包管理
```bash
1. *.gz 大多数压缩工具只能针对单一文件操作，压缩目录时用tar将目录内的多个文件打包成一个文件，再压缩.  tar打包的称为源码包，一般包含有，程序源代码文件，配置文件（configure），安装使用说明（INSTALL,HOWTO,README）
安装：解压=>安装要求=>gcc编译，生成二进制=>将二进制文件安装到主机

2. 源码包麻烦，linux厂商推出类似windows的安装方式，直接在已知的系统中编译好，使用者可以直接下载并进行安装，升级，卸载等操作； 
    RPM（RedHat Package Manager）:提前编译，打包，然后在rpm包里面存放了用以记录软件依赖关系的相关数据，当用户安装时，优先查看这些数据，如果系统满足数据	要求就安装软件包，否则不能安装，安装完成后，将软件包相关信息记录到rpm自己的数据库中，便于查询和卸载等。所以说rpm的优点是方便安装，卸载，查询，缺点就是     只能在指定的操作系统上使用，所以不同厂商的rpm包，甚至同一厂商不同版本操作系统的rpm包都不通用。rpm包命名： Cython-0.19-5.el7.x86_64.rpm
    dhcp-server-	4.3.6  -30		.el8	   .x86_64   .rpm
    软件名称		 版本	  编译次数	适用的系统  适用的平台  后缀名

	rpm包的相关文件一般都会放在对应的目录中，比如rpm包安装后，配置文件会放在/etc下，执行文件会放在/usr/bin下，链接库文件会放在/usr/lib下，帮助与说明文	  档会放在/usr/share/man和/usr/share/doc目录下

dpkg(Debian Packager):

3. YUM（Yellow dog Updater, Modified）基于rpm却更胜于rpm的管理工具； 自动解决软件间的依赖问题。
	YUM缓存：YUM运行时，会从YUM下载源获得软件信息与文件，并且暂存于本机的硬盘上。这个暂存的目录，称为“YUM缓存（YUM cache）”。缓存目录为/var/cache/yum

4. DNF是新一代的rpm软件包管理器。最早出现在 Fedora 18 这个发行版中，在Fedora 22中正式取代了yum
    /etc/dnf/dnf.conf 配置文件
    /etc/dnf/aliases.d/ 为相关命令定义别名的如dnf alias add rm=remove
    /etc/dnf/modules.d&/etc/dnf/modules.defaults.d 模块的设置
    /etc/dnf/plugins/ 插件的设置
    /etc/dnf/protected.d/ 受保护的软件包的设置
    /etc/dnf/vars/ 变量设置
```

**源码编译**

> 然后必须获取到该软件需要的编译工具，并依据编译工具进行对应操作（以 GNU 编译工具为例）：
>
> 1. 找到 `configure` 脚本文件并运行，以确认在当前系统环境下软件可以成功编译（例如确认系统已安装所需依赖）
> 2. `configure` 脚本运行成功后，将产生对应本系统的 `Makefile` 文件，该文件中包含在本系统编译整个软件所需的指令
> 3. 接下来需要使用工具 `make`，它将按照 `Makefile` 文件的指示，主导软件的编译过程
> 4. 在软件编译成功后使用 `make install` 来进行最终的安装
>
> <font color=#0099ff>然而上述操作仅仅是基础流程，在实际的编译过程中还会涉及到许多问题，例如软件安装位置的选择（该软件是某一用户专用，还是所有用户都需要使用？），软件编译的具体配置（通过不同编译配置可以对得到的软件进行自定义），更不要说噩梦般的软件依赖处理（需要先找到本软件依赖软件的源代码，并先对依赖软件完成编译安装，还得小心依赖冲突）。</font>

##### 2.VI

[vi设置行号](https://www.cnblogs.com/ggzhangxiaochao/p/10773712.html)

```
/etc/vimrc   是系统范围的初始化配置
～/.vimrc     个人的vim初始化配置
```
```bash
1. HLM（当前页)   G gg 10G(10行)     0 $ ^非空格 d$ d0  y$ y0    
x(del) dd(剪切行) yy复制行  p   dG删光标到最后 d1G  yG y1G
u复原 ^+r重做  .重复前一个动作   光标右移n空格  下移n回车
>缩进 ^+e,y上下滚动，w,b,e行内单词  f行内查找  ，反向查找     zz滚动中间   zt  zb  

下搜 /   上搜?        :n1,n2s/word1/word2/g  (n1、n2 行之间查找word1替换为word2)   1,$(第一到最后一行) 或 用%
:10,20s/^/#/g (10-20行加#注释符) :10,20s/^#//g (删除)  	//:起始行号,结束行号s/^/注释符/g
:10,20s#^#//#g (10-20行加//注释符) :10,20s#^//##g (删除)   //:起始行号,结束行号s/^注释符//g
批量注释：^+v块，移动光标选行，大写I行首插入//，esc退出块  

2.i光标处 a下一字符 o下一行  r取代一次 
3.w q wq  ZZ保存退出 ZQ不保存强退
```

```
cat\grep过滤空行、注释行：cat /etc/1.conf | grep -Ev '^$|#'  #v不匹配行，E扩展正则语法 $vi里是行尾，是空行，^$就是不是行尾但是是空行。
grep -Ev  '^$|#' /etc/1.conf;     grep -v "^#" /etc/1.conf | grep -v "^$"
```



##### 3.命令 重定向   文件描述符

[curl下载](https://www.cnblogs.com/rumenz/articles/15430995.html) [sed](https://www.cnblogs.com/skaarl/p/14668954.html) [ls](https://www.cnblogs.com/weq0805/p/14873267.html)  [ls](https://www.modb.pro/db/99173) [wc](https://www.runoob.com/linux/linux-comm-wc.html)  [lsof](http://blog.itpub.net/31397003/viewspace-2147485) [lsof详解](http://t.zoukankan.com/igoodful-p-11661883.html)  [netstat、lsof、ps](https://blog.csdn.net/weixin_52109884/article/details/121172446?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_title~default-0-121172446-blog-116157567.pc_relevant_antiscanv2&spm=1001.2101.3001.4242.1&utm_relevant_index=3) [grep](https://m.runoob.com/linux/linux-comm-grep.html) [awk](https://m.runoob.com/linux/linux-comm-awk.html) [awk](https://blog.csdn.net/anqixiang/article/details/117903529)  [sed](https://www.cnblogs.com/liwei0526vip/p/5644163.html)  [find](https://www.cnblogs.com/klelee/p/15759037.html)   [exec](https://www.jianshu.com/p/1f0437bb8b55)  [exec](https://www.cnblogs.com/JIKes/p/15331269.html)   [ulimit](https://www.cnblogs.com/wangkangluo1/archive/2012/06/06/2537677.html)   [sed](https://www.cnblogs.com/liwei0526vip/p/5644163.html)  [Linux查找文件](https://www.cnblogs.com/novae/p/15502230.html)  [ man](http://c.biancheng.net/view/766.html)  [man结构](https://blog.csdn.net/weixin_42430824/article/details/81019155)  [man详解](https://www.cnblogs.com/DataArt/p/10010673.html)  [高效地使用 man 页 ](https://linux.cn/article-9165-1.html) [grep详解](https://blog.csdn.net/llljjlj/article/details/89810340)

[sed 菜鸟教程](https://www.runoob.com/linux/linux-comm-sed.html)  [more](https://www.runoob.com/linux/linux-comm-more.html)  [history](https://www.jianshu.com/p/7ecd5ff9e5dd)  [history](https://www.cnblogs.com/ifme/p/12365394.html)   [history](https://blog.csdn.net/weixin_31642733/article/details/116908568)  [man](https://www.cnblogs.com/webnote/p/5734586.html)  [常用命令](https://www.cnblogs.com/xiongyi1/p/14085963.html)  [别名](https://blog.csdn.net/weixin_42410658/article/details/123932066)  [ls ](https://www.cnblogs.com/wodiaonimade/p/12027698.html)  [xargs](https://www.cnblogs.com/lidabo/p/15662869.html)  [xargs](https://www.runoob.com/linux/linux-comm-xargs.html) [cat创建文件](https://wenku.baidu.com/view/137b5f376f175f0e7cd184254b35eefdc9d3154c.html)  [cut](https://www.runoob.com/linux/linux-comm-cut.html) [cut](https://blog.csdn.net/weixin_45842494/article/details/124679008)

```bash
man mkdir | less +/-m   #跳过-m 之前的内容，       &bind 只显示匹配行
man mkdir | grep -- '-m'         man mkdir | grep -e '-m'  #mkdir中的 -m含义
chown -R root.root /share #改文件用户和组    chmod 777 /share #改用户权限
查找配置文件：rpm -ql rsync | grep etc      rpm -qc  rsync
```



```bash
磁盘管理：df -ahTi   du   fdisk -l; chown 改所属用户和组，chmod 用户权限
ll; sz rz(文件从srv下到本地)； ll |grep ^d  /$ 只看目录，-i不分大小写，^ $正则用法，行首 -e    ls -F -p   ls -lrt最新文件在下面 r倒序 t时间排序  more时h显示帮助  ls -ld   rm -f
alias ll='ls -l --color=tty'
文本分析awk [选项] '条件{动作}'  文件名    sed后接动作加单引号，搜索关键字/ /括起来 sed -n '/^d/p'  p打印  ^d开头是d
egrep 等同 grep -E 用正则   haead -n 查看文件前n行  tail -fF后
curl -o /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-7.repo
rpm -qa | grep sys 查看    yum groupinstall "Development Tools"
which ls查看命令路径   字符集乱码转换: iconv  
wc(计算字数)  lsof获取打开文件信息  lsof -a -p $$ -d0,1,2
locate [选择参数] [样式]			find [路径][选项][内容]
find / -iname  profile    find /dev -type b -exec ls -l {} \;   -exec将前一个命令得到的结果传递给下一条命令作为参数; 前面命令的查找结果，输出到{}的位置，作为后边命令的参数，而\;是转义了一个分号表示语句结束，使用反斜杠是因为分号在bash语句中有特殊的用途;
nl输出加编号 cd -回上次目录     cat -n  less -N   grep -n ^d               
chattr锁定文件 lsattr查看锁定文件 tr替换  
chkconfig     tree -L 1 /   显示/目录下1级目录
free查内存   
执行历史!n  !!前一个命令 !string  ^+p调出命令  ^+r搜索 ^+g退出 esc.前个命令!$ !-2倒数第2
history -c清空   command !^ !$  !*  !:n第n个参数 
cat /etc/redhat-release   内核uname -r  -m -n   last w who lastlog
cat>11 ^+d结束  cat>11<<EOF  结束符用EOF
cut -d ' ' -f 1 cut.txt   "里面空格分隔" -f 取第几列   -b字节为单位分隔  -c字为单位  awk
单引号原样输出echo '$PATH'    双引号：显示内容    netstat -lnt|grep 873检查端口 反查端口干嘛的lsof -i tcp:873
```

```bash
man结构：name、synopsis参数大致使用方法、description、examples、overview概述、defaults默认功能、options可用选项、environment环境变量、files用到的文件、see also相关、history维护历史；  
&bind 无需使用 n 和 SHIFT+n 来滚动到下一个/上一个匹配的位置。& 模式只会显示那些包含搜索内容的行，其他的内容全都被省略掉

man 有不同帮助级别；man -f  man 1 passwd；  -k 査看命令名中包含指定字符串的所有相关命令的帮助；whatis作用与man -f一致； apropos与man- k一致；   -w 帮助文件路径；
想知道命令是干什么的whatis ；想知道命令在哪里whereis；想知道当前登录用户是谁 whoami 。
```

[加大文件描述符FD ](https://baijiahao.baidu.com/s?id=1659479624291885631&wfr=spider&for=pc)   ：高效管理已打开文件所创建的索引  ulimit -n    [重定向 ](https://www.runoob.com/linux/linux-shell-io-redirections.html) [Linux重定向](https://www.cnblogs.com/qinghuani/p/15024730.html) [文件描述符](http://c.biancheng.net/view/3066.html)  [文件描述符 ](https://www.cnblogs.com/tz90/p/13528174.html) 

```bash
1. >出   <入   >>追加     command1 < file > outfile //执行命令，从file读内容；输出到outfile文件   stdin和out都重定向；  find . -type d 当前目录类型为目录的文件 .当前目录
文件描述符 0 通常是标准输入（STDIN），1 是标准输出（STDOUT），2 是标准错误输出（STDERR）
command 2>file  	//stderr重定向到file

command > file 2>&1 //err合并到out后，重定向到file;   >&是赋值后描述符的输出属性
执行命令，但不希望显示输出结果，可以将输出重定向到 /dev/null; 
/dev/null写入到它的内容都会被丢弃；如果尝试从该文件读取内容，那么什么也读不到;
将命令的输出重定向到它，会起到"禁止输出"的效果;  屏蔽 stdout 和 stderr  2>&1

2. Here Document，SHELL中的特殊重定向， EOF(End Of File);  EOF中的内容作为输入传给command
3. 执行命令，但不在屏幕输出，重定向到 /dev/null:  command > /dev/null
```



##### 4.目录

[linux系统文件](https://blog.csdn.net/youmatterhsp/article/details/80010468)    [Linux文件系统与目录结构详解](https://www.oldboyedu.com/blog/3615.html) [目录结构 ](https://blog.csdn.net/youmatterhsp/article/details/79964675) [Systemd入门](https://www.linuxprobe.com/systemd-command.html)  [Linux：FHS标准](https://www.cnblogs.com/happyframework/p/4480228.html) [FHS](https://blog.csdn.net/vic_qxz/article/details/80965660)  

```bash
/boot 100-200M,  swap内存1.5-2倍，内存大于16G，给8-16G；      ls -ld
1.opt(optional可选)，额外安装软件目录。比如你安装一个ORACLE数据库则就可以放到这个目录下。默认空。
2.proc(Processes进程)，管理内存空间；伪文件系统（也即虚拟文件系统）;存储的是当前内核运行状态,是一个虚拟目录，内存的映射，可以通过直接访问这个目录来获取系统信息。这个目录的内容不在硬盘上而是在内存里.
3.var变量，存经常被修改的目录，包括日志。
4.usr(unix shared resources共享资源),重要目录，用户的很多应用程序和文件都放在这个目录,类似program files
5.run临时文件系统，存储系统启动以来的信息。当系统重启时，这个目录下的文件应该被删掉或清除。如果你的系统上有 /var/run 目录，应该让它指向 run。
```

不同目录可对应不同磁盘，/test => /dev/sda2 

```bash
ll /dev/sda*   df -hiT显示挂载  mount /dev/sda1 /mnt 挂到mnt目录
系统目录启动时挂载：/etc/fstab       init启动进程，被systemd取代；
linux目录按类别组织，例如，可执行程序在/usr/bin； 配置和服务启动在/etc；数据和帮助在/usr/share
目录层级结构：FHS，定义2层规范，第一层定义'/'下目录放什么，第二层定义/usr和/var
```

```bash
重要的子目录：
/etc/sysconfig/network-scripts/ifcfg    配置ip及gw      /etc/resolv.conf 配置DNS      /etc/hosts
/etc/fstab  开机要mount的文件系统,目录挂载 etc/rc.local;     /etc/initab 设置启动runlevel
/etc/exports NFS配置文件  etc/xinit.d  如果服务器通过xinetd模式运行，它的脚本放在这个目录
/etc/issue  用户登录前显示信息     /etc/motd   用户登录提示
/etc/group  passwd etc/shadow密码  /etc/sudoers  /etc/syslog.conf日志配置   rsyslog.conf(C6.4)
/etc/login.defs登录缺省配置   /etc/securetty哪些终端能登root  /etc/modprobe.conf内核模块额外参数
/lib/modules 内核模块   /var/lib/rpm rpm套件安装处
/usr/local 自编译安装软件存放目录  /usr/local/bin    /usr/src内核源码存放目录

/var/log  /var/log/messages系统信息默认日志，非常重要，按周轮询   /var/log/secure登录信息  last w who lastlog
/var/log/wtmp 登录者信息  /var/spool /var/spool/cron/root 定时任务crontab默认目录
```

```
/etc/DIR_COLORS设颜色   /etc/protocols系统支持的协议  /etc/x11 x window配置
```



##### 5.环境变量

[Centos7 设置系统和用户环境变量](https://blog.csdn.net/hnjb5873/article/details/111034506)     [CentOS7环境变量](https://www.cnblogs.com/htlp/p/14906003.html) [centos7环境变量 ](https://www.cnblogs.com/soymilk2019/p/14985827.html)    [环境变量](https://blog.csdn.net/guyan0319/article/details/79542836)    [Centos7 设置环境变量](https://blog.csdn.net/hnjb5873/article/details/111034506)  [CentOS7环境变量](https://www.cnblogs.com/htlp/p/14906003.html) [环境变量](https://blog.csdn.net/guyan0319/article/details/79542836)  [source /etc/profile](https://blog.csdn.net/llzhang_fly/article/details/104980029)  

`/etc/profile   /etc/environment   ~/.bash_profile    /etc/bashrc`

> 1. 系统环境变量：三种方法，/etc/profile      /etc/profile.d            /etc/bashrc
>
>    1.  /etc/profile中设置
>
>       用户登录时执行/etc/profile文件中设置系统的环境变量。但是，Linux不建议在/etc/profile文件中设置系统环境变量。
>
>    2. /etc/profile.d目录中增加环境变量脚本文件，这是Linux推荐的方法。
>
>       /etc/profile在每次启动时会执行/etc/profile.d下全部的脚本文件。/etc/profile.d比/etc/profile好维护，不想要什么变量直接删除/etc/profile.d下对应的 shell 脚本即可。/etc/profile.d目录下有很多脚本文件。
>
>    3. /etc/bashrc中设置环境变量
>
>       该文件配置的环境变量将会影响全部用户使用的bash shell。但是，Linux也不建议在/etc/bashrc文件中设置系统环境变量。  每次新开一个shell，该文件就被读取
>
> 2. 用户环境变量，多种方法
>
>    1. bash_profile（推荐首选）；    用户主目录，有几个特别文件，ls看不见，用 ls .bash_* ；   echo "ls = 'ls  -F --color=auto'"  >> ~/.bash_profile
>       当用户登录时执行，每个用户都可以使用该文件来配置专属于自己的环境变量。
>    2. .bashrc
>       当用户登录时以及每次打开新的Shell时该文件都将被读取，不推荐在里面配置用户专用的环境变量，因为每开一个Shell，该文件都会被读取一次，效率肯定受影响。
>    3. .bash_logout
>       当每次退出系统（退出bash shell）时执行该文件。
>    4. .bash_history
>       保存了当前用户使用过的历史命令。
>
> 3. 环境变量脚本文件的执行顺序：
>    <font color=#0099ff>/etc/profile -> /etc/profile.d -> /etc/bashrc -> 用户的.bash_profile -> 用户的.bashrc</font>
>    同名的环境变量：如果多个脚本中有配置，以最后执行的脚本中的配置为准。在Shell下，export设置的环境变量对当前Shell立即生效，Shell退出后失效。
>    
> 4. /etc/environment设置整个系统的环境，而/etc/profile是设置所有用户的环境，前者与登录用户无关，后者与登录用户有关。
>    注：系统是先执行/etc/environment，再执行/etc/profile

```bash
export 变量名='值'    source变量生效或.  ..bash_profile    /etc/profile.d/
查看：env  echo $变量名  echo $PATH;    https://muma16fx.netlify.app
vi .bash_profile  :分隔
```

> 1、/etc/profile：是操作系统定制用户环境使用的第一个文件,此文件为系统的每个用户设置环境信息,当用户第一次登录时,该文件被执行。
>
> 2、/etc/environment：在登录时操作系统使用的第二个文件,系统在读取你自己的profile前,设置环境的变量。
>
> 3、~/.bash_profile：登录时用到的第三个文件是.profile文 件,     用户自定义的shell信息,   用 户登录时,该文件仅执行一次，默认情况下，设置一些环境变量，执 行用户的.bashrc文件。
> /etc/bashrc：为每一个运行bash shell的用户执行此文件.当bash shell被打开时,该文件被读取。
>
> 4、~/.bashrc:该文件包含专用于你的bash shell的bash信 息,当登录时以及每次打开新的shell时,该该文件被读取。

<font color=#0099ff>.bashrc相当于 shell 配置文件; 一般.bash_profile 中显式调用.bashrc。linux启动时首先读取 ~/.bash_profile,  这样 ~/.bashrc也得到执行;</font>

##### 6.优化_开机启动

###### a. System   V

  /etc/rc.d/rc[0-6]   软链接到  /etc/init.d          inittab设定运行级别runlevel  

[linux系统优化总结](https://www.cnblogs.com/lcrbg/p/5323100.html)[SELinux](https://blog.csdn.net/weixin_30279315/article/details/97605109)  [sed](https://www.cnblogs.com/skaarl/p/14668954.html) [关闭selinux,关闭firewalld 防火墙](https://zhuanlan.zhihu.com/p/414552638)  [centos7七个运行级别](https://www.cnblogs.com/renshengdezheli/p/13935307.html)  [chkconfig增加服务](http://www.ttlsa.com/linux-command/linux-chkconfig-1/) [chkconfig常用服务](https://www.cnblogs.com/xuey/p/7680623.html)  [centos脚本关开机服务](https://www.cnblogs.com/xhzj/p/14432205.html)  etc/rc.local    etc/init.d/iptables start   [p51内核优化](https://blog.51cto.com/oldboy/1184165)   p52优化总结  [linux系统基础调优32条技巧](https://blog.csdn.net/weixin_33843947/article/details/85023972?spm=1001.2101.3001.6650.19&utm_medium=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~default-19-85023972-blog-106628194.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~default-19-85023972-blog-106628194.pc_relevant_default&utm_relevant_index=25)  [linux系统基础调优](https://blog.csdn.net/suheng1/article/details/106628194)  [Linux系统调优基础 ](https://blog.51cto.com/sihua/1893019) [linux系统基础调优32条技巧](https://blog.51cto.com/oldboy/988726)    [一键系统优化15项脚本](https://www.cnblogs.com/nulige/p/6087638.html)  [shell脚本：一键优化centos系统](https://blog.51cto.com/mofansheng/1710247) 

```bash
1.关Selinux
sed -i 's#SELINUX=enforcing#SELINUX=disabled#g' /etc/selinux/config   //永久生效 i直接修改
sed [option] 'command' input_file   sed -i 's/line/text/g' test.txt #line替换text，s替换，g全局替换

setenforce 0 //临时关   查看：sestatus   getenforce
grep SELIN /etc/selinux/config   //看一眼文件里的参数
2.运行级别 cat /etc/inittab  systemctl set-default multi-user.target //默认3文本  init   systemctl get-default
3.精简开机服务  setup  ntsysv  脚本
chkconfig --list | grep 3:on //3级别on的
crond、network、sshd、syslog    
所有的优化都可以变为脚本：一键系统安装及优化脚本
```

```bash
chkconfig [--add][--del][--list][系统服务] 或 chkconfig [--level <等级代号>][系统服务][on/off/reset]
on指定服务启动，on\off只对运行级3，4，5有效；
level设置服务在指定运行级启动； chkconfig –level httpd 23 on  #httpd在2、3下都是on状态
```

```bash
增加一个服务：
1.服务脚本必须存放在/etc/ini.d/目录下；
2.chkconfig –add servicename；  然后在/etc/rc.d/rc5.d中可以看到链接。
在chkconfig工具服务列表中增加此服务，此时服务会被在/etc/rc.d/rcN.d中赋予K/S入口了；
```

```
service vsftpd start     和    /etc/init.d/vsftpd  start 都是启动服务
CentOS用Chkconfig配置，而Ubuntu用sysv-rc-conf配置
```

p51优化内核参数：/etc/sysctl.conf   sysctl -p配置生效

```
.bashrc相当于 shell 配置文件; 一般.bash_profile 中显式调用.bashrc。linux启动时首先读取 ~/.bash_profile,  这样 ~/.bashrc也得到执行;
```

[centos7启动流程导图](https://blog.csdn.net/qq_25518029/article/details/119904129)  [grub2的boot.img生成过程](https://blog.csdn.net/baidu_31504167/article/details/89136605)    [Inittab重要文件讲解及Linux启动过程](https://haokan.baidu.com/v?pd=wisenatural&vid=4193091067687245412)  [启动过程](https://max.book118.com/html/2021/1121/5132031203004114.shtm)   [Linux五大初始化](https://www.linuxprobe.com/five-modern-init-linux.html)  [五大初始化](http://www.techweb.com.cn/network/system/2016-12-21/2456104.shtml)  [CentOS 7 systemd取代System V init](https://blog.51cto.com/kusorz/1889886)     [服务优先级设置](https://blog.51cto.com/zhengdzy/2108879)     [grub2详解(翻译和整理官方手册) ](http://www.javashuo.com/article/p-tuyfivcl-cb.html)    [cpu实模式](https://baike.baidu.com/item/实模式/7354531?fr=aladdin) [深入浅出CPU的两种工作模式](https://baijiahao.baidu.com/s?id=1716199970322138603&wfr=spider&for=pc)  [CPU的实模式、保护模式和长模式](https://blog.csdn.net/xystrive/article/details/120722344)   [实模式，保护模式与长模式](https://blog.csdn.net/m0_57691497/article/details/120555753)  [上电reset信号给cpu](https://wenku.baidu.com/view/d1a9f483f624ccbff121dd36a32d7375a417c686.html)

 [硬盘拆解](https://www.meipian.cn/1s4jzwxt)  [磁头、磁道、扇区、柱面](https://blog.csdn.net/weixin_45142411/article/details/122984765)    [盘片、磁道、扇区、柱面](https://zhuanlan.zhihu.com/p/373313740)   [绝对/相对扇区](https://blog.csdn.net/ghostltc/article/details/1378942) [硬盘基础知识](https://blog.csdn.net/ghostltc/article/details/1378942)   [硬盘基本知识](https://wenku.baidu.com/view/c966427dbd23482fb4daa58da0116c175f0e1eb4.html)    [GRUB2启动和组成结构 ](https://wenku.baidu.com/view/d1a9f483f624ccbff121dd36a32d7375a417c686.html)   [GRUB2启动流程](https://blog.csdn.net/weixin_30418341/article/details/96701701)   [CentOS6启动导图](https://blog.csdn.net/qq_25518029/article/details/119905231)  [vmlinuz](https://baike.baidu.com/item/vmlinuz/4106145?fr=aladdin)   [KB和KiB](https://blog.csdn.net/weixin_45790919/article/details/112967713)    [制作BIOS+UEFI兼容的refind和grub2启动盘](https://www.jianshu.com/p/86cbb35cf091?from=timeline&isappinstalled=0)  [grub2fm](https://github.com/a1ive/grub2-filemanager/releases) [GRUB2配置文件](http://www.jinbuguo.com/linux/grub.cfg.html)

 [传统System V系统守护进程的管理 ](https://www.initroot.com/linuxintroduction/linuxdaemonsysv.html)  [System V、BSD、Posix概念](https://blog.csdn.net/qq_29344757/article/details/78657874)   [开机自启动](https://baijiahao.baidu.com/s?id=1707123036458447562&wfr=spider&for=pc)  [驱动加载initrd](https://blog.csdn.net/liudongdong19/article/details/79774171)     [从“头号玩家”看懂大火的“元宇宙”的未来形态](https://zhuanlan.zhihu.com/p/435968069) 

讲的透彻的资料：[grub2详解(翻译和整理官方手册) ](http://www.javashuo.com/article/p-tuyfivcl-cb.html)     [ grub2救援](https://blog.csdn.net/wang_xya/article/details/45741449)    [ CentOS7启动流程](https://blog.csdn.net/qq_25518029/article/details/119904129)  [CentOS6启动流程](https://blog.csdn.net/qq_25518029/article/details/119905231)  [grub2详解-必须看](http://www.javashuo.com/article/p-tuyfivcl-cb.html)   [GRUB2启动和组成结构 ](https://wenku.baidu.com/view/d1a9f483f624ccbff121dd36a32d7375a417c686.html)  [GRUB2启动和组成结构](https://blog.csdn.net/weixin_30418341/article/details/96701701)    [centos7的启动过程](https://blog.51cto.com/m51cto/1958856)    [MBR引导类型详解](https://blog.csdn.net/China_XXX/article/details/119995334)   [grub4dos](http://grub4dos.chenall.net/)  [GNU GRUB Manual 2.06官方手册](https://www.gnu.org/software/grub/manual/grub/html_node/index.html#SEC_Contents)

```
grub2修复：
1、开机进入grub rescue模式
2、进入grub
3、可见grub menu，无法开机
4、进入initramfs
5、处理grub异常状况

1、mbr找不到硬盘：帮它找到grub位置
2、找到磁盘与分区，找不到可用的grub.cfg  [2、3都是cfg文件有问题]
3、能找到grub.cfg,但文件有问题，无法找到核心，无法识别uuid或label
4、载入内核没问题，真正的文件系统挂载不了； 可以利用mount挂载。假设你已经确认：/ 在/dev/sda3，/boot在/dev/sda2；  chroot /mnt改变根目录；blkid查看磁盘分区uuid
5、上面4种错误处理完后，进入系统接著处理的事情。不然下次开机仍会发生一样的问题

grub2设备从0开始，分区从1开始
```

```
 search --no-floppy   --fs-uuid   --set=root   --hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1 --hint='hd0,msdos1'  367d6a77-033b-4037-bbcb-416705ead095
 搜uuid为"{367d6...95}"的设备，使用多个hint，表示先匹配bios平台下/boot分区为(hd0,msdos1)的设备，以后还指定了几个hint，但由于search使用的是uuid搜索方式，因此这些hint选项是多余的，由于单磁盘上分区的uuid是惟一的。
两个boot分区(如多系统共存时): search --no-floppy --fs-label=boot --set=root --hint=hd0,msdos5  不使用uuid搜索，而是使用label方式搜索
```

```
set root=(hd0,3); linux (hd0,2)/vmlinuz-3.11.0-18-generic root=/dev/sda3; initrd (hd0,2)/initrd.img-3.11.0-18-generic; boot
grub2命令：
ls、lsmod、cat、set设环境变量、unset取消变量、insmod载入模块、rmmod卸载模块、background_color当前激活输出终端的背景颜色、background_image仅在使用'gfxterm'作为输出终端时，才能改变。
search [--file|--label|--fs-uuid] [--set [var]] [--no-floppy] name:经过文件[--file]、卷标[--label]、文件系统UUID[--fs-uuid]来搜索设备;
configfile:装载配置文件，在grub.cfg丢失时，该命令将排上用场； 
export：导出环境变量，若在configfile的file中导出环境变量，将会在当前环境也生效。
menuentry定义一个菜单、terminal_input不带参数，列出输入终端、terminal_output列出输出终端、linux载入内核映像、initrd载入"initial ramdisk"
probe:探测分区或磁盘的属性信息
save_env和list_env: 环境变量保存到环境变量块中，列出当前的环境变量块中的变量
loopback: 将file映射为回环设备。-d删除映射 loopback loop0 /path/to/image;  ls (loop0)/
normal和normal_exit：进入和退出normal模式，相对于救援模式

常用内置变量：prefix：grub自动将/boot/grub2目录的绝对路径赋值给该变量，使得之后能够直接从该变量所表明的目录下加载各文件或模块。 set prefix = (hd0,gpt1)/boot/grub2/
root：指定根设备名称，通常该变量根据prefix变量设置而来。 例如：prefix=(hd0,gpt1)/boot/grub2，则root=(hd0,gpt1)，
```

```
grub内核的启动参数(3类：编译内核时参数，启动时参数和运行时参数):
init=   ：指定Linux启动的第一个进程init的替代程序。
root=   ：指定根文件系统所在分区，在grub中，该选项必须给定。
ro,rw   ：启动时，根分区以只读仍是可读写方式挂载。不指定时默认为ro。
initrd  ：指定init ramdisk的路径。在grub中由于使用了initrd或initrd16命令，因此不须要指定该启动参数。
rhgb    ：以图形界面方式启动系统。
quiet   ：以文本方式启动系统，且禁止输出大多数的log message。
net.ifnames=0：用于CentOS 7，禁止网络设备使用一致性命名方式。
biosdevname=0：用于CentOS 7，也是禁止网络设备采用一致性命名方式。
             ：只有net.ifnames和biosdevname同时设置为0时，才能彻底禁止一致性命名，获得eth0-N的设备名。

grub2配置文件:
1、经过/etc/default/grub文件生成grub.cfg
grub2-mkconfig用来生成grub.cfg文件: grub2-mkconfig -o /boot/grub2/grub.cfg;  grub2-mkconfig是根据/etc/default/grub文件来建立配置文件的。该文件定义grub的全局宏，修改内置的宏能够快速生成grub配置文件。实际上在/etc/grub.d/目录下还有一些grub配置脚本，这些shell脚本读取一些脚本配置文件(如/etc/default/grub)，根据指定的逻辑生成grub配置文件。
虽然可用的宏较多，但可能用的上的就几个：GRUB_DEFAULT、GRUB_TIMEOUT、GRUB_CMDLINE_LINUX和GRUB_CMDLINE_LINUX_DEFAULT。

2、脚本方式直接编写grub.cfg文件
```

```
一、硬件启动阶段
二、grub2引导阶段
三、内核引导阶段：加载驱动，切换到真正的根文件系统
四、systemed系统初始化阶段
MB：单位以10为底数的指数；   MiB：是以2为底数的指数    1KB=10^3 =1000,  1KiB=2^10=1024
```

```
二、grub2引导阶段：
1. 先加载两个镜像；（boot.img、core.img）
2. 再加载MOD模块文件，把grub2程序加载执行；
3. 接着解析配置文件/boot/grub/grub.cfg，根据配置文件加载内核模块到内存；
4. 之后构建虚拟根文件系统，最后转到linux内核。

grub.cfg配置：CentOS7中一般使用命令进行配置，而不直接去修改配置文件。不过我们可以看到grub.cfg配置文件开头注释部分说明了由/etc/grub.d/目录下文件和/etc/default/grub文件组成。一般修改好配置后都需要使用命令grub2-mkconfig -o /boot/grub2/grub.cfg，将配置文件重新生成。
```

```
三、内核引导阶段： 加载驱动，切换到真正的根文件系统。
/boot/vmlinuz  		linux内核映像及内核参数传递；
/boot/initramfs		在内存中释放供内核使用的根文件系统/boot/initramfs，挂载真正的根文件系统，最后执行/usr/lib/systemd/system
内核初始化
```

```bash
四、systemed系统初始化阶段
default.target指向了/lib/systemd/system/下的graphical.target或multiuser.target;  
graphical.target依赖multiuser.target，multiuser.target依赖basic.target，basic.target依赖sysinit.target，所以倒过来执行。

1. 执行默认target配置文件/etc/systemd/system/default.target（这是一个软链接，与默认运行级别有关）；default.target -> /usr/lib/systemd/system/multi-user.target

2. 然后执行sysinit.target来初始化系统和basic.target来准备操作系统；  /usr/lib/systemd/system/sysinit.target;  
/usr/lib/systemd/system/basic.target;    /usr/lib/systemd/user/basic.target

3. 接着启动multi-user.target下的本机服务，并检查/etc/rc.d/rc.local文件是否有用户自定义脚本需要启动；(rc.local是为了达到兼容性的目的)
4. 最后执行multi-user下的getty.target及登录服务，检查default.target是否有其他的服务需要启动。
```



> 1、vmlinuz：是可引导的、压缩的[内核](https://baike.baidu.com/item/内核/108410)。“vm”代表 “Virtual Memory”。Linux 支持[虚拟内存](https://baike.baidu.com/item/虚拟内存/101812)，Linux能够使用硬盘空间作为虚拟内存，因此得名“vm”。vmlinuz是可执行的Linux内核，它位于/boot/vmlinuz，它一般是一个软链接。 作用：进程管理、内存管理、文件管理、驱动管理、网络管理。
>
> 2、initrd.img是一个小的映象， 放的是和启动相关的驱动模块。通常的步骤是先启动内核，然后内核挂载initrd.img，并执行里面的脚本来进一步挂载各种各样的模块。其中最重要的就是根文件系统驱动模块，有了它才能挂载根文件系统，继而运行用户空间的第一个应用程序init或者systemd，完成系统后续的启动

```
core.img是动态生成的，路径为/boot/grub2/i386-pc/core.img； 而其余的img则存在于/usr/lib/grub/i386-pc目录下。grub2的默认配置文件为/boot/grub2/grub.cfg

X86 GRUB2启动流程：
1、上电 -> BIOS：硬件电路产生RESET信号并经复位引脚输入给CPU，CPU进入实模式，执行第一条指令,0xFFFF0物理地址(ROM)处存放的是BIOS执行代码,BIOS完成上电POST、BIOS中断调用等初始化,最终读取主引导扇区的512B的数据至0x7C00物理内存地址开始处，并跳转至0x7C00处执行代码；
主引导扇区512B数据格式：
a) 0x000 ~ 0x1BD：占446B，为MBR引导代码；
b) 0x1BE ~ 0x1FD：占64B，4组磁盘分区表信息(DPT)，每组分区信息占16B
c) 0x1FE ~ 0x1FF：结束标志，0x55和0xAA；
2、BIOS -> MBR(GRUB2 boot.img)
此场景中MBR引导代码即GRUB2的boot/i386/pc/boot.S编译出来的代码，称为boot.img；代码执行位置即0x7C00， boot.img唯一作用：读取属于core.img的第一个扇区并跳转到它身上，将控制权交给该扇区的img。【主要行为：设置堆栈指针为ox2000处，探测硬盘CHS/LBA工作模式，并加载第二个扇区最终至0x8000处，并跳至0x8000执行】【boot.img最终加载diskboot.img至0x8000处，并跳至0x8000处执行代码】， bootloader约定使用0x1000~0x10000内存段；
3、GRUB2 boot.img-> GRUB2 diskboot.img (第2个扇区)
第二个扇区代码由boot/i386/pc/diskboot.S编译生成，称为diskboot.img；boot.img最终加载diskboot.img至0x8000处，并跳至0x8000处执行代码；

4、GRUB2 diskboot.img -> GRUB2 kernel.img(第3~ n个扇区, n<63)
diskboot.img的作用是读取GRUB2的内核kernel.img（由kern\下的文件生成）至内存的某位置处；
kernel.img主要工作：初始化系统，加载模块，并进入normal或者rescue模式，GRUB2会根据配置文件或者用户输入，加载操作系统并运行；调用grub_load_modules()来加载所有的模块，这就是GRUB2扩展性能的体现之一。

内核初始化系统中各设备并做相关的配置工作，其中包括CPU、I/O、存储设备等,
设备驱动程序，一部分直接编译进内核镜像中，另一部分以模块的形式放在initrd(ramdisk)中。

boot.img=>core.img(diskboot.img、kernel.img、module & others)
```

```
硬盘：1、柱面：硬盘通常由重叠的一组盘片构成，每个盘面对应一个磁头。所有的磁头都是连在同一个磁臂上的，因此所有磁头只能“共进退”。所有盘面中相对位置相同的磁道组成柱面；  【每个盘面都被划分为数目相等的磁道，并从外缘的“0”开始编号，具有相同编号的磁道形成一个圆柱，称之为磁盘的柱面； 柱面数与一个盘面上的磁道数相等】  不同盘片相同半径构成的圆柱面：为柱面

2、磁盘块/簇（虚拟出来的）：操作系统中最小的逻辑存储单位。操作系统与磁盘打交道的最小单位是磁盘块。 通俗的来讲，在Windows下如NTFS等文件系统中叫做簇；在Linux下如Ext4等文件系统中叫做块（block）。每个簇或者块可以包括2、4、8、16、32、64…2的n次方个扇区。
【为什么有块：1、读取方便：由于扇区的数量比较小，数目众多在寻址时比较困难，所以操作系统就将相邻的扇区组合在一起，形成一个块，再对块进行整体的操作。2、分离对底层的依赖：操作系统忽略对底层物理存储结构的设计。通过虚拟出来磁盘块的概念，在系统中认为块是最小的单位。】
3、page：操作系统与内存操作，是虚拟一个页的概念来作为最小单位。与硬盘打交道，以块为最小单位。   每个盘面都有自己的磁头，因此，盘面数等于总的磁头数
扇区： 硬盘的最小读写单元      块/簇： 是操作系统针对硬盘读写的最小单元      page： 是内存与操作系统之间操作的最小单元。  

4、容量 ＝ 磁头数(盘面数) × 磁道(柱面)数 × 每磁道扇区数 × 每扇区字节数
```

 

```
1、硬盘有多个盘片，每盘片2个面，每个面一个磁头
2、 盘片被划分为多个扇形区域即扇区
3、同一盘片不同半径的同心圆：为磁道
4、不同盘片相同半径构成的圆柱面：为柱面
5、容量 ＝ 磁头数(盘面数) × 磁道(柱面)数 × 每磁道扇区数 × 每扇区字节数
6、信息记录可表示为：xx磁道（柱面），xx磁头，xx扇区(sector) 【CHS柱面磁头扇区】 CHS寻址
7、MBR位于硬盘第一个物理扇区（绝对扇区）柱面0，磁头0，扇区1处。由于DOS是由柱面0，磁头1，扇区1开始，故MBR不属于DOS扇区，DOS不能直接访问。MBR中包含硬盘的主引导程序和硬盘分区表。分区表有4个分区记录区。记录区就是记录有关分区信息的一张表。它从主引导记录偏移地址01BEH处连续存放，每个分区记录区占16个字节。
```

```
1.44m的3.5英寸软盘，每个磁道分18个扇区。

chs称为“绝对扇区”表示法；dos不能直接使用绝对扇区进行磁盘上的信息管理，而是用所谓“相对扇区”或“DOS扇区”。“相对扇区”只是一个数字，如柱面140，磁头3，扇区4对应的相对扇区号为2757。
当使用相对扇区编号时，DOS是从柱面0，磁头1，扇区1开始（注：柱面0，磁头0，扇区1没有DOS扇区编号，DOS下不能访问，只能调用BIOS访问），第一个DOS扇区编号为0，该磁道上剩余的扇区编号为1到16（设每磁道17个扇区），然后是磁头号为2，柱面为0的17个扇区，形成的DOS扇区号从17到33。直到该柱面的所有磁头。
然后再移到柱面1，磁头1，扇区1继续进行DOS扇区的编号，即按扇区号，磁头号，柱面号（磁道号）增长的顺序连续地分配DOS扇区号。
```



> 1. Bios->MBR(grub等引导程序安装在MBR)
> 1. boot loader(grub引导菜单、解析grub的配置文件/boot/grub/grub.conf，然后加载内核镜像到内存中，并将控制权转交给内核；etc/grub.conf)
> 3. 加载kernel内核  (内核初始化系统中各设备并做相关的配置工作，其中包括CPU、I/O、存储设备等),
>    设备驱动程序，一部分直接编译进内核镜像中，另一部分以模块的形式放在initrd(ramdisk)中。
> 2. 启动init进程，依据> inittab设定运行级别runlevel     ps -ef|grep init    initab终端初始化设置
> 3. init进程，读取inittab，执行rc.sysinit,rc等脚本(etc/inittab    etc/rc.d/rc.sysinit   etc/rc.d/rc3.d)
> 4. 启动内核模块；(启动mingetty，进入登录界面)
> 5. 执行不同运行级别的脚本程序
> 6. 执行etc/rc.d.local
> 7. 执行/bin/login程序，启动minegetty登录

system V启动的第一个用户进程为init，所有的守护进程都是由init进程启动。

systemd是Linux系统最新的初始化系统(init),作用是提高系统的启动速度，尽可能启动较少的进程，尽可能更多进程并发启动.

etc/init.d 存放系统服务的管理（启动与停止）脚本; 用service resin start 执行；  

服务分  独立启动 和 超级守护进程(xinetd或inetd两个超级守护进程)

/etc/init.d是指向/etc/rc.d/init.d的软连接  ll init.d；   rc.d/rc[0-6]为系统的运行级别runlevel(用户定义的执行登记 1单人  3文本  5图形)；   rc3.d/S10network   S为启动服务，10为启动顺序，依序启动服务。

/etc/init.d/rcS系统开机后执行的脚本；/etc/init.d/rcK系统关机时执行的脚本。  
init 5    3切换到5               
设置服务开机启动: chkconfig daemon on        

###### b. Systemd

[Systemctl 详解 - 简书](https://www.jianshu.com/p/3dd6b57a16bf)    [Systemctl ](https://www.jianshu.com/p/3dd6b57a16bf)   [systemd配置文件详解](https://blog.csdn.net/zj631455878/article/details/122133912)  [systemd 配置](https://blog.csdn.net/zj631455878/article/details/122133912)    [systemctl详细理解及常用命令](https://blog.csdn.net/skh2015java/article/details/94012643)      [系统和用户配置文件](https://blog.csdn.net/qq_16268979/article/details/114771258)     [systemd的service文件说明](https://blog.csdn.net/qq_16268979/article/details/114771854)  [systemd 配置文件](https://www.cnblogs.com/mhc-fly/p/8512491.html)  [Systemd 配置](https://linux.cn/lfs/LFS-BOOK-7.7-systemd/chapter07/systemd-custom.html)   [systemd.unit配置完整字段官方文档](https://www.freedesktop.org/software/systemd/man/systemd.unit.html)     [ udev](https://blog.csdn.net/chengziwang/article/details/111873757)  [Linux管理临时文件tmpfiles ](https://www.jianshu.com/p/a338f0705615)  [tmpfiles.d 中文手册 ](http://www.jinbuguo.com/systemd/tmpfiles.d.html)    [systemctl 管理的 active(exited) 状态说明 ](http://www.360doc.com/content/20/1213/16/17673261_951276461.shtml)

[CentOS 7 添加开机启动服务/脚本](https://www.iemblog.com/?p=1312&lang=zh)   [centos7用rc.local来管理开机自启动脚本](https://blog.csdn.net/weixin_39573822/article/details/110665322?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_title~default-4-110665322-blog-121547138.pc_relevant_antiscanv2&spm=1001.2101.3001.4242.3&utm_relevant_index=7)  [CentOS7 开机自启动脚本 ](https://www.jianshu.com/p/3d817f5b9403)  [CentOS7开机启动](http://t.zoukankan.com/haoyufeng-p-4449507.html)  [centos7 系统服务启动程序 ](https://www.xiaocaicai.com/2020/07/centos7-系统服务启动程序-开机启动-systemd-service/)    [CentOS7编写systemd服务脚本](https://wenku.baidu.com/view/be5ee35e32b765ce0508763231126edb6f1a7627.html)   [系统运维|在 systemd 中使用控制组管理资源](https://linux.cn/article-13881-1.html)  [SysVinit to Systemd Cheatsheet - Fedora Project Wiki](https://fedoraproject.org/wiki/SysVinit_to_Systemd_Cheatsheet)       [centos7下nginx作为服务开机启动](https://blog.csdn.net/xiaofangzhen/article/details/121421716 "centos7下nginx作为服务开机启动")

/sbin/init  软链接到  /lib/systemd/systemd;

```bash
Systemd 默认从目录/etc/systemd/system/读取配置文件。但是，里面存放的大部分文件都是符号链接，指向目录/usr/lib/systemd/system/，真正的配置文件存放在那个目录。       systemctl enable命令用于在上面两个目录之间，建立符号链接关系。

systemd也分系统和用户的设置；系统/etc/systemd/system/   用户/usr/lib/systemd/user/  
配置文件主要放在/usr/lib/systemd/system，也可能在/etc/systemd/system
systemctl cat sshd.service 查看配置文件

Systemd 可以管理所有系统资源。不同的资源统称为 Unit; 一共分12种unit； 配置文件的后缀名，就是该 Unit 的种类，比如sshd.socket;     每一个 Unit 都有一个配置文件，告诉 Systemd 怎么启动这个 Unit 。

```

```bash
systemd的Unit放在目录/usr/lib/systemd/system(Centos) 或 /etc/systemd/system(Ubuntu)；主要有四种类型文件.mount,.service,.target,.wants
wants文件定义了要执行的文件集合，每次执行，.wants文件夹里面的文件都会执行；   .target定义了一些基础的组件，供.service文件调用(Target是服务组，表一组服务);  .mount定义一个挂载点，[Mount]节点里配置了What,Where,Type三个数据项;等同于以下命令： mount -t hugetlbfs /dev/hugepages hugetlbfs

配置文件：
1. unit：启动顺序与依赖
after\before 在哪些服务之后/前启动；wants/requires 弱/强依赖，弱依赖启动失败不影响服务。

2. service：启动行为:如何启动服务
EnvironmentFile段：服务的环境参数文件。该文件内部的key=value键值对，可以用$key的形式，在当前配置文件中获取。
ExecStart：启动进程时执行的命令；ExecReload重启；ExecStartPre启动服务之前执行的命令；ExecStartPost启动之后
前加-，表示"抑制错误"，即发生错误的时候，不影响其他命令的执行。比如，EnvironmentFile=-/etc/sysconfig/sshd

启动类型
type：启动类型；simple(启动的进程为主进程)、forking、oneshot、dbus、notify、idle
RemainAfterExit=yes 表示进程退出后，它上面的命令就开始执行。

重启行为：
killmode=process 	定义 Systemd 如何停止 sshd 服务；     表示只停止主进程，不停止sshd 子进程；
restart=on-failure  定义sshd 退出后，Systemd 的重启方式;   表示任何意外失败，就重启sshd
RestartSec   重启服务前，需要等待的秒数

3.install 如何安装这个配置文件，即怎样做到开机启动
WantedBy：该服务所在的 Target; Target是服务组，表一组服务。WantedBy=multi-user.target指的是，sshd 所在的 Target 是multi-user.target         
#systemctl get-default   Systemd默认的启动Target,在这个组里的所有服务，都将开机启动.      
查看 multi-user.target 包含的所有服务:  systemctl list-dependencies multi-user.target        切换到另一个 target: systemctl isolate shutdown.target

4. Target 配置文件里面没有启动命令
Conflicts=1:冲突字段，1运行，它就不能运行
AllowIsolate=yes：允许使用systemctl isolate命令切换到multi-user.target

5. 修改配置文件以后，需要重新加载配置文件 systemctl daemon-reload ，然后重启相关服务 systemctl restart foobar

```

```bash
比如我们为 etcd 服务创建了配置文件 /lib/systemd/system/etcd.service，然后执行 enable 命令：systemctl enable etcd.service；   所谓的 enable 就是在 multi-user.target.wants 下面创建了一个链接文件；  至于为什么会链接到 multi-user.target.wants 目录下，则由 etcd.server 文件中的配置决定。

WantedBy=multi-user.target 这个设置非常重要，因为执行systemctl enable sshd.service命令时，sshd.service的一个符号链接，就会放在/etc/systemd/system目录下面的multi-user.target.wants子目录之中。

systemctl enable命令用于在两个目录之间(/etc/systemd/system/    /usr/lib/systemd/system/)，建立符号链接关系；
```

 *.service启动服务的配置，systemctl就是操作\*.service;

手工创建的单元文件（service文件）建议存放在/etc/systemd/system/；

创建开机启动脚本: [CentOS 7 添加开机启动服务/脚本](https://www.iemblog.com/?p=1312&lang=zh)  [systemd 开机执行rc.local ](http://www.javashuo.com/article/p-adqmdgpa-dd.html)

##### 7.权限

[visudo](https://blog.csdn.net/allway2/article/details/122173365)  [NOPASSWD还需密码](https://www.php.cn/wenda/101214.html)   [Linux 文件基本属性](https://www.runoob.com/linux/linux-file-attr-permission.html)  visudo   chattr   p156-161企业生产环境用户权限集中管理

```bash
user	machine= 		commands   //机器=(授权哪个角色的权利)   
root    all=(all)		 all       //能用哪些命令  例如/usr/sbin/useradd
myttian ALL=(ALL)   /usr/sbin/useradd          查看用户id myttian  sudo -l
NOPASSWD放最后，不然%sudo会把这条给覆盖掉   sudo su - root    //which ls

文件属性两种设置方法，一种是数字(r4 w2 x1)，一种是符号(rwx)
```

#####  8.中文字符集 时间同步

字符集配置文件 /etc/locale.conf (centos7)      export LANG="zh_CN.UTF-8" 临时     乱码转换: iconv

查看已安装 locale -a | grep zh_CN      [CentOS7设置中文字符集 ](https://www.cnblogs.com/wucongzhou/p/12579332.html)

ntpdate  定时任务：/var/spool/cron/root      crontab -l

##### 9.  文件类型和权限

```
drwxr-xr-x   d属主属组其它用户 硬链接数
类型：字符设备(串行接口设备)及块设备(硬盘光驱等);  
软链接(ln -s)、硬链接(通过索引节点号Inode Index连接,)文件  ls -i   find / -inum 33 找所有硬链接
setuid setgid 粘帖位 chmod chown umask
目录不可创建硬链接，目录下有一个硬链接号.和上级目录链接..
```

##### 10. 分区p162-168  193

[linux系统文件属性_老男孩](https://blog.csdn.net/youmatterhsp/article/details/80010468)  [用户管理](https://blog.csdn.net/youmatterhsp/article/details/80533132?ops_request_misc=%7B%22request%5Fid%22%3A%22165244480616782395360941%22%2C%22scm%22%3A%2220140713.130102334.pc%5Fblog.%22%7D&request_id=165244480616782395360941&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_ecpm_v1~rank_v31_ecpm-8-80533132-null-null.nonecase&utm_term=老男孩&spm=1018.2226.3001.4450)  [磁盘分区](https://blog.csdn.net/youmatterhsp/article/details/80684937?ops_request_misc=%7B%22request%5Fid%22%3A%22165244480616782395360941%22%2C%22scm%22%3A%2220140713.130102334.pc%5Fblog.%22%7D&request_id=165244480616782395360941&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_ecpm_v1~rank_v31_ecpm-14-80684937-null-null.nonecase&utm_term=老男孩&spm=1018.2226.3001.4450)  [运维入门](https://blog.csdn.net/youmatterhsp/article/details/80315693?ops_request_misc=%7B%22request%5Fid%22%3A%22165244480616782395360941%22%2C%22scm%22%3A%2220140713.130102334.pc%5Fblog.%22%7D&request_id=165244480616782395360941&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_ecpm_v1~rank_v31_ecpm-23-80315693-null-null.nonecase&utm_term=老男孩&spm=1018.2226.3001.4450)  [用户权限集中管理方案](https://blog.csdn.net/youmatterhsp/article/details/80557168?ops_request_misc=%7B%22request%5Fid%22%3A%22165244480616782395360941%22%2C%22scm%22%3A%2220140713.130102334.pc%5Fblog.%22%7D&request_id=165244480616782395360941&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_ecpm_v1~rank_v31_ecpm-29-80557168-null-null.nonecase&utm_term=老男孩&spm=1018.2226.3001.4450)   [find+sed考试题及生产实战解决案例分享 ](https://blog.51cto.com/oldboy/792396)  [Web服务器磁盘满深入解析及解决](https://blog.51cto.com/oldboy/612351)    [ 硬盘介绍及硬盘分区 ](https://www.cnblogs.com/fengze/p/6756300.html)  [文件系统](https://blog.51cto.com/yolynn/1895136)   [Linux文件系统](https://www.cnblogs.com/tcicy/p/8458359.html) [ 服务器技术和架构](https://blog.csdn.net/weixin_34242509/article/details/91440806)

分区格式化为ext3后，一般有2部分，inode和block，block存实际数据，inode存属性信息(ls -l的结果)，df -i：查看inode的用量。df -h：查看磁盘使用量。dumpe2fs /dev/sda1|grep -i "Inode count"：查看Inode的数量。[查看分区文件系统](https://www.linuxprobe.com/partition-file-system.html)

```
fdisk -l   df -h    du -sh /*(目录文件大小)  free -m  文件系统：df -T -h   lsblk -f
parted分区：fdisk大于2T不能用；
```



##### 11.网络配置p127

```
hostname 主机名   sed -i 's#hostname#britney#g' /etc/sysconfig/network     /etc/hosts
ifconfig   /etc/sysconfig/network-scripts/ifcfg 配置ip及gw   /etc/resolv.conf 配置DNS  
ifup ifdown启动网卡  route -n
```

##### 12.定时任务Crond

[linux定时任务crond](https://blog.51cto.com/oldboy/1410555)   [crontab命令](https://blog.51cto.com/oldboy/485969)

守护进程：就是一直运行的程序。 分2种：系统自己配置的定时任务(ll /etc |grep cron)； 用户定义的任务

```
定时任务软件：at(就执行一次)、crontab(守护进程crond)、anacron(非7*24开机)
crontab [-u user] {-leri}     #l list、e edit、r del、i    cat /etc/crontab
哪些用户能用cron,/etc/cron.deny cron.allow;allow优先deny；crontab配置文件在/var/spool/cron
时间单位：分、时、日、月、周；      
用户定时任务6段，系统的7段；前5段为时间设定，第6段为命令或脚本
```

```shell
* 任意时间都，"每"的意思， 00 01 * * * cmd表示每月每周每日的凌晨1点执行cmd任务。
- 时间段；  00 17-19 * * * cmd，就是17,18,19点的整点分别执行cmd；
, 分隔时间段；  30 17,18,19 * * * cmd 表示每天17,18,19点的半点执行cmd；
/n 每隔n单位时间； 每10分钟执行一次任务  */10 * * * * cmd,

定时任务结尾加 >/dev/null 2>&1      # n >& m	将输出文件 m 和 n 合并。
>/dev/null 2>&1 等价于 1>/dev/null  2>/dev/null   (一般脚本任务加)
每次执行定时任务，系统会给root发邮件，如果不加 >/dev/null 2>&1,同时邮件服务又没开，邮件都到临时目录/var/spool/clientmqueue(邮件临时队列目录，垃圾文件存放于此)，文件猛增，占用大量inode节点，以致inode满而无法写入正常文件；(如果是centos 6.4，默认不装sendmail服务，所以不会有这个目录。）
```

##### 13.NFS网络文件系统P173-192

[ NFS ](https://www.cnblogs.com/fengze/p/6752564.html) [NFS网络文件共享](https://www.shuzhiduo.com/A/kPzOmRw5xn/)  [NFS ](https://www.bbsmax.com/A/kPzOmRw5xn/) [ systemctl 停止iptables](https://www.csdn.net/tags/MtTaAg4sNTgxNDM1LWJsb2cO0O0O.html)  [配置问题解决](https://blog.csdn.net/HelloWorld_4396/article/details/111614806)  [exportfs命令](https://blog.csdn.net/weixin_33967071/article/details/91735157)  [win7 使用NFS](https://blog.51cto.com/u_9597987/3493469)  [win7挂载nfs](https://blog.csdn.net/weixin_28829903/article/details/119498972)  [mount](https://blog.csdn.net/weixin_40277264/article/details/122433290)  [NFS服务器配置（windows访问） ](http://t.zoukankan.com/BrokenEaves-p-14452681.html)   [NFS参数](https://www.cnblogs.com/panther1942/p/12775650.html)   [windows下挂载NFS权限修改](https://www.shuzhiduo.com/A/n2d9y1Y6dD/)

NFS客户端通过挂载mount的方式访问NFS服务端；小企业用NFS,大公司用分布式MFS,GFS,FASTFS;

用户上传的文件放到NFS;   低成本：淘宝就用lvs+haproxy替换了netscaler，用fastfs，TFS替换了netapp，emc存储；

```
NFS传输时使用的端口是随机的，通过RPC（远程过程调用）协议/服务来实现； RPC记录每个NFS功能对应的端口号，将该信息传递给请求数据的NFS客户端，让client连接到正确的端口，实现数据传输。RPC服务用111监听NFS客户端的请求。
启动nfs，首先要启动RPC服务，C5.8 portmap,C6.4 rpcbind服务，修改nfs配置文件，不需重启nfs，执行/etc/init.d/nfs reload 或 exprtfs -rv即可使/etc/exports生效
```

```bash
1. ifconfig eth0; 部署nfs,要安装2个软件包,nfs-utils(nfs主程序),portmap(rpc主程序);查询已安装:rpm -qa nfs-utils rpcbind  portmap
创建共享目录：mkdir /data/bbs -p 设权限：chown -R nfsnobody.nfsnobody /data/bbs 

2. 启动相关服务:systemctl start apache.service  查看：systemctl [status|is-active|is-failed|is-enabled] apache.service     rpcinfo -p localhost   ps -ef|egrep "rpc|nfs"看进程多过滤； 至少2个daemons，一个管client是否能登录nfsd(rpc.nfsd)，一个管client能取得的权限(rpc.mountd)；  开机启动：chkconfig nfs on

3.配置NFS服务：
配置文件:/ext/exports ; 格式：共享目录   nfs客户端地址(参数...) 
client地址：ip、域名、主机名、*、网段(10.0.0.0/24)等;  参数：访问权限设置
exap:/home/oldboy 10.0.0.5(rw,sync)  #sync数据同步写入内存和硬盘中

4.客户端启动rpc：/etc/init.d/portmap start    开机启动：chkconfig portmap on
显示挂载：showmount -e 10.0.0.19  关防火墙：/etc/init.d/iptables stop  systemctl stop firewalld     exportfs -avr   查看nfs状态：nfsstat -s   tail -2 /etc/rc.local
5.client挂载:mount -t nfs srvip:/共享目录 /挂哪里   查看成功：df -h   umount -v /mnt/mymount/      卸不掉：umount -lf /mnt
只要nfs权限，目录权限也要设置(类似win共享和ntfs权限）；cat /var/lib/nfs/etab  
6.win7挂载nfs：程序中安装nfs，cmd中showmount -a srv查看，mount \\srv\共享目录  h:挂载 umount Z:  
win7挂载后uid2,gid2,只能读，改注册表HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ClientForNFS\CurrentVersion\Default中，添加DWORD值两项：AnonymousUid，AnonymousGid
7.开机自动挂载：2种方法：/etc/rc.local;  /etc/fstab
```
##### 14. Rsync同步+sersync p214-220

[rsync传输模式](https://blog.csdn.net/weixin_44953658/article/details/107676078)  [Rsync数据同步 ](https://www.cnblogs.com/zoe233/p/11962110.html)  [sersync实时同步 ](https://www.cnblogs.com/dsryyds/p/15111164.html)  [sersync 介绍](http://www.yunweipai.com/36026.html)  [Rsync+sersync实现文件自动同步](https://www.jianshu.com/p/67eb0573f5e4)  [sersync 实时](https://www.cnblogs.com/zhangrumingbj/p/3887742.html?utm_source=tuicool&utm_medium=referral) [sersync+rsync](https://blog.51cto.com/zhangshaoxiong/1307054)  [ sersync+rsync原理及部署](https://blog.csdn.net/sandy9919/article/details/80942491) [rsync+sersync实现数据实时同步](https://blog.51cto.com/xuegod/2322136)  [ lsyncd](https://blog.csdn.net/fgf00/article/details/81980995)  [ DRBD](https://blog.csdn.net/tjiyu/article/details/52723125) 

[打包脚本组合备份](https://blog.csdn.net/weixin_29503445/article/details/116668981) [rsync](https://blog.csdn.net/qq_33033819/article/details/118500427)  [rsync+sersync实现数据实时同步](https://blog.51cto.com/xuegod/2322136)  [sersync+rsync](https://blog.csdn.net/sandy9919/article/details/80942491)  [sersync+rsync](https://blog.51cto.com/zhangshaoxiong/1307054)  [sersync](https://www.cnblogs.com/jkz1/p/13028332.html)  

```shell
三种方法传输：1、本地数据传输(rsycn [option] src [dest]) : rsync  -avz  -P /opt  /tmp/
2、rpc ssh等通道传输: 拉 rsync [option] [user@] host:src [dest]   推：rsync [option] src  [user@]host:dest      #rsync -vzrtopg --progress -e 'ssh -p 22'  oldboy@10.0.0.141:/opt   /tmp  -vzrtopg=avz，同步时文件目录属性不变； --progress显示同步过程，可用-p代替； -e通过ssh传输数据  /tmp本地路径
3、以守护进程方式传输
相当于有服务端，配置rsync守护进程，分2种情况，每种情况2种语法：
拉：1、rsycn [option] [user@]host::src   [dest]      	2、rsycn [option] rsync://[user@]host[:port]/src   [dest]
推：1、rsync [option] src  [user@]host::dest  			2、rsync [option] src  rsync://[user@]host[:port]/dest 
```

普通用户推送用root权限,3种方法：1、用户配成sudo权限用户  2、把客户端echo、cp等命令修改为setuid权限位  3、配置root免登录认证，安全隐患(防火墙封堵ssh端口)

```bash
重点：守护进程方式；在备份服务器上以守护进程方式部署rsync服务，使得客户端可以把数据备份过来。
一、服务端：
1. 配置/etc/rsyncd.conf:   rsync分为全局模块和局部模块，全局模块针对所有局部模块生效，局部模块用来定义备份路径，有多个备份路径就定义多个局部模块;
2. 创建rsync用户，修改所属：mkdir /data /mysql_bak; chown -R rsync.rsync /data
2.创建虚拟用户认证文件，多用户逗号分隔，必须600权限
echo "rsyncd_backup:123456" >/etc/rsyncd_passwd     chmod 600 /etc/rsyncd_passwd
3.启动服务、关防火墙 systemctl start(enable) rsyncd;   stop firewalld
二、客户端
1.启动rsyncd，关防火墙
2.echo "123456" >/etc/rsyncd_passwd  #仅密码   chmod 600 /etc/rsyncd_passwd  
3.推测试：rsync -avz  /home/share/   rsyncd_backup@192.168.56.12::mysql_backup/  --password-file=/etc/rsync_password
#::后接rsyncd.conf的模块名;--password-file免交互输入密码
```

```bash
#全局模块 /etc/rsyncd.conf
uid = rsync
gid = rsync
port 873
fake super = yes
use chroot = no
max connections = 200
timeout = 600
ignore errors
read only = false
list = false
auth users = rsyncd_backup
secrets file = /etc/rsyncd_passwd
log file = /var/log/rsync/rsync.log
#局部多模块,多目录			
[web_backup]
comment = commit
path = /data
[mysql_backup]
comment = mysql bak
path = /mysql_bak
```

`rsync --daemon以守护进程方式启动； ps -ef|grep rsync |grep -v grep`  -v反向匹配，去除包含grep的进程行 ，避免影响最终数据的正确性

<font color=#0099ff size=5>Sersync + Rsync实时同步：客户端sersync服务，监控目录，实时推送到rsync服务端。</font>

```bash
实际上sersync就是监控本地的数据写入或更新事件，然后，在调用rsync客户端的命令，将写入或更新事件对应的文件通过rsync推送到目标服务器
1. 下载：wget https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/sersync/sersync2.5.4_64bit_binary_stable_final.tar.gz
2.tar -zxvf -C /home/sersync
3.修改xml：<sersync>监控目录，rsync服务器、模块；  <rsnyc>认证；作用是拼接同步到命令 <36行failLog path=>同步失败记录日志，60分钟失败重新同步；
4.开启sersync守护进程同步数据：sersync -r -d -o /root/sersync/conf/confxml.xml -d daemon  -o配置文件 -r初始化时同步
for n in `ls`;do echo(rm -f) 111>$n/$n.txt;done  `ls` esc下的反引号 `seq 10`10个文件

ps -ef |grep sersync进程  pkill sersync关进程
5. p215sersync配置文件、216插件、217生产测试报告、218压力测试、219撰写测试报告、220监控与优化(NAGIOS监控)
6.其他同步方案：lsyncd+rsync、csync2+inotify、csync2+lsyncd、drbd块数据同步

```

##### 15. ssh key免密码验证分发、管理、备份

无交互式验证数据传输；ssh提供2种安全验证：1、基于口令 2、基于密钥

```bash
1.添加系统账号：useradd oldboy;    echo "123456"|passwd --stdin oldboy #不需交互直接设置密码，结合shell可批量创建用户密码；userdel -rf oldboy 删除   tail -1(数字) /etc/passwd 查看
2.生成密钥对dsa key(生成钥匙和锁)：A为分发服务器，建立密钥对：公钥(public key作为锁)和私钥（作为钥匙）；A\B\C三个服务器其中一台建立一次就行；我选A来生产密钥对。用oldboy用户分发，切换su - oldboy; ssh-keygen -t dsa  #t密钥类型：ras加密和数字签名认证，dsa只能认证。 公钥/home/oldboy/.ssh/id_dsa.pub  私钥：id_dsa
3.分发公钥（发锁）：公钥从A拷到B.C用户家目录.ssh；系统自带发公钥脚本：ssh-copy-id -i id_dsa.pub oldboy@192.168.56.11       ssh配置文件cat /etc/ssh/sshd_config |grep -Ev '^$|#'
4.用oldboy用户测试:A访问B，不要密码 ssh oldboy@192.168.56.11  /sbin/ifconfig  
```

```bash
分发数据用scp：scp -P22 -r /home/oldboy/1 oldboy@192.168.56.11:~  Port  r目录  ~家目录 -p保持文件目录属性
rsync分发：rsync -avz -P -e 'ssh -p 22'   /home/1     oldboy@192.168.1.1:~
千台以上大公司：用cfengine、puppet等分发，复杂。
管理：用命令查看客户机 ssh oldboy@192.168.56.11  free -m 看内存
```

推送hosts到/etc，权限不够，方法3种：1、把oldboy配成sudo用户，visudo 开启Defaults requiretty； 用命令ssh -t hostname sudo <cmd>；2、setuid位；chmod 4755 /usr/bin/rsync（rsync命令给root权限） ; 3、root免登录认证。     [分发服务器安全管理](https://blog.csdn.net/youmatterhsp/article/details/80557099)

```
备份数据(多钥匙开一把锁)：x、y数据都备份到z，免验证；xy放私钥，z放公钥
```



### 二、视频教程

 [老男孩Linux初级运维教程](https://www.bilibili.com/video/BV1rJ411M7S1?p=6&spm_id_from=pageDriver) 

```
p37 su - myttian[加-为了把环境变量、用户配置文件全调过去]     //$普通用户  #root
p40 visudo      
```

 
