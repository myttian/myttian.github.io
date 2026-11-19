安装MySQL

**这里建议大家使用压缩版,安装快,方便.不复杂.**

# 1、MySQL软件下载

mysql5.7 64位下载地址:

https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.19-winx64.zip

电脑是64位的就下载使用64位版本的！



# 2、MySQL安装步骤



1、下载后得到zip压缩包.

2、解压到自己想要安装到的目录，本人解压到的是D:\Environment\mysql-5.7.19

3、添加环境变量：我的电脑->属性->高级->环境变量

```
选择PATH,在其后面添加: 你的mysql 安装文件下面的bin文件夹
```

4、编辑 my.ini 文件 ,注意替换路径位置

```
[mysqld]
basedir=D:\Program Files\mysql-5.7\
datadir=D:\Program Files\mysql-5.7\data\
port=3306
skip-grant-tables
```

5、启动管理员模式下的CMD，并将路径切换至mysql下的bin目录，然后输入mysqld –install (安装mysql)

6、再输入  mysqld --initialize-insecure --user=mysql 初始化数据文件 启动MySql 服务 

```
net start mysql
```

7、然后再次启动mysql 然后用命令 mysql –u root –p 进入mysql管理界面（密码可为空）

8、进入界面后更改root密码

```
update mysql.user set authentication_string=password('123456') where user='root'and Host = 'localhost';
```

9、刷新权限

```
flush privileges;
```

10、修改 my.ini文件删除最后一句skip-grant-tables

11、重启mysql即可正常使用

```
net stop mysql
net start mysql
```

12、连接上测试出现以下结果就安装好了

# 3、MySQL卸载

```
sc delete mysql
```



# 4、MySQL常用命令

> 连接数据库

打开MySQL命令窗口

- 在DOS命令行窗口进入 **安装目录\mysql\bin**
- 可设置环境变量，设置了环境变量，可以在任意目录打开！

**连接数据库语句 :** mysql -h 服务器主机地址 -u 用户名 -p 用户密码

注意 : -p后面不能加空格,否则会被当做密码的内容,导致登录失败 !

**几个基本的数据库操作命令 :**

```sql
update user set password=password('123456')where user='root'; 修改密码
flush privileges; 刷新数据库
show databases; 显示所有数据库
use dbname；打开某个数据库
show tables; 显示数据库mysql中所有的表
describe user; 显示表mysql数据库中user表的列信息
create database name; 创建数据库
use databasename; 选择数据库

exit; 退出Mysql
? 命令关键词 : 寻求帮助
-- 表示注释
```

# 5、MySQL常用的图形化管理工具(DBMS）

#### 1. 前言

MySQL是一个非常流行的小型关系型[数据](http://www.fly63.com/)库管理系统。目前MySQL被广泛地应用在Internet上的 中小型[网站](http://www.fly63.com/)中。由于其体积小、速度快、总体拥有成本低，尤其是开放源码这一特点，许多中小型[网站](http://www.fly63.com/)为了降低[网站](http://www.fly63.com/)总体拥有成本而选择了MySQL作为[网站](http://www.fly63.com/)[数据](http://www.fly63.com/) 库。

要管理 MySQL [数据](http://www.fly63.com/)库服务器，不妨来试试以下这些或具有 Web 界面、或拥有[前端](http://www.fly63.com/)界面、或包含 GUI 界面的[工具](http://www.fly63.com/tool)，使用它们自会为你省力不少。



#### 2. [php](http://www.fly63.com/tag/php)MyAdmin

官方网址：http://www.[php](http://www.fly63.com/tag/php)myadmin.net

[php](http://www.fly63.com/tag/php)MyAdmin是最常用的MySQL维护[工具](http://www.fly63.com/tool)，是一个用[php](http://www.fly63.com/tag/php)开发的基于Web方式架构在[网站](http://www.fly63.com/)主机上的MySQL管理[工具](http://www.fly63.com/tool)，支持中文，管理[数据](http://www.fly63.com/)库非常方便。不足之处在于对大[数据](http://www.fly63.com/)库的备份和恢复不方便。



#### 3. MySQLDumper

官网网址：http://www.mysqldumper.de/en

MySQLDumper使用[php](http://www.fly63.com/tag/php)开发的MySQL[数据](http://www.fly63.com/)库备份恢复程序，解决了使用[php](http://www.fly63.com/tag/php)进行大[数据](http://www.fly63.com/)库备份和恢复的问题，数百兆的[数据](http://www.fly63.com/)库都可以方便的备份恢复，不用担心网速太慢导致中间中断的问题，非常方便易用。这个软件是德国人开发的，还没有中文语言包。



#### 4. Navicat

官方[网站](http://www.fly63.com/)：http://www.navicat.com

Navicat是一个桌面版MySQL[数据](http://www.fly63.com/)库管理和开发[工具](http://www.fly63.com/tool)。和微软SQLServer的管理器很像，易学易用。Navicat使用图形化的用户界面，可以让用户使用和管理更为轻松。支持中文，有免费版本提供。



#### 5. MySQL GUI Tools

官方网址：http://dev.mysql.com/downloads/gui-tools/

MySQL GUI Tools是MySQL官方提供的图形化管理[工具](http://www.fly63.com/tool)，功能很强大，值得推荐，可惜的是没有中文界面。



#### 6. MySQL ODBC Connector

官方网址：http://dev.mysql.com/downloads/connector/odbc

MySQL官方提供的ODBC接口程序，系统安装了这个程序之后，就可以通过ODBC来访问MySQL，这样就可以实现SQLServer、Access和MySQL之间的[数据](http://www.fly63.com/)转换，还可以支持ASP访问MySQL数据库。



#### 7. SQLyog

官方网址：https://www.webyog.com

SQLyog是业界著名的Webyog公司出品的一款简洁高效、功能强大的图形化MySQL数据库管理[工具](http://www.fly63.com/tool)。使用SQLyog可以快速直观地让您从世界的任何角落通过网络来维护远端的MySQL数据库。

SQLyog相比其它类似的MySQL数据库管理[工具](http://www.fly63.com/tool)其有如下特点:

1、基于C++和MySQLAPI编程；

2、方便快捷的数据库同步与数据库结构同步[工具](http://www.fly63.com/tool)；

3、易用的数据库、数据表备份与还原功能；

4、支持导入与导出XML、[html](http://www.fly63.com/tag/html)、CSV等多种格式的数据；

5、直接运行批量SQL脚本文件，速度极快；

6、新版本更是增加了强大的数据迁

应用平台： Win2003/XP/2000/9X/linux/unix





#### 8. 总结

mysql的GUI界面软件很多，建议都试用一下，适合自己的才是最好的。如果懒得折腾，就直接使用[php](http://www.fly63.com/tag/php)MyAdmin



> 引用至 小狂神的分享 https://mp.weixin.qq.com/s/E1PM4EHwU6Joot4OG0gDjw