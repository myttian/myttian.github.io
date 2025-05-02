### 一、网段划分p230-234

[老男孩Linux初级运维教程](https://www.bilibili.com/video/BV1rJ411M7S1?p=230)  [Apifox - API 文档、调试、Mock、测试一体化协作平台](https://www.apifox.cn/?track_id=pbaes.mLk0Pos4z20nBd1SAo0SY-fifNu31G0kgM0YMNc5KKWkED3NPAzaC2jP_eXZusjHbjiF73fT9KfY2FWn11-P9PaujQZuRKSSaDzlAJjlSZa_OdkRVvsWzyToPoJSXBH8NAveroBTS5oUZ2EgkUcDkZ4Qua22Ux0FRox0xOskBbQ)

### 二、SSH p235-248

### 三、RAID  LVM p268-281

### 四、http  p283-292

[网络编程从Apache到Nginx](https://zhuanlan.zhihu.com/p/20204159)   [2021年8月Web服务器排行](https://zhuanlan.zhihu.com/p/405514312)  [ web服务器](https://www.csdn.net/tags/MtzaAg0sNzY2OTAtYmxvZwO0O0OO0O0O.html)  [2022年04月 Web 服务器排行](https://www.hellogithub.com/report/netcraft/?url=/periodical/volume/47/)  [April 2022 Web Server Survey | Netcraft News](https://news.netcraft.com/archives/2022/04/27/april-2022-web-server-survey.html)   [数据库排行榜](https://www.hellogithub.com/report/db-engines/?url=/periodical/volume/47/)  [编程语言排行榜](https://www.hellogithub.com/report/tiobe/?url=/periodical/volume/47/)  [alpha、beta、rc软件版本](https://baijiahao.baidu.com/s?id=1676595616359738233&wfr=spider&for=pc)  [Alpha、Beta、RC、GA版本的区别 ](https://zhuanlan.zhihu.com/p/420745873)

[rpm包制作](https://www.cnblogs.com/yanghuinnn/p/14984828.html)  [eDiary知识管理](https://zhuanlan.zhihu.com/p/403198730)   [RPM包制作](https://www.bilibili.com/video/BV1ai4y1N7gp?spm_id_from=333.337.search-card.all.click)  [搭建私有yum源与仓库](https://www.cnblogs.com/mrj0528/p/15349888.html)  [yum](https://www.osyunwei.com/archives/tag/yum)  [yum](http://yum.baseurl.org/)   [文德尔施泰因7-X](https://baike.baidu.com/item/文德尔施泰因7-X/22776035?fr=aladdin) [仿星器](https://baike.baidu.com/item/仿星器)

[使用echo $? 查看命令成功执行](https://zhuanlan.zhihu.com/p/78897515) [rpm安装到指定目录](https://www.jianshu.com/p/2c722186319e) [rpm命令详解 ](https://www.cnblogs.com/lpeng94/p/12546432.html?ivk_sa=1024320u)  [journal日志文件清理](https://blog.csdn.net/lijun_work/article/details/107480162?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~Rate-1-107480162-blog-107381541.pc_relevant_antiscanv2&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~Rate-1-107480162-blog-107381541.pc_relevant_antiscanv2&utm_relevant_index=2)     

[rpm命令小结](https://blog.csdn.net/shenwuwangc/article/details/84558544)

```bash
linux命令：
egrep -v '#|^$' nginx.conf #不显示空行、注释；   tree -L 1 /www 只显示一层； mkdir /www/{www,bbs,blog}  -p    sed处理文本；sed [option] 'command' input_file；命令：append、change、insert、delete、print、subs
是文件内容整齐排序：column -t     去重：sort -n yes.log |uniq -c   echo $? 查看命令成功执行；  echo $!打印进程号   rz上传文件   vimdiff (beyond compare比较文件)
正向代理为客户端服务\反向代理为服务器端服务。
使用 printf 的脚本比使用 echo 移植性好

```
##### 1.行业术语

IP：独立ip数，0-24点相同ip为一次。   PV（page view）：页面浏览量或点击率，用户每次刷新即被计算一次 。   UV（unique visitor）：访问的一台电脑client为一个访客，0-24内只算一次。

```
Netcraft 是一家总部位于英国巴斯始于 1995 年的互联网服务公司。 该公司官网每月发布的调研数据报告：Web Server Survey 系列 已成为当今人们了解全球网站的服务器市场份额、排名情况的主要参考依据， 时常被诸如 HelloGitHub、华尔街杂志、英国 BBC、Slashdot，等知名媒体引用。 每月更新一次
```

```
软件包安装方式：1、源码编译，灵活，自己做饭，只编译想要的参数   2、yum或rpm，简单，不灵活，下饭店吃饭   3、高级安装：通过源码制成符合自己需求的rpm，放到自己的yum仓库，给客户端通过yum批量部署。
```

##### 2. Nginx p308  cmake编译等

[Dmidecode](https://blog.51cto.com/hmtk520/2052041)  [Nginx ./configure --help ](https://blog.csdn.net/DMDD_NB/article/details/88800173) [configure作用](https://qastack.cn/programming/2529566/what-does-a-typical-configure-do-in-linux) [./configure](https://blog.csdn.net/weixin_32158567/article/details/116892809)  [c99错误](https://blog.csdn.net/IT_xiao_bai0516/article/details/123213842)  [编译为C99](https://www.orcode.com/question/690112_k94a53.html)  [nginx安装的是PCRE2](https://www.cnblogs.com/Jordandan/p/10402912.html) [安装 Nginx 库](https://www.cnblogs.com/webyu/p/14914389.html) [nginx 模块依赖库](http://wangying.sinaapp.com/archives/436)   [kill -9](https://blog.csdn.net/weixin_42319496/article/details/121125378)    [Centos7下安装Nginx并配置开机启动](https://blog.csdn.net/xiaofangzhen/article/details/121421716)  

Web和反向代理服务器软件，可作负载均衡服务器(Haproxy)、邮件代理服务、缓存服务器(squid)、

```
配置：/etc/nginx/nginx.conf (rpm安装)  主目录：/usr/share/nginx/html（rpm） 
配置文件语法检查：/usr/sbin/nginx -t  重启也可用发信号方式：kill -HUP 'cat /var/run/nginx.pid'   #向master进程的PID发信号  nginx支持的信号
nginx工作模式是1个master进程+n个worker进程
```

```bash
tar zxf解压；  ./configure    make && make install   #make编译; make install安装，有些软件要测试：make check;make test; make clean删临时文件； 
Configure是一个可执行脚本，有很多选项，在待安装的源码路径下使用命令./configure --help输出详细的选项列表； 
--prefix选项是配置安装的路径，不配置，安装后可执行文件默认放/usr/local/bin，库文件默认放在/usr/local/lib，配置文件默认放在/usr/local/etc，其它的资源文件放在/usr/local/share，比较凌乱。  ./configure --prefix=/usr/local/test；另一个好处是卸载软件或移植软件。卸载只须删除该安装目录，移植软件只需拷贝整个目录到另外一个机器即可（相同的操作系统）。 要卸载程序，也可以在原来的make目录下用一次make uninstall，但前提是make文件指定过uninstall。

configure检查系统、依赖等信息，运行configure生成makefile和configure.h文件；脚本由m4语言编写，是一种宏语言；makefile中有安装代码的位置，以及用于生成程序的编译器所需的定义(编译准备)；

#不是所有的tar包都是源代码的包，可以ls看看有没有configure这个文件，如果是二进制的包，解压后直接就能使用
3.c99错误解决：CFLAGS=-std=c99 ./configure

```

[autotools自动生成Makefile](https://baijiahao.baidu.com/s?id=1673786821319256844&wfr=spider&for=pc)  [configure原理](https://www.cnblogs.com/pysery/archive/2012/06/17/2552680.html)   [configure详解](https://blog.csdn.net/qinglinsan/article/details/51419559)   [configure详解](https://blog.csdn.net/zhangxuechao_/article/details/46820323)  [AutoTools制作deb包](https://blog.csdn.net/u011238754/article/details/121925895) [Autotools，Cmake和Scons区别](https://qastack.cn/programming/4071880/what-are-the-differences-between-autotools-cmake-and-scons)  [Cmake 语法](https://zhuanlan.zhihu.com/p/267803605)   [scons使用 ](https://www.cnblogs.com/hookjc/p/13183905.html) [scons ](https://baike.baidu.com/item/scons/7224721?fr=aladdin) [ Makefile.am 语法](https://blog.csdn.net/vevenlcf/article/details/48134313) [Makefile.am详解](https://blog.csdn.net/wh8_2011/article/details/78830430) 

[configure参数说明](https://www.cnblogs.com/my_life/articles/2119249.html)  [configure参数详解](https://www.jianshu.com/p/ea75de3a47bd)  [ configure详解](https://blog.csdn.net/zhangxuechao_/article/details/46820323) 

```
1. 作为源代码发行的软件，希望在尽可能多的环境上可以运行，这些环境包括了操作系统的类型，硬件系统、开发环境的不同的方面；
另一方面，在Linux系统中没有一种统一的位置可以确定系统中是否支持某种功能，例如：无 法确认这个系统是否安装了gcc工具，它的位置在哪里，该操作系统是否支持mmap功能、甚至是环境是大端字节序还是小端字节序等属性，
所以需要通过执行 configure来动态的尝试确定源代码构建和运行环境需要的属性情况。最重要的目的是替换Makefile中的指定变量，
2. GNU 提供的Autoconf及Automake可以自动生成Makefile；
```

```bash
1.安装Pcre：perl兼容正则，安装pcre使nginx支持http rewrite模块； dmidecode | grep "Product Name" #将DMI数据库中的信息解码，获取硬件信息  
2.安装nginx：    mkdir -p /home/oldboy/tools #p不提示目录是否存在，循环向下创建目录；
先创建nginx用户(每个软件运行时，都创建一个用户)useradd nginx -s /sbin/nologin -M #禁止登录，M不创建家目录
 ./configure --user=nginx --group=nginx --prefix=/software/nginx-1.20.2 --with-http_stub_status_module --with-http_ssl_module #激活状态模块  #./configure --help 查看模块  
 3.ln -s /software/nginx-1.20.2 /software/nginx #加软链接
 /software/nginx/sbin/nginx -t 语法检查；  ./nginx启动服务  ps -ef |grep nginx #进程检查   反查端口:lsof -i :80  netstat -lnt|grep 80  #80是否存在    grep html nginx.conf
 4.作为服务启动：/usr/lib/systemd/system创建nginx.service；测试配置：systemctl start nginx; 设置开机启动：systemctl enable nginx   systemctl日志：journalctl -f跟踪日志 -u 服务名 -n尾部10行 
 
```

```
[Unit]
Description=nginx
After=network.target
  
[Service]
Type=forking
ExecStart=/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf 
ExecReload=/usr/local/nginx/sbin/nginx -s reload
ExecStop=/usr/local/nginx/sbin/nginx -s quit   #用自己的nginx文件路径
PrivateTmp=true
  
[Install]
WantedBy=multi-user.target

```

[聊聊mysql的cmake方式](https://www.php.cn/mysql-tutorials-483205.html)    [cmake安装MySQL](https://www.cnblogs.com/topass123/p/12007190.html)   [cmake安装MySQL](https://blog.csdn.net/weixin_42333370/article/details/113301378)  [cmake方式编译安装MySQL](https://blog.csdn.net/weixin_36469682/article/details/113425300)

源码Cmake方式编译安装mysql：  

```bash
1. wget mysql-5.5.32.tar.gz; cmake-2.8.8.tar.gz
2. 安装cmake，tar zxf; ./configure ; gmake;  gmake install; 查看安装是否错误：echo $?
3. 添加mysql组和用户：groupadd mysql; useradd mysql -s /sbin/nologin -M -g mysql
4. yum install ncurses-devel -y  安装devel库

5. 用cmake装mysql： tar zxf mysql;  cmake . -DCMAKE_INSTALL_PREFIX=/app
6. make; make install
```



###### a. 基于域名的虚拟主机

[Nginx目录结构](https://blog.csdn.net/Learning_xzj/article/details/124518421)    [ Nginx的目录结构](https://blog.csdn.net/javaee_gao/article/details/122639023)  [vim替换 g 和 % 区别](https://www.cnblogs.com/uangyy/p/5563158.html)  [vim中强大的g指令删除#开头或者空格#开头的行](http://www.04007.cn/article/833.html)  [vi/vim中:s命令参数分隔符](https://blog.easwy.com/archives/vim_command_parameter_separator/)  [linux vi 中s 替换方法 ](https://www.bbsmax.com/A/qVde8A085P/)   [轻松获取LAMP，LNMP环境编译参数配置](https://blog.51cto.com/oldboy/929333)


```bash
user nginx nginx;        #访问用户                      
worker_processes  8;	#启动进程					
events {
	use epoll;
    worker_connections  1024;
}
http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile        on;     
    keepalive_timeout  65;
    server {
        listen       80;     
        server_name  www.britney.org  alias.com;   #虚拟主机  别名
        location / {
            root   html;   
            index  index.html index.htm;
        }       
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;   
        }       
    }
}
```

```
1. 配置nginx.conf后，创建站点目录 (配置的是基于域名的虚拟主机)
2. 多虚拟主机配置拆分 sed -n '1,20p' nginx_vhosts.conf >blog.etian.org;主配置文件里include导入
```

###### b. 基于ip及端口的虚拟主机 (改配置文件里的虚拟主机)

配置nginx状态信息虚拟主机：显示nginx运行时的状态、连接数等信息。../../nginx     加stub_status on;

基于端口的虚拟主机：不常用，内部人员用：如页面后台、CMS发布、phpmyadmin等；只是改一下虚拟主机端口

基于ip的虚拟主机：更少用，每个ip对应自己的虚拟主机，conf里server_name域名改为ip 

```
ifconfig eth0:17 down
ifconfig eth0:196  10.0.0.196 netmark 255.255.255.0 up
ifconfig eth0:197  10.0.0.197 netmark 255.255.255.0 up
ifconfig eth0:198  10.0.0.198 netmark 255.255.255.0 up
```

```bash
vi中g(global)和%的区别：g:全局的；s/pattern/replacement/  : 替换行中出现的每一个pattern    linux中的grep = g/rep/p #全局查找出来并print
g/hello/s/abcd/1234/ 在全文中查找包含hello的行，并对这些行中的abcd替换成1234  # 如果省abcd，g/hello/s//1234/ ,这时就会把hello替换成1234。g/hello/s//1234/ === %s/hello/1234/g
g/pattern/s/pattern/replacement/g : 开始处的g是全局命令，意味着对所有与地址匹配的行进行改变。结尾处的g是一个标志，意味着改变一行上的每个。   

%:代表文件本身每一行：  % == g/.*/         #g表全局操作，还是一个末行命令    g/pattern/cmd; 查找pattern，对找到的行执行cmd命令。


g要与模式/pattern/一起使用，表示在某个范围内（一行或者整个文本）中所有与该模式匹配的部分。
g/pattern/ 意味着对所有与地址匹配的行，/pattern/ 意味着与这个地址匹配的第一行
s/pattern/replacement/ 意味着只替换行中匹配到的第一个，s/pattern/replacement/g 意味着替换行中匹配到的所有

%s/pattern/replacement == g/.*/s/pattern/replacement
g/.*/ : 对所有有任意数量的任意字符的行    % : 本文件的所有的行        

疑问：vi中s命令是替换还是参数分隔符？？？？？
```

上面3个总结：通过域名、端口、ip地址访问网页，即虚拟主机

###### c. nginx多实例架构应用 p311

nginx -h帮助 -V编译参数  -s发信号给master进程  -c指定配置文件不用默认，来实现跑多实例  

### 五、LNMP p335-433

一键部署：[ Linux + Nginx+ MySQL+ Tomcat](https://blog.csdn.net/a82793510/article/details/51685608?spm=1001.2101.3001.6650.16&utm_medium=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-16-51685608-blog-113584480.pc_relevant_paycolumn_v3&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-16-51685608-blog-113584480.pc_relevant_paycolumn_v3&utm_relevant_index=21)  [Index of / (linuxeye.com)](http://mirrors.linuxeye.com/)   [JavaWeb环境（JDK+Tmocat+Mysql+Nginx+Redis+IDEA部署](https://blog.csdn.net/coding_deliver/article/details/107146992?spm=1001.2101.3001.6650.11&utm_medium=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-11-107146992-blog-113584480.pc_relevant_paycolumn_v3&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-11-107146992-blog-113584480.pc_relevant_paycolumn_v3&utm_relevant_index=16)   [Jenkins](https://blog.csdn.net/qq_45533609/article/details/107737870)  [大数据](https://blog.csdn.net/supermapsupport/article/details/93873692?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-5-93873692-blog-107737870.pc_relevant_paycolumn_v3&spm=1001.2101.3001.4242.4&utm_relevant_index=8)  [常用一键部署脚本](https://blog.51cto.com/riverxyz/4810580)   [Docker Datacenter](https://help.aliyun.com/document_detail/55868.html)   [lnmp](https://blog.csdn.net/weixin_30174223/article/details/113584480)

架构：[ Apache Pulsar架构](https://blog.csdn.net/sun_5flower/article/details/118765265)   [三层架构](https://blog.csdn.net/weixin_49066399/article/details/109440855)  [LNMT](https://blog.51cto.com/u_12760547/2662844)  [一键部署linux+nginx+mysql+java+redis+es+ftp](https://blog.csdn.net/weixin_30174223/article/details/113584480)

Java Web系统架构：[Java Web系统架构](https://www.cnblogs.com/sjk168/p/16035713.html)  [Java架构师](https://www.cnblogs.com/sjk168/p/16035704.html)   [JavaWeb演进 ](https://www.cnblogs.com/sjk168/p/16035719.html)  [Java架构师学习](https://www.cnblogs.com/sjk168/p/16035479.html) [Spring框架](https://www.cnblogs.com/fengye/archive/2007/02/05/641118.html)  [Spring框架的前世今生](https://www.cnblogs.com/itzhoucong/p/14335584.html)

J2EE：[j2ee标准](https://baike.baidu.com/item/j2ee/110838?fr=aladdin)[ J2EE主要技术](https://blog.csdn.net/qq_42918433/article/details/110224736) [J2EE领域的技术框架结构图](https://www.yisu.com/zixun/471739.html)   [servlet](https://blog.csdn.net/weixin_33303537/article/details/115571903)  [J2EE领域的技术框架](http://dljz.nicethemes.cn/news/show-496855.html)   [Spring框架和 Spring Boot 的历史](https://www.oschina.net/news/94902/history-of-spring-framework-and-spring-boot)   [各种开源框架](https://cxybb.com/article/weixin_34337381/92031392)  [tomcat](https://baike.baidu.com/item/tomcat/255751?fr=aladdin)

微服务架构：[微服务的前世今生](https://blog.51cto.com/u_15214399/2823243)  [服务架构演进史](https://www.cnblogs.com/yssd/p/15176218.html)  

[ LNMP源码编译安装](https://blog.csdn.net/qq_43609529/article/details/107578086)  [glibc](https://baike.baidu.com/item/glibc/10058561?fr=aladdin)   [glibc内存管理精髓](https://baijiahao.baidu.com/s?id=1715600885104847188&wfr=spider&for=pc)   [Glibc标准C语言库](https://www.oschina.net/p/glibc?hmsr=aladdin1e1)   [centos7安装mysql5.7](https://blog.csdn.net/xtaypyvi123456/article/details/124685689)     [LNMT实现动静分离和负载均衡](https://blog.51cto.com/u_13858192/2170655)     [LNMT负载均衡，动静分离](https://blog.51cto.com/u_13910274/2171365) 

 [LNMP架构](https://blog.csdn.net/weixin_62466637/article/details/122391675)   [ web应用程序发展历程](https://blog.csdn.net/qq_40480474/article/details/123847134)  [Web服务器、应用程序服务器](https://zhuanlan.zhihu.com/p/93717792)   [Nginx+Java+PHP](http://t.zoukankan.com/wawahaha-p-4712270.html)  [随着微服务（服务化）的盛行，php是否势必会越来越衰颓](https://www.zhihu.com/question/392233455/answer/1223105460)   [搭建基于 LNMP 和 JAVA 环境的服务](https://www.jianshu.com/p/ca7c7fb4be89?tdsourcetag=s_pctim_aiomsg)    

架构图： [LAMT架构图](https://www.cnblogs.com/keep-going2099/articles/7048508.html)     [lnmp架构图](https://blog.csdn.net/givenchy_yzl/article/details/115691371)   [企业架构](https://www.icode9.com/content-4-930290.html)    [ 架构](https://www.cnblogs.com/xuexiaosong/p/13528007.html)   [J2EE流行框架架构图](https://www.docin.com/p-700931836.html)  [ 微服务架构图](https://blog.csdn.net/admans/article/details/124702463)  [Web集群实现共享存储的架构演变及MogileFS](https://dude6.com/article/34051.html)  

```
Java Web系统架构、java架构师、
J2EE:用 Java 技术开发企业级应用的工业标准,Servlet是java平台上的CGI技术。Servlet在服务器端运行，动态地生成Web页面。
servlet是一个Java类,狭义的Servlet是指Java语言实现的一个接口，广义的Servlet是指任何实现了这个Servlet接口的类,主要功能是承载网络连接，业务逻辑处理，比如一些编码格式的转换、登录拦截等。

Spring 是一个开源框架，是为了解决企业应用程序开发复杂性而创建的。框架的主要优势之一就是其分层架构，分层架构允许您选择使用哪一个组件，同时为 J2EE 应用程序开发提供集成的框架。
j2ee领域框架：spring、ibatis、struts1、struts2、Hibernate、j2ee架构、oracle架构

JSP最好的组合就是j2EE+Tomcat+mysql；  lnm+tomcat, Tomcat处理动态请求;
```

```
javaweb演进：
1.纯jsp / jsp+Servlet / jsp+JavaBean+Servlet
2.MVC / MVP / 三层架构
3.使用EJB进行分布式应用的开发，EJB是重量级框架，在使用上比较复杂和麻烦
4.由于EJB太重了，于是Spring应运而生，但是Spring在发展上越来越臃肿，所以还是有许多繁琐的配置
5.同样的由于String配置太繁琐，于是Spring boot诞生了，这时就可以体验到 “约定大于配置” 的乐趣
```



```
LNMP架构图：用户发起http请求，请求被Nginx处理，如果是静态请求Nginx直接返回，如果是动态请求Nginx则通过fastcgi协议转交给后端的PHP处理。

```

```
web服务器：IIS、Apache、nginx、Tomcat
应用程序服务器：Weblogic、WebSphere

应用服务器为客户端应用程序提供可调用的方法（应用程序提供(serves)商业逻辑）；以javaEE为例，Web服务处理静态页面和作为Servlet容器，解释和执行servlet/jsp，而应用服务器运行业务逻辑；
Apache经常与Tomcat配对使用。对HTML页面具有强大的解释能力，但不能解释脚本代码（JSP/Servlet）；
Tomcat处理动态请求; 早期的Tomcat是一个嵌入Apache内的JSP/Servlet解释引擎，Apache+Tomcat就相当于IIS+ASP， 后来Tomcat不再嵌入Apache，Tomcat进程独立于Apache进程。 而且，Tomcat已经是一个独立的Servlet和JSP容器，业务逻辑层代码和界面交互层代码可以分离了。因此，有人把Tomcat叫做轻量级应用服务器。
Tomcat是Servlet和JSP容器（运行它们），omcat处理静态HTML的能力不如Apache；

Weblogic、WebSphere因为能提供强大的J2EE功能，毫无疑问是绝对的应用服务器

Apache对Java的支持很灵活，它们的结合度也很高，例如Apache+Tomcat和Apache+resin等都可以实现对Java应用 的支持。Apache一般采用一个内置模块来和Java应用服务器打交道，
Nginx在配合Java应用服务器方面，耦合度很低，它只能通过自身的反向代理功能来实现与Java应用服务器的支持。但这恰恰是Nginx的一个优点，耦合度的降低，可以使Nginx与Java服务器的相互 影响降到最低。

J2EE主要技术：servlet、JSP、JDBC、EJB；  J2EE是一套针对企业级分布式应用的计算环境。它定义了动态Web页面功能（Servlet和Jsp）、商业组件（EJB）、异步消息传输机制（JMS）、名称和目录定位服务（JNDI）、数据库访问（JDBC）、与子系统的连接器（JCA）和安全服务等
```

```
大型网站系统架构的演进都是随着业务增长不断演进，所有的出发点都是为了满足业务需求。最初访问量下，功能简单时，单体软件可以解决所有问题；后来访问量逐渐增大，功能愈加丰富，此时单体软件的架构逐渐成为开发和运维的瓶颈。所以微服务拆分，集群化部署，消息中间件，内存数据库，数据库中间件等解决方案逐渐走进视野。
```

##### 1.mysql

###### a. mysql安装

```bash
开源软件版本：rc内部测试版  beta公开测试 rc(Release Candidate（候选版本）)  stable稳定版
商用软件版本：RTM工厂版  oem厂商定制版  eval评估版    rtl零售版   rtw网络分发
mysql-5.1.70.tar.gz 常规编译安装；   mysql-5.1.70-linux-x86_64-glibc23.tar.gz解开包直接用；       #glibc是GNU发布的libc库，即c运行库。glibc是linux系统中最底层的api，几乎其它任何运行库都会依赖于glibc。
mysql-5.5.32.tar.gz  cmake方式编译安装
```

[ MySQL 5.6 ,5.7 ,8.0在安装部署的异同](https://blog.csdn.net/Jsben/article/details/105699506?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-4-105699506-blog-110861146.pc_relevant_paycolumn_v3&spm=1001.2101.3001.4242.3&utm_relevant_index=7)    [mariaDB替代mysql](https://baike.baidu.com/item/mariaDB/6466119?fr=aladdin)     [linux编译安装mysql5.1.x  ](https://www.cnblogs.com/achengmu/p/9485117.html)  [MySQL5.7修改数据目录位置](https://baijiahao.baidu.com/s?id=1721277808279676209&wfr=spider&for=pc)   [MYSQL5.5编译安装](https://www.bianchengquan.com/article/340965.html) [linux编译安装mysql5.1.x](https://www.cnblogs.com/achengmu/p/9485117.html)    [MySQL8.0.23](https://zhuanlan.zhihu.com/p/370585453)   [centos7平台安装MySQL](https://zhuanlan.zhihu.com/p/31296214)  [centos7平台安装MySQL](https://zhuanlan.zhihu.com/p/31296214)   [MySQL DBA数据库工程师](https://www.bilibili.com/video/BV1Co4y1o7He?p=88)  

[Mysql用户密码管理](https://blog.csdn.net/jingde528/article/details/121974444)  [MySQL用户密码](https://baijiahao.baidu.com/s?id=1712229959772649208&wfr=spider&for=pc)

```bash
mysql-5.1.72安装：
1. 先建mysql账号：groupadd mysql ;     useradd  -s /sbin/nologin  -g  mysql -M mysql  #s禁止该用户登录，g属于mysql组，M不创建用户家目录
2. make install后ln软链接
3. 配置文件：mysql-5.1.72/support-files/*.cnf
4. 创建mysql数据库 （初始化数据库）
mkdir -p /application/mysql/data  		#mysql存数据目录 
chown -R mysql /application/mysql 		#授权mysql用户访问mysql安装目录
/application/mysql/bin/mysql_install_db --basedir=/application/mysql  --datadir=/application/mysql/data --user=mysql  #安装初始化mysql数据库文件
5.启动mysql
mysql-5.1.72/support-files/下有启动脚本，mysql.server  cp到/application/mysql/bin下面。
改脚本权限chmod 755,脚本启动要有权限；默认端口3306
传统方法启动p336：cp /mysql/bin/mysql.server  /etc/init.d/mysqld  #拷到启动目录改名； 通过/etc/init.d/mysqld start启动； chkconfig mysqld on设为开机启动 chkconfig --list mysqld;   放vi /etc/rc.local做成自启动，/etc/init.d/nfs start
```

```bash
mysql-5.7.36安装：1. 删除mariadb; yum list installed | grep mariadb;  yum -y remove mariadb-libs.x86_64 或  rpm -e --nodeps mariadb-libs.x86_64   2. 配置my.cnf;  3. 初始化： mysqld --initialize-insecure； 4.启动服务、登录
```

```
默认数据目录：/var/lib/mysql  .sock;   log:/var/log/mysqld.log
出现权限错误：把数据目录root用户换成mysql用户
```

```
my.cnf配置：[client]客户端配置；  [mysql]mysql命令行配置；  [mysqld]服务端配置； [mysqldump];  [mysqlhotcopy]; [mysqld_safe]
```

[MySQL-配置文件my.cnf参数优化详解](http://blog.itpub.net/31397003/viewspace-2647250/)     [my.cnf详解](https://www.cnblogs.com/netflix/p/15093183.html)  [socket错误](https://blog.csdn.net/ichen820/article/details/120264679)  [socket错误](https://blog.csdn.net/hjf161105/article/details/78850658?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2~default~CTRLIST~default-1-78850658-blog-119839404.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2~default~CTRLIST~default-1-78850658-blog-119839404.pc_relevant_default&utm_relevant_index=1)   [ socket](https://blog.csdn.net/wy20210818/article/details/119839404)

###### b. mysql命令

[TransactSQL帮助中SQL语法](http://t.zoukankan.com/jshchg-p-1751509.html)   [MySQL5.1参考手册 ](http://shouce.jb51.net/mysql/)   [MySQL8官方中文参考手册](http://www.java1234.com/a/javabook/database/2021/0904/21001.html)  [MySQL :: MySQL 5.7 Reference Manual :: Preface and Legal Notices](https://dev.mysql.com/doc/refman/5.7/en/preface.html)   [MySQL最新手册教程](https://www.php.cn/course/37.html)

```mysql
大写:Transact-SQL 关键字;    斜体: Transact-SQL 语法中用户提供的参数。
[]:可选，不必键入方括号；     {}： 必选，不要键入大括号。
加粗： 数据库名、表名、列名、索引名、存储过程、实用工具、数据类型名，以及必须按所显示的，原样键入的文本。
<标签> ::= 语法块的名称。此规则用于对可在语句中的多个位置使用的过长语法或语法单元部分进行分组和标记。适合使用语法块的每个位置由括在尖括号内的标签表示：<标签>。

show databases;  select user()看用户；quit; 用户登录mysql -uroot -p'pwd'；改密码：mysqladmin -u root password 'aaa' ；show variables like '%dir%';
帮助: help contents； \c ;清理多余用户:help drop user; select user,host from mysql.user  #mysql库user表，user\host列；  drop user ''@'host';   有大写的删不掉，去表中删：delete form mysql.user where user="" and host="CCC";  刷新权限：flush privileges；

```

#####  2.PHP

 [centos 7装php7.3  PHP中文网](https://www.php.cn/php-ask-485334.html)    [centos/RHEL 7.6 使用yum安装php7.3](https://www.shuzhiduo.com/A/RnJWZGQozq/)  [libxml的使用](https://www.cnblogs.com/fire909090/p/6798136.html)  [libiconv](https://blog.csdn.net/p1279030826/article/details/110789783)  [libxml安装](https://www.cnblogs.com/timecode-2011/articles/2251329.html)   [yum安装PHP](https://www.cnblogs.com/mrjiang-test/p/13407194.html)  [用yum方式安装php](https://blog.csdn.net/weixin_52270081/article/details/118915209)  [CentOS7安装PHP](https://www.cnblogs.com/-wei/p/15222477.html)  [PHP: Downloads](https://www.php.net/downloads)   [通用网关接口CGI](https://baike.baidu.com/item/通用网关接口/3351606?fromtitle=fastcgi&fromid=10880685&fr=aladdin)  [CGI架构](https://zhuanlan.zhihu.com/p/246268005)  [PHP-FPM作用](https://www.php.cn/php-weizijiaocheng-455614.html)    [搜php73模块](https://blog.csdn.net/weixin_34409903/article/details/115633334)   [centos7搭建php7.3服务](https://blog.csdn.net/weipaiyizhan/article/details/121098994)  [centos 7.3 安装 php7.3 运行环境 - ](https://www.cnblogs.com/coding8832/p/14469906.html)    [CentOS7安装PHP ](https://www.cnblogs.com/-wei/p/15222477.html)

[centos配置epel和remi源 ](https://www.cnblogs.com/cblx/p/10481588.html) [php remi源](https://zhuanlan.zhihu.com/p/355992730)   

一键安装生产环境nginx，一键配置优化生产环境，

```
php-fpm:管理fast-cgi，管理启动一个master进程和多个worker进程的程序
```



```
1. 检查mysql、nginx是否安装；netstat -lntup|grep -E '80|3306'； 

2. php安装依赖库：rpm -qa zlib libxml libjpeg freetype libpng gd curl libiconv zlib-devel libxml2-devel libjpeg-devel freetype-devel libpng-devel gd-devel curl-devel  
安装： tar zxvf;   ./configure --prefix=/usr/local/libiconv;  make ; make install
安装libmcrypt库、mhash加密扩展库

3. 安装php
tav zxvf;  ./configure;  配置/etc/php.ini  php-fpm.conf.default(fastcgi)  php -v  安装php7.3模块： yum --enablerepo=remi-php73 install php-xml php-soap php-xmlrpc php-mbstring php-json php-gd php-mcrypt
搜索PHP 7.3的所有模块：yum --enablerepo=remi-php73 search php | grep php73
5. 对apache来讲，php没进程，只是一个模块；对nginx要用fastcgi来跑，php有进程。
6. wordpress是php和mysql的开源博客；
```

### 六、mysql语言学习

##### 1、分类  p363：包括6个部分

> 1. 查询DQL：select、where、order by、group by、having等
> 2. 数据操作DML：insert、update、delete等，增、删、改表中的行
> 3. 事物处理TPL：确保被DML语句影响到表得到更新，bgein transaction、commit、rollback等
> 4. 数据控制DCL：grant、revoke等，获得许可，确定用户和用户组对数据库对象的访问
> 5. 数据定义DDL：creat、drop等，创建、删除表、为表加索引等
> 6. 指针控制CCL：declare cursor，fetch into、update where current等，用于对一个或多个表单独行操作。

实际没这么细，常这么分类：

> 1. DDL：数据定义，create、alter、drop
> 2. DML：数据操作,select、insert、delete、update
> 3. DCL：数据控制，grand、revoke、commit、rollback

##### 2、命令

```
help create database;
```

```
创建数据库、删db、连接db、授权用户
建表、索引、表操作、插入数据、查询等
```

p382：mysql带 -e 实现非交互式对话：可以不用登录做mysql的配置操作；

mysql --help |less； mysql   -usystem   -poldboy123   -e 'show databases;'

##### 3、mysql多实例、

##### 4、主从复制、主从同步

基于mysql多实例，用2台mysql服务器去做也可以；

[DB各种同步方案](https://blog.csdn.net/weixin_39940770/article/details/113262974)   [DB各种同步方案](https://www.cnblogs.com/cnxy168/p/11653962.html)   [MySQL主从复制](https://www.cnblogs.com/shenjianping/p/13605511.html) 

##### 5、Mysql存储引擎

mysql5.5默认storage engine是innoDB、5.5以前默认存储引擎是MyISAM；mysql可同时使用多种存储引擎，每种存储引擎和mysql之间通过插件的方式使用。

[MySQL体系结构与存储引擎 ](https://www.cnblogs.com/Sungeek/p/12202605.html)    [MySQL—InnoDB存储引擎体系架构](https://blog.csdn.net/lki_suidongdong/article/details/119717969)   [Mysql的各种存储引擎](https://blog.csdn.net/KaiKaiWaWa/article/details/123318199)  [ mysql连接多个存储存储](https://blog.csdn.net/weixin_33215370/article/details/113142744)  [Mysql存储引擎概念特点介绍及不同业务场景选用依据 ](https://www.cnblogs.com/pangguoping/p/5577270.html)   

### 七、shell编程

[shell](https://www.bilibili.com/video/BV1RY411H7pd?spm_id_from=333.337.search-card.all.click)    [shell教程](https://www.bilibili.com/video/BV19Q4y1m72Z?p=42)   [Linux三剑客grep、sed、awk](https://www.bilibili.com/video/BV1Kg411g7bC/?spm_id_from=333.788.recommend_more_video.4)    [shell ](https://www.bilibili.com/video/BV1XA4y1S7r1?spm_id_from=333.337.search-card.all.click) [Linux 运维](https://www.bilibili.com/video/BV1gE411W71j?spm_id_from=333.337.search-card.all.click)  [shell脚本编程](https://www.bilibili.com/video/BV1ih41127yK?spm_id_from=333.337.search-card.all.click)

##### 1、概述 p434 

Bash语法、Bash各种规则、Base编程潜规则

三剑客命令：grep、sed、awk、find

**`书写脚本:1、拆解：问题拆解为小步骤;  2、根据每个步骤写伪代码(中文) 3、根据伪代码，写shell脚本；`**

脚本规则：1、首行#!bin/bash 2、开头加版权信息(3w1h谁/什么时候/用来干嘛) 3、费曼学习法：概念-讲给别人-回顾总结-简化

##### 2、命令

[Linux中引号](https://blog.51cto.com/prepared/3116112) [wc -l](https://blog.csdn.net/weixin_41092791/article/details/100525847)      

```
运行shell脚本3方法：a、加执行权限，相当于一个命令，chmod +x ./test.sh使可执行； ./test.sh相对路径执行； #告诉系统，在当前目录找test.sh;写成test.sh,系统会去PATH找，找不到。 脚本第一行：#!/bin/bash (告诉系统脚本需要什么解释器来执行，即使用哪一种 Shell)
b、作为解释器参数(sh常用 )：直接运行解释器，参数就是脚本名：/bin/sh test.sh    /bin/php test.php;这种方式运行的脚本，不需要在第一行指定解释器信息，写了也没用。
c、让变量生效命令，source或.在当前环境执行一次脚本（类似include功能，比如nginx把每个站点配置文件包含进来）
```

```
file a.cnf 查看文件类型    一个英文字符等于一个字节(8位，不分大小写)
#!/bin/bash 指定脚本使用的命令解释器（幻数）；
双引号可以保留变量内容，而单引号仅能是一般字符； name=bill, echo "$name"; 反引号中的内容会先执行，执行的结果将作为外部的输入信息。 wc -l `locate crontab` ；  head `which yum`  
wc输出每个指定文件的行数、单词计数和字节数; which在环境变量$PATH设置的目录里查找文件;
```

```
#!/bin/bash
#想来点颜色，在 /etc/init.d/functions,就要把文件放在本脚本中（包含进来，用source命令）
source /etc/init.d/functions
action "web is ok"  /bin/true  #因为把颜色文件包含进来了，就能用action
```

##### 3. 变量、

###### a、（环境、普通）变量、特殊变量

变量命名规则：不能数字开头、多个单词中间_连接、驼峰命名(开头小写)

变量分类：环境变量(全局变量)、普通变量(局部变量)、特殊变量(十几个)：匹配脚本参数、服务状态、特殊替换

```
重定向：标准输入(stdin):文件描述符0； 输出（stdout）：1； 错误（stderr）：2
查看环境变量：env、declare、export；grep UID *;  改密码：echo 1234|passwd --stdin root; 历史配置文件:~/.bash_history（当前用户家目录）; HISTSIZE、HISTFILESIZE、HISTFILE；history -c清除；
修改环境变量加export:export HISTCONTROL=ignorespace,空格开头的命令不记录到历史记录；TMOUT:不操作自动断开登录时间；存放的命令/脚本会在下一个命令执行前运行：PROMPT_COMMAND=data；
设置和取消环境变量：export/unset；永久修改：etc/profile  变量取值：${week}day
```

与变量有关的文件：etc/profile(存环境变量、别名)、etc/bashrc(官方要求放别名和函数的地方)、～/.bashrc(当前用户别名)、～/.bash_profile(当前用户环境变量)、/etc/profile.d/xxx.sh用户登录后执行这个目录下以.sh结尾的脚本

###### b、特殊变量传参

更方便的判断服务、文件、进程等状态  [伪代码](https://baike.baidu.com/item/伪代码/10321865?fr=aladdin)  [伪代码](https://lulaoshi.info/blog/k-means-iris-dataset)  [JavaScript(JS)逆向](https://blog.csdn.net/PZ0605/article/details/123925416) [特殊变量](https://blog.csdn.net/weixin_34764432/article/details/124229607)  [Typora页面美化](https://blog.csdn.net/a2352159950/article/details/108153531?spm=1001.2101.3001.6650.7&utm_medium=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~default-7-108153531-blog-120435457.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~default-7-108153531-blog-120435457.pc_relevant_default&utm_relevant_index=9)  [typora美化](https://blog.csdn.net/qd2013498006/article/details/120435457)

| 符号                                         | 含义                                             | 应用                                                     |
| :------------------------------------------- | :----------------------------------------------- | -------------------------------------------------------- |
| <span color=red>$0</span>                    | 脚本的名字                                       | 脚本执行错误，给出错误提示或帮助                         |
| <span style='color:red'>**$n(n数字)**</span> | 脚本的第几个参数(命令行传参)                     | 把脚本参数传递给脚本(把命令行中的内容通过$n传递到脚本中) |
| $#                                           | 脚本参数的个数，一共几个参数                     | 脚本开头，判断参数是否正确（判断是否使用参数：0没使用）  |
| $*                                           | 取出脚本所有参数：加双引号相当于一个整体一个参数 | 循环或者数组                                             |
| $@                                           | 取出脚本所有参数：加双引号每个参数独立           | 循环或者数组                                             |

echo \${0..12}显示脚本中\$1到\$12多个脚本参数。   帮助：man bash  找special parameters

状态：$?上条命令/脚本的返回值（判断执行是否成功）；\$\$当前运行脚本的pid；\$!上一个运行脚本的pid；\$_上一个命令或脚本的最后1个参数（esc .）；

变量子串：${xxx}；帮助：man bash=>parameter expansion

```
变量赋值：1、直接赋值 old=666; 2、引用其它命令结果赋值 ip=\'ls'\ 3、交互式变量赋值 read -s不显输入信息 -t超时时间 -p指定输出  4、脚本传参 $1 $2
```

##### 4、运算符

<span style='color:greenyellow;font-size:20px'>**equal、not equal、greater（大于Great than）、g+e大于等于、 less than小于、le小于等于**</span>

&&前1个命令执行 成功再执行后面的命令；||前一个失败再执行后面； expr 2 + 2；   

使用 printf 的脚本比使用 echo 移植性好，加\n换行；  test检查条件是否成立

运算方式：1、echo $((1+2))       2、let  1+2      3、expr      4、bc：   echo 9/6 |bc      5、\$[] ：    echo \$[1/3]       6、awk

原生bash不支持简单的数学运算，但是可以通过其他命令来实现，例如 awk 和 expr，expr 最常用

##### 5、条件/循环语句

```bash
终端：if [condition]; then cmd ;else cmd;  fi     #if else 经常与 test 命令结合使用;
多分支：if 条件1； then cmd1;   elif 条件2；then cmd2;   else cmd; fi

case：	case 分支右圆括号开始，两个分号 ;; 表示 break，即执行结束，跳出整个 case ... esac 语句，esac作为结束标记。取值后面必须为单词 in；  case $aNum in

```

```bash
for： 	for var in item1 item2 ...; do cmd1; cmd2…    done;
while:	 while 条件； do cmd  done     #变量计算中不需要加 $ 来表示变量，<Ctrl-D>结束循环
无限循环：while true;  do cmd  done   或者   for (( ; ; ))
until: 	 until 条件；  do cmd  done

break跳出所有循环、continue跳出当前循环
```

##### 6、数组

```bash
重定向：command << EOF  （将EOF之间内容作为输入传给cmd）
定义：array_name=(value0 value1 value2 value3)     #空格隔开，括号表数组
读取：${数组名[下标]}； echo ${array_name[@]}  #@或*获取所有元素
```

##### 7、函数

```bash
[ function ] funname [()]      #可以function fun() 定义，也可以fun() 定义,不带任何参数。
{
    action;
    [return int;]
}    #参数返回，可以显示加：return 返回，不加，以最后一条命令结果，作为返回值。 return后跟数值n(0-255)
```

##### 8、文件包含

包含外部脚本，source或.在当前环境执行一次脚本（类似include）；被包含的文件 不要可执行权限

```
. filename   # 注意点号(.)和文件名中间有一空格
或
source filename
```

### 八、LVS集群

##### 1、概述 p554

2、

### 九、高可用

### 十、redis持久化
