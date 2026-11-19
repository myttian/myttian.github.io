# sharepoint

[微软企业级产品Sharepoint 2010实战_王进](https://www.bilibili.com/video/BV1JV411S7a6?p=2) [SharePoint Foundation和SharePoint Server的区别 ](https://www.cnblogs.com/wphl-27/p/5249465.html)   [Windows 10 镜像](https://dbmer.com/win/msdn/windows-10-fido/)

[project server 2016 ](https://www.cnblogs.com/jindahao/p/5856544.html) [使用Project客户端和Project Server进行项目管理](https://blog.csdn.net/hfahe/article/details/5742852)  [在 Microsoft Evaluation Center 试用 Project Server 2019](https://www.microsoft.com/zh-cn/evalcenter/evaluate-project-server-2019)  [Active Roles  ](https://support.oneidentity.com/zh-cn/active-roles/7.4.1/technical-documents) 

[加入AD域试图加入的域的SID与本计算机的SID相同](https://www.cnblogs.com/oscarli/p/14320103.html)  sysprep /generalize /oobe /reboot

sharepoint server 和 sharepoint server foundation(免费)  [SharePoint 2016 图文安装教程 后面有激活序列号](https://www.office26.com/sharepoint/sharepoint_7558.html)  

SharePoint 2016起就不再有Foundation版本了，大家切记。还有SharePoint Designer也只更新到2013版本，支持SharePoint 2013/2016和2019版本，同时支持SharePoint online。



[SharePoint 2019 图文安装教程 ](https://www.cnblogs.com/jianyus/p/9874010.html)

```
1. DC--域控，证书服务器  192.168.1.2
2. server1--SQL server 192.168.1.3	sysprep /generalize /oobe /reboot
3. server2--SharePoint 192.168.1.4
4. server3--Exchange   192.168.1.5
5. server4--Lync

```

sql最后建一个独立账号，因为管理员密码定期会变，域里建一个SQLAdmin，

概念：服务器场(多台sharepoint服务器集合)、管理中心、web应用程序(场里有web应用程序)、网站集(web应用程序包含网站集)等，

创建网站集，用户访问；

### 初始化和客户端访问

用配置向导初始化，很慢；

# Server 2012

[Windows Server 2012精讲系列课程（王进老师版）](https://www.bilibili.com/video/BV1ZJ411t7Sd?spm_id_from=333.999.0.0)

```
新功能：容错DHCP、NIC Team（多网卡成组）、重复数据删除、direct access(VPN)

服务器角色（Role），就是一大批程序的集合，这些程序都是围绕一个大的目标来开发，比如 IIS。
角色服务（Role），就是角色中的程序，比如 IIS 的 FTP 服务。
功能（Feature），功能也是程序，只不过微软觉得这些程序不足以“拉拢其他兄弟”形成一个集合，比如 Telnet。
```

访问共享磁盘的方式有2种，一种走IP协议：iscsi:3260,IP-SAN,一种走光纤协议：FC-SAN;iscsi发起程序(应用服务器连接后台存储[san]的接口)

[集群CLUSTER](https://www.cnblogs.com/chhuang/p/4182868.html)
文件服务器高可用：DFS、Cluster   [白话 Windows Server 的服务器角色、角色服务和功能](http://www.cftea.com/c/2018/12/11348.asp)
批量部署：WDS、MDT(wds工具包)、OSD(收费)；      [SCCM](https://www.jianshu.com/p/7686e8d95998)、[SCCM部署](https://www.jianshu.com/p/7686e8d95998)、[SCCM2019](https://www.icode9.com/content-4-893668.html)、[Microsoft System Center 2019 全系列组件](https://www.ittel.cn/archives/2823.html)

RDS:虚拟桌面

APP-V/RD APP:应用程序虚拟化：把软件装在服务器，服务器上显示软件的快捷方式，所有客户端通过虚拟化远程运行。 [App-V](https://baike.baidu.com/item/App-V/4299721?fr=aladdin)

##### P6权限管理

```
动态访问控制-通过对象属性[用户、设备、资源属性]；基于NTFS权限；adsiedit.msc
```

> 1. 启用动态访问控制DAC---组策略，gpmc.msc 管理-系统-KDC
>
> 2. 声明用户、设备、资源---活动目录管理中心
>
> 3. 创建规则---活动目录管理中心
>
> 4. 创建策略---活动目录管理中心,规则包含进策略里面
>
> 5. 发布策略---组策略，安全设置-文件系统-中心访问策略
>
> 6. 功能校验
>
>    Claim types:声明(例如部门)   Central Access Rules:规则(部门=sales)    Central Access Policy:策略，包含多个规则

##### P7存储

[Windows 8/windows server 2012中的存储池](https://www.chiphell.com/thread-831627-1-1.html)  [Windows10使用分层存储，自制混合硬盘 ](https://zhuanlan.zhihu.com/p/456602263) [Windows Server 2016 存储池和ISCSI虚拟磁盘](https://blog.51cto.com/lumay0526/2051410#先决条件)  [windows server ADAC（活动目录管理中心）](https://www.pianshen.com/article/9049452031/)  [SAN交换机与以太网交换机的区别](https://blog.csdn.net/beyond911/article/details/106063391?spm=1001.2101.3001.6650.5&utm_medium=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-5.pc_relevant_antiscanv2&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-5.pc_relevant_antiscanv2&utm_relevant_index=10)  [SAN技术及应用](https://blog.csdn.net/qq_38265137/article/details/80349383)

```
das单台服务器存储扩展，nas文件服务器，san多个应用服务器存储集中管理；
建存储池最小5g硬盘；
网络设备到域中身份验证，经过RADIUS服务器；
```

群集服务Cluster:需要域环境，共享存储(S盘存储   Q盘做仲裁，偶数盘需要)；三个网络(Public，Private、Storage)，故障转移群集

##### P21批量部署

[PXE远程安装与kickstart无人值守安装](https://blog.csdn.net/qyf158236/article/details/108574522?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_title~default-8.pc_relevant_default&spm=1001.2101.3001.4242.5&utm_relevant_index=11) [无盘网吧](https://blog.csdn.net/weixin_34221384/article/details/119554092)  [学校无盘服务器带机量50台要求,锐起XP无盘](https://blog.csdn.net/weixin_40004960/article/details/119559787?spm=1001.2101.3001.6650.2&utm_medium=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~Rate-2.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~Rate-2.pc_relevant_default&utm_relevant_index=5)

```
Boot.wim预安装阶段winpe系统，install.wim真正的系统文件
必须windows DHCP，其他dhcp不支持；wds部署服务器存储镜像，传输服务器给用户来建立连接；
```

[LDAP概念和原理介绍](https://www.cnblogs.com/wilburxu/p/9174353.html)   

无盘系统：[iscsi无盘](https://www.bilibili.com/video/av926762255)   [San Devtools 调试工具](https://www.wenjiangs.com/article/san-devtools-use.html) [无盘服务器架设之一：编译iPXE，用于网络，ISO，USB等无盘启动](https://blog.csdn.net/geleibo/article/details/82865121)  [CSDN博客](https://blog.csdn.net/geleibo/article/list)  [用ipxe网络启动打造无盘ESXi系统](https://blog.csdn.net/weixin_39582737/article/details/119437675?spm=1035.2023.3001.6557&utm_medium=distribute.pc_relevant_bbs_down_v2.none-task-blog-2~default~OPENSEARCH~Rate-6.pc_relevant_bbs_down_cate&depth_1-utm_source=distribute.pc_relevant_bbs_down_v2.none-task-blog-2~default~OPENSEARCH~Rate-6.pc_relevant_bbs_down_cate)  [使用ipxe+iscsi搭建的无盘工作站，多个终端使用同一个镜像，启动后计算机重名](https://bbs.csdn.net/topics/390807093?page=1)  [无盘服务器架设之四：iPxe无盘超级应用实例](https://blog.csdn.net/geleibo/article/details/82865283?spm=1001.2101.3001.6650.5&utm_medium=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~Rate-5.pc_relevant_aa&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~Rate-5.pc_relevant_aa&utm_relevant_index=9)  [iscsitarget+ipxe无盘启动详解](https://blog.csdn.net/wolfsun3/article/details/47722437/)

[PXE打造无盘系统ESXI配合群晖ISCSI安装教程](https://www.vediotalk.com/archives/3858)    [NewBeePE系列网启服务器](https://www.bilibili.com/video/BV1864y1z7A6?share_source=copy_web)  [超凡精简PE](http://bbs.wuyou.net/forum.php?mod=viewthread&tid=425197&extra=&page=1)  [GRUB2从入门到折腾](http://bbs.wuyou.net/forum.php?mod=viewthread&tid=420722&extra=&ordertype=1)  [一文详解SFP+与SFP、XFP的区别](http://www.elecfans.com/d/682464.html)   [安装win10系统到NAS(iscsi-uefi)无盘系统](https://www.bilibili.com/video/BV1gQ4y1i7nS/?spm_id_from=333.788.recommend_more_video.-1)  [用史上最伟大万能启动工具远程给外面的女友重装系统&不用U盘安装微软原版系统iso](https://www.bilibili.com/video/BV1Ly4y1U7aD?spm_id_from=333.999.0.0)   [史上最伟大网管-手把手教你制作免费的iscsi无盘](https://www.bilibili.com/video/av926762255)

[一键恢复CGI-plus v5.0.0.8 – 宋永志博客 (songyongzhi.com)](http://www.songyongzhi.com/cgi.html)

# Server 2012网络配置

[Windows Server 2012 R2企业级网络配置指南实战](https://www.bilibili.com/video/BV1S54y1G7Q1?p=2&spm_id_from=pageDriver)  [在线网络计算器](https://www.sojson.com/convert/subnetmask.html)  [广播地址](https://blog.csdn.net/tennysonsky/article/details/45564479) [计算机网络](https://www.cnblogs.com/qingl/p/9094406.html) [TCP/IP详解之环回接口](https://blog.csdn.net/weixin_38233274/article/details/80273375?spm=1001.2101.3001.6650.6&utm_medium=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-6.pc_relevant_paycolumn_v3&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-6.pc_relevant_paycolumn_v3&utm_relevant_index=13)  [windows服务器应对高并发和DDOS攻击](https://blog.csdn.net/qq_33974741/article/details/84465334)

广播地址：主机标识段host ID（**简称主机 ID**） 为全 1 的 IP 地址；

例如，对于10.1.1.0 （255.255.255.0 ）网段，其广播地址为10.1.1.255 （255 即为 2 进制的 11111111 ），当发出一个目的地址为10.1.1.255 的数据包时，它将被分发给该网段上的所有计算机。

路由表：用目的IP地址和路由表中的子网掩码相与，若结果出现在路由表中的目的网络中，则转发相应的下一跳，若没有出现在路由表中的目的网络中，则转发到默认站

跃点数用来选数据包走的路线； 

在链路上：表示不需要通过路由器，就能和目标ip通讯。

网络目标可以是网络id(192.168.1.0),ip地址(192.168.1.1),广播地址(192.168.1.255)，多播地址(224.0.0.0)

掩码：主要用来目标网络ip和某路由的掩码做与运算，确定目标网络的有效性

网关：如果上面与运算后，结果等于该路由的网络目标，就将数据包发送给该网关ip，如果显示‘在链路上’，表计算机可直接与目标通信，不需要通过路由器转发。

跃点数：通过此路由来发送数据包的成本，它可能代表发送速度的快慢、数据包从来源到目的地需要经过的路由器路数、此路径的稳定性等。路由跃点数=接口跃点数+网关跃点数；netsh interface ip show address;   接口跃点数:以网络接口速度来计算，100mbps/20,1gbps/10,10gbps/5;  网关跃点数默认值256，如果跃点数一样：网络连接-布局-菜单-高级设置，改上下顺序。自动检测网关是否正常：改注册表，HKEY_LOCAL_MACHINE\SYSTEM\ControlSet\Services\Tcpip\Parameters\DeadGWDetectDefault    

```
0.0.0.0 		默认路由，与运算后没有匹配的，就走这条路由；
127开头	  	   环回网络路由，测试tcp/ip协议有没问题；
192.168.1.0  	 表在这个网段上；
192.168.1.2      主机路由，发送给自己；
192.168.1.255	 直接广播路由；也称为子网广播路由；1网段的所有ip都会收到信息；
224开头		   多播路由；
4个255			有限的广播路由；受限广播路由；

```

加静态路由：route -p add 192.168.4.0 mask 255.255.255.0    192.168.3.253(网关)  metric 256(默认跃点数)  if(interface丙网络接口号码13) 13   //4.0目标网络

删除：route delete 192.168.4.0

本地表示不经过路由器，就能发送到目的地；命令行建立的路由就是网络管理，

### 筛选进出路由器的数据包

入站、出站筛选器

### 动态路由RIP

自动添加路由，解决手动容易出错问题；RIP用在小型网络，OSPF EIGRP is-is用在中大型网络。

[用动态路由打通各 Virtual L2（Zerotier）](https://www.openwrt.pro/post-515.html) [OpenWrt的路由配置(单播路由/静态路由、策略路由、IGMP组播路由)](https://www.cnblogs.com/ccky/p/15510855.html)

RIP跃点数=接口跃点数[netsh interface ip show address]+RIP跃点数[最后的路由和目标相连，跃点数2，中间2个路由和目标不相连，跃点数是1，2+1+1=4]；RIP跃点数以数据传输中经过的路由器数量来计算；win server 2012会将非通过RIP学习来的路由跃点数固定为2，包含直接连接的网络路由和静态路由。

RIP属性的设置：RIP筛选
