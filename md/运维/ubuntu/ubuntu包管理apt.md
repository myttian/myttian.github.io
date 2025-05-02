# apt

[apt命令](https://www.runoob.com/linux/linux-comm-apt.html)  [apt](https://baike.baidu.com/item/apt/20109246?fr=ge_ala)  [apt-cache](https://blog.csdn.net/feiying0canglang/article/details/128179026)  [apt-get](https://www.cnblogs.com/ylxtiankong/p/14637333.html) 

[apt-get、dpkg常用命令](https://www.cnblogs.com/dgp-zjz/p/12886340.html) [apt-cache](https://blog.csdn.net/feiying0canglang/article/details/128179026)  [Ubuntu](https://blog.csdn.net/qq_44379042/article/details/122838310) 

[apt update、apt upgrade和apt full-upgrade三个命令的区别](https://blog.csdn.net/liweiweili126/article/details/138211514)  [apt-get和apt-cache命令的原理](https://www.zhihu.com/question/41639127/answer/2276801192) 

[apt详解](https://blog.csdn.net/weixin_44063383/article/details/136579089) 

安装：[apt安装的软件包位置](https://blog.csdn.net/qq_31477905/article/details/132084005)  [apt-get](https://blog.csdn.net/u014470361/article/details/84948020) 

删除：[删除/卸载软件包](https://blog.csdn.net/LEON1741/article/details/85114318)  [Linux五种清理系统垃圾的方式](https://blog.csdn.net/u013541325/article/details/123932803) [卸载清理](https://blog.51cto.com/u_15672212/5381642)  [清理垃圾](https://www.cnblogs.com/aididiao/p/14840891.html)  

报错：[安装deb包](https://blog.csdn.net/weixin_49505963/article/details/136135321)

```sh
dpkg -i package_name.deb				#安装本地deb包
apt-cache madison nginx					# 列出包的所有来源
apt-cache policy  kubeadm				# 比apt-cache madison详细，是否安装，已安装优先级100
apt-cache showpkg  kubeadm				# 包信息，常规、正反向依赖关系等

apt-cache stats							# 相关统计信息
apt-cache pkgnames mysql				# 列出所有软件包
apt-show-versions  -a nginx				# 列出所有版本，查看是否安装

apt search nginx --full					# 查找包，支持正则，详细信息
apt download nginx						# 下载包
apt source nginx						# 下载源代码
apt list --installed |grep zstd			# 已安装的包
apt list --all-versions					# 已安装包版本
apt show nginx							# 包信息
apt update nginx						# 更新包
apt upgra
apt full-upgra
apt list --upgradeable					# 列出可更新的包

apt clean								# /var/cache/apt/archives
apt autocle
apt remove mplayer						# 删包,不删依赖，保留配置
apt autoremove							# 慎用：清理不再使用的依赖和库文件
apt purge nginx							# 移除包及配置
dpkg -L nginx							# 查看包安装位置
dpkg -S nginx							# 文件属于哪个已安装的包

apt install -s							# 模拟安装，只模拟执行命令，不实际安装
apt insatll mplayer --only-upgrade		# 只升级，若不存在就不安装
apt install mplayer --no-upgrade		# 安装包，但不想升级
apt insatll mplayer=1					# 安装指定版本
apt-get install --reinstall initramfs-tools		# 重新安装
apt-get build-dep nginx					# 安装相关编译环境
apt showsrc nginx						# 查看源码包信息

apt-cache depends nginx					# 该包需要哪些依赖包
apt-cache rdepends 						# 该包被哪些包依赖
apt-get check							# 检查依赖，是否有损坏的依赖
```

## apt配置

[apt配置](https://blog.csdn.net/u013390088/article/details/81984965)   [Linux开发环境配置](https://blog.csdn.net/cclethe/article/details/126336644)  [/etc/apt/apt.conf.d/文件作用](https://blog.csdn.net/Dontla/article/details/122863715)  [apt.conf.d目录文件_百度搜索](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=apt.conf.d%E7%9B%AE%E5%BD%95%E6%96%87%E4%BB%B6&rn=20&oq=%252Fapt.conf.d&rsv_pq=c51cffa5001d8d8f&rsv_t=84d3n1rOn5E3y54hrrm04EBLigdeX2bExxUPXBU2zFbJIMo3kCxj%2F7G8%2BIs&rqlang=cn&rsv_enter=1&rsv_dl=tb&rsv_sug3=11&rsv_sug1=3&rsv_sug7=100&rsv_sug2=0&rsv_btype=t&inputT=4494&rsv_sug4=4495)  [apt配置](https://www.jianshu.com/p/fdae9cb5181b) [find命令](https://blog.51cto.com/lemidi/1370531)  [apt显示仓库中包的信息_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=apt%E6%98%BE%E7%A4%BA%E4%BB%93%E5%BA%93%E4%B8%AD%E5%8C%85%E7%9A%84%E4%BF%A1%E6%81%AF) 

`apt.conf.d`是Debian及其衍生系统如Ubuntu中APT（Advanced Package Tool）的配置文件目录

- APT用这个目录下的配置文件来确定, 如何处理软件包及其元数据
- 通常有几个文件，如`10apt`、`20archive`、`99other`等，包含不同的配置选项。名称以数字开头，以控制处理它们的顺序

```sh
# 给apt-get设置变量:  配置一个键值对，后跟一个键值对,表示设置一个键的值
apt -o Acquire::http::proxy="http://192.168.12.215:3128/" update
```

[apt-get强制使用Ipv4](https://www.cnblogs.com/huangshiyu13/p/7092677.html) 

```sh
apt-cache 
-o Acquire::ForceIPv4=1 
-o Acquire::http::Pipeline-Depth=5 
-o Acquire::BrokenProxy=true 
-o Acquire::GPGCheck=false 
-o Acquire::Check-Valid-Until=false 
-o Acquire::No-Cache=true 
-o Acquire::Source-Configuration=true 
-o Acquire::Allow-Downgrade=true 
-o Acquire::Allow-Insecure=true 
-o Acquire::Allow-Unsupported=true 
-o Acquire::Check-Date=false 
-o Acquire::Check-Valid-Until=false 
-o Acquire::GPGCheck=false 
-o Acquire::No-Cache=true 
-o Acquire::Source-Configuration=true 
-o Acquire::Allow-Downgrade=true 
-o Acquire::Allow-Insecure=true 
-o Acquire::Allow-Unsupported=true 
-o Acquire::Check-Date=false 
-o Acquire::http::No-Cache=true 
-o Acquire::http::Pipeline-Depth=5 
-o Acquire::BrokenProxy=true 
-o Acquire::GPGCheck=false 
-o Acquire::Check-Valid-Until=false 
-o Acquire::http::No-Cache=true 
-o Acquire::http::Pipeline-Depth=5 
-o Acquire::BrokenProxy=true 
-o Acquire::GPGCheck=false 
-o Acquire::Check-Valid-Until=false 
-o Acquire::http::No-Cache=true 
-o Acquire::http::Pipeline-Depth=5 
-o Acquire::BrokenProxy=true 
-o Acquire::GPGCheck=false 
-o Acquire::Check-Valid-Until=false 
-o Acquire::http::No-Cache=true 
-o Acquire::http::Pipeline-Depth=5 
-o Acquire::BrokenProxy=true 
-o Acquire::GPGCheck=false 
-o Acquire::Check-Valid-Until=false 
-o Acquire::http::No-Cache=true 
-o Acquire::http::Pipeline-Depth=5 
-o Acquire::BrokenProxy=true 
-o Acquire::GPGCheck=false 
-o Acquire::Check-Valid-Until=false 
-o Acquire::http::No-Cache=true 
-o Acquire::http::Pipeline-Depth=5 
-o Acquire::BrokenProxy=true 
-o Acquire::GPGCheck=false 
-o Acquire::Check-Valid-Until=false 
-o Acquire::http::No-Cache=true 
-o Acquire::http::Pipeline-Depth=5 
-o Acquire::BrokenProxy=true 
-o Acquire::GPGCheck=false 
-o Acquire::Check-Valid-Until=false 
-o Acquire::http::No-Cache=true 
-o Acquire::http::Pipeline-Depth=5 
-o Acquire::BrokenProxy=true 
-o Acquire::GPGCheck=false 
-o Acquire::Check-Valid-Until=false 
-o Acquire::http::No-Cache=true 
-o Acquire::http::Pipeline-Depth=5 
-o Acquire::BrokenProxy=true 
-o Acquire::G
```



## 安装

`apt` 安装的包被存储在以下默认位置

- **可执行文件**：在 /usr/bin 目录下，这是系统范围内可执行文件的主要存放位置
- **配置文件**：在 /etc 目录下，大多数软件的配置文件都会存储在这个目录中
- **库文件**：在 /usr/lib 或 /usr/lib64 目录下，这里存放了共享库文件（动态链接库）
- **文档和帮助文件**：在 /usr/share/doc 或 /usr/share/man 目录下，这里存放了软件包的文档和帮助文件

## apt源

[apt命令和源](https://cloud.tencent.com/developer/article/1728805) 

```sh
/etc/apt/sources.list		# 源站点
/var/lib/dpkg/available		# 安装源中的所有软件包,包括已安装和未安装的包
/var/cache/apt/archives		# 安装软件时，软件包临时存放路径
/var/lib/apt/lists			# 使用apt-get update会从/etc/apt/sources.list中下载软件列表，并保存到该目录
```

# 远程连接服务器开发

## vscode

[Win7安装OpenSSH](https://jingyan.baidu.com/article/48a4205741b854e82525046e.html)    [OpenSSH](https://github.com/PowerShell/Win32-OpenSSH/releases) 

[使用VSCode SSH实现公网远程连接本地服务器开发](https://blog.csdn.net/qq_53317005/article/details/132505454)    [cpolar内网穿透](https://www.baidu.com/s?ie=UTF-8&wd=cpolar%E5%86%85%E7%BD%91%E7%A9%BF%E9%80%8F) 

[VScode远程连接ssh](https://cloud.tencent.com/developer/article/2413510)  [vscode打开ssh项目_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=vscode%E6%89%93%E5%BC%80ssh%E9%A1%B9%E7%9B%AE)  [vscode 通过 ssh 连接远程服务器使用 GUI 全流程](https://zhuanlan.zhihu.com/p/698507761) 

[VSCode网页版（本地版）连接（远程）Docker容器的SSH服务 ](https://zhuanlan.zhihu.com/p/666975429) 

1. 安装openssh
2. vscode配置ssh
3. 通过内网穿透来实现在公网环境下的远程连接

**问题：** 

卡在downloading with wget： 55m，可以慢慢等它下完

[卡在downloading with wget](https://blog.csdn.net/weixin_42469354/article/details/132625615)   [vscode ssh 低网络连接](https://www.bilibili.com/read/cv29909544/) 
