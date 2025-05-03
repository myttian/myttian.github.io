[认识云原生](https://zhuanlan.zhihu.com/p/499334409)  [云原生_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=%E4%BA%91%E5%8E%9F%E7%94%9F)	

**云原生的代表技术包括容器、[服务网格](https://zhida.zhihu.com/search?content_id=199094935&content_type=Article&match_order=1&q=服务网格&zhida_source=entity)、微服务、[不可变基础设施](https://zhida.zhihu.com/search?content_id=199094935&content_type=Article&match_order=1&q=不可变基础设施&zhida_source=entity)和[声明式API](https://zhida.zhihu.com/search?content_id=199094935&content_type=Article&match_order=1&q=声明式API&zhida_source=entity)** 

#### 1、云计算概述

[typora样式自定义](https://www.bilibili.com/read/cv10285496/)   [gitbook使用](https://segmentfault.com/a/1190000017960359) [云原生技术栈-温玉wiki笔记-gitbook实例](https://www.zhaowenyu.com/)  [云原生技术栈: 云原生技术栈社区汇总、整理、翻译云原生相关的文档](https://gitee.com/cncfstack/) 

##### 1.1 云计算分类：公有云、私有云、混合云

##### 1.2 云计算分层：IAAS、PAAS、SAAS

runtime运行时环境 ：  [PHP、PYTHON、java等叫运行时环境]

IAAS：基础设施当作服务提供给别人

PAAS：平台即服务，你只要把运行代码(你的应用)放上去就行了。例如:新浪云SAE,DOCKER也是，docker构建的就是运行环境，你只需要跑你的应用就行。

SAAS：软件即服务；例如：邮箱，CRM，云盘 

![image](./Docker_狂神.assets/1637349-20220604163344939-1264988399.jpg)

#### 2.虚拟化 

##### 2.1内核级虚拟化KVM(Kernel-based Virtual Machine)P126 

云计算是一种使用模式；虚拟化是一种技术。                 云计算使用虚拟化的技术：弹性伸缩 

LXD：容器 虚拟化技术，替代KVM;

a、虚拟化分：硬件虚拟化、软件虚拟化；    b、全虚拟化(vmware,kvm)、半虚拟化(xen);                c、 服务器、桌面、应用虚拟化；kvm超配，xen不超配

半虚拟化效率高；openstack(**用来更容易的管理虚拟机**)默认的虚拟机技术就是KVM；  [libvirt详解](https://blog.csdn.net/weixin_42752248/article/details/107299491) ：对虚拟机进行管理的工具和API    [vnc,xshell,putty](https://blog.csdn.net/qq_51283187/article/details/119415414)   [ LVM原理详解及实战](https://blog.csdn.net/weixin_40228200/article/details/120673984)    

```bash
kvm包含2部分：1、设备驱动/dev/kvm  2、针对模拟pc硬件的用户空间组件
内核级虚拟化：能虚拟cpu、内存等，但磁盘、网卡等虚拟不出来，用qemu能虚拟这些；
cat /proc/cpuinfo;    grep -E '(vmx|svm)' /proc/cpuinfo;  yum list |grep kvm
yum install qemu-kvm qemu-kvm-tools libvirt

1、启动
systemctl start libvirtd ; #启动后会创建一个桥接网卡virbr0; ifconfig; px显示进程

2、创建虚拟机
whereis qemu-img; rpm -qf
qemu-img create -f raw /opt/CentOS-7-x86_64.raw 10G;    yum install -y virt-install
virt-install --virt-type kvm --name win7  --ram 2048 --cdrom=/root/win7.iso  --disk path=/opt/CentOS-7-x86_64.raw --network network=default --graphics vnc,listen=0.0.0.0 --noautoconsole
网卡eth0：net.ifnames=0 biosdevname=0  分区就分一个/；  tightvnc    

管理虚拟机：virsh list --all；  virsh start ;  ip ad li;  vi  /etc/sysconfig/network-scripts/ifcfg; yum install net-tools; {vim screen mtr nc nmap tree lrzsz openssl-devel gcc glibc gcc-c++ make zip dos2unix systat mysql}
3、管理虚拟机
libvirt(一个进程daemon、一个调用api管理vm)：virsh --help；
```



##### 2.2. Docker P133 

[老男孩高级架构师体系13期-docker-135](https://www.bilibili.com/video/BV15W41117ZZ?p=135&vd_source=7346303e5e18677d7261c2c0c109ecfd) [docker容器](https://blog.51cto.com/u_13887323/2550604)     [狂神说Java_Docker基础](https://www.bilibili.com/video/BV1og4y1q7M4/?spm_id_from=333.788.recommend_more_video.1&vd_source=7346303e5e18677d7261c2c0c109ecfd)  [Docker进阶篇](https://www.bilibili.com/video/BV1kv411q7Qc?p=14)  [How nodes work](https://docs.docker.com/engine/swarm/how-swarm-mode-works/nodes/)  [docker基础篇 ](http://t.zoukankan.com/qiulovelinux-p-10297417.html)  [深入浅出Docker（一）：Docker核心技术预览](https://www.infoq.cn/article/docker-core-technology-preview/)  [深入浅出Docker](https://max.book118.com/html/2020/0322/8020055070002103.shtm)  [Docker的安全性](https://www.cnblogs.com/ztxd/p/12283716.html)  [一、Linux常见指令和权限理解](https://blog.csdn.net/QIYICat/article/details/124079825)     [docker命令](https://blog.51cto.com/dihaifeng/1713512)   [Docker 架构 | 菜鸟教程](https://www.runoob.com/docker/docker-architecture.html)    [Docker ](https://www.cnblogs.com/moveofgod/p/12830198.html)

[老男孩Linux初级运维教程](https://www.bilibili.com/video/BV1rJ411M7S1/?p=230&vd_source=7346303e5e18677d7261c2c0c109ecfd) 

Docker是基于Linux内核实现的, Docker最早采用了LXC技术, LXC是Linux原生支持的容器技术, 可以提供轻量级的虚拟化. Docker基于LXC发展, 提供了LXC的高级封装, 标准的配置方法, 在LXC的基础上, Docker提供了一系列更强大的功能. 而虚拟化技术, 比如KVM, 是基于模块实现, 后来Docker改为自己研发并开源的runc技术运行容器；

```
Docker 相比虚拟机的交付速度更快，资源消耗更低，Docker 采用客户端/服务端架构，使用远程API来管理和创建容器，其可以轻松的创建一个轻量级的、可移植的、自给自足的容器；
Docker遵从apache 2.0协议，并通过（namespace及cgroup等）来提供容器的资源隔离与安全保障等，所以Docke容器在运行时不需要类似虚拟机（空运行的虚拟机占用物理机6-8%性能）的额外资源开销，因此可以大幅提高资源利用率,总而言之Docker是一种用了新颖方式实现的轻量级虚拟机.类似于VM但是在原理和应用上和VM的差别还是很大的，并且docker的专业叫法是应用容器(Application Container)。
```

docker 的三大理念是build(构建)、ship(运输)、 run(运行)；对应代码发布面临的三个问题：构建，不仅仅是代码的构建，包括环境；  运输就是可以把环境放在任意地方；  类似java：一次构建，到处运行（跑在java虚拟机里）

docker是隔离，虚拟机是虚拟；

```bash
掌握：docker基础、原理、网络、服务、集群、错误排查、日志
linux docker k8s

概念：仓库 => 镜像 => 容器    #通过镜像创建容器； 容器：独立运行一个或一组应用
```

![](./Docker_狂神.assets/370445-20200505121725365-346977209-1746170427318-2.png)

###### a、docker安装

[DaoCloud ](http://get.daocloud.io/)    [CentOS Docker 安装 | 菜鸟教程](https://www.runoob.com/docker/centos-docker-install.html)    [Install Docker](https://docs.docker.com/engine/install/)   [Docker 的崛起、殒落](https://baijiahao.baidu.com/s?id=1725294485470667740&wfr=spider&for=pc)   [Docker-py](https://www.oschina.net/p/docker-py?hmsr=aladdin1e1)  [Docker安装-狂神](http://www.manongjc.com/detail/28-jrbefeanyxlhvgs.html)  [docker安装](https://blog.csdn.net/weixin_43164251/article/details/122877156) [Docker从入门到放弃](https://www.cnblogs.com/guihai/p/16212204.html#二、Docker安装以及配置（基于Centos安装）)  [Docker CE是什么](https://www.php.cn/docker/488462.html)  [Docker最新超详细版教程](https://www.bilibili.com/video/BV1og4y1q7M4?p=17&vd_source=7346303e5e18677d7261c2c0c109ecfd)

docker仓库：[Docker Hub](https://hub.docker.com/)   [ Docker Hub](https://hub.docker.com/search?q=cloudstack)    [DaoCloud | Docker 极速下载](http://get.daocloud.io/)   [Docker Hub](https://hub-stage.docker.com/)	

[解决docker 仓库无法访问](https://blog.csdn.net/ladymorgana/article/details/139731425)  [DockerHub被封，万无一失的所有国外镜像仓库的镜像下载和同步方法](https://www.bilibili.com/video/BV137421d7za/?vd_source=7346303e5e18677d7261c2c0c109ecfd)		 

[搭建 Docker 私有镜像仓库](https://www.cnblogs.com/studyjobs/p/17481217.html)	

[docker虚拟Windows_百度搜索](https://www.baidu.com/s?ie=utf-8&f=3&rsv_bp=1&tn=baidu&wd=docker%E8%99%9A%E6%8B%9FWindows&oq=Docker&rsv_pq=d0b14586000aff33&rsv_t=6ed3W4RrA2%2BgizOXVbiprGOnNUV224BYMpLjs5NBKpe8all29VZQY8Qwt%2Bo&rqlang=cn&rsv_enter=1&rsv_dl=ts_0&rsv_sug3=8&rsv_sug1=5&rsv_sug7=100&rsv_sug2=0&rsv_btype=t&prefixsug=Docker%25E8%2599%259A%25E6%258B%259Fwin&rsp=0&inputT=5936&rsv_sug4=5937)	[Windows系统搭建Docke](https://blog.csdn.net/tian_1_2_3/article/details/144213797)  [Docker](https://cloud.tencent.com/developer/article/1375788)	 [在 Windows 中配置 Docker](https://learn.microsoft.com/zh-cn/virtualization/windowscontainers/manage-docker/configure-docker-daemon)	 	

[curl](https://baike.baidu.com/item/curl/10098606?fr=aladdin)   [curl 的用法指南 - 阮一峰](https://www.ruanyifeng.com/blog/2019/09/curl-reference.html)   [curl 命令详解](https://www.cnblogs.com/guixiaoming/p/8507268.html)  [ Linux curl命令最全详解](https://blog.csdn.net/angle_chen123/article/details/120675472)

kubernetes：[CentOS7安装k8s ](https://www.cnblogs.com/spll/p/10033316.html)  [Kubernetes 深入学习](https://www.cnblogs.com/chiangchou/p/k8s-1.html) [Kubernetes 是什么？ | Kubernetes](https://kubernetes.io/zh/docs/concepts/overview/what-is-kubernetes/)   [2022最适合运维开发人员学的kubernetes（k8s）](https://www.bilibili.com/video/BV1Bu41167wW?p=18)  [K8s入门进阶实战全套课程](https://www.bilibili.com/video/BV1ZA4y1Z7dK?spm_id_from=333.337.search-card.all.click)

```
Kubernetes的横空出世给这家初创公司施加了巨大的压力，它未能顶住这个压力。Kubernetes是谷歌发明的一种免费开源容器管理工具，抢走了Docker自己产品的风头
```

```
yum install -y docker
Docker是S/B结构，服务端挂了，容器全挂
Docker组成：docker client（docker命令）；    docker server（后台进程）
Docker由三个组件构成：镜像、容器、仓库；
Docker用容器运行业务，就像KVM要运行一个虚拟机； 镜像放到仓库里面，类似linux yum仓库；
```

```
镜像：系统；  
容器：和镜像的关系，类似于类和实例；image是定义；容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等； 容器就是从镜像创建一个实例；用容器来运行业务，就像运行一个kvm虚拟机。
仓库：可看成一个代码控制中心，用来保存镜像

主机(host):物理或者虚拟机,用于执行 Docker 守护进程和容器。
```

###### b、docker和kvm区别

![image](./Docker_狂神.assets/1637349-20220604163558510-2022933082.jpg)
<font color=#0099ff size=5 face="微软雅黑"> python支持虚拟环境，解决py模块之间的依赖和py版本之间的问题； </font>
![image](./Docker_狂神.assets/1637349-20220604163656063-1432490863.jpg)

###### c、docker快速入门 p135

docker代理：[CentOS 7下设置Docker代理](http://t.zoukankan.com/EasonJim-p-9988154.html)  [为什么要修改docker的cgroup driver ](http://www.manongjc.com/detail/20-nytgptlajikhhpx.html) [什么是CICD](https://wenku.baidu.com/view/83a4d9346ddb6f1aff00bed5b9f3f90f76c64dec.html)  [docker常用命令 ](https://www.jianshu.com/p/887daff2518c)

```
markdown改颜色: $\color{设置颜色} {文本内容} $
<font color=#0099ff size=7 face="黑体"> color=#0099ff size=7 face="黑体" </font>
1.直接用对应颜色的英文表示，如Blue（纯蓝）、Red（纯红）、Pink（粉红）等（首字母大小写都行）。
2.rgb三原色(红绿蓝)：rgb(0,0,0)（黑色） 每一项0-255变化，全0为黑，全255为白。
3.十六进制表示法：如#000000(黑色)、#ffffff(白色)、#008000（绿色）
```

```
Docker改变了什么？？？
面向产品: 快速的产品交付  #很多开源项目现在都有dockfile
面向开发： 简化环境配置
面向测试： 多版本测试
面向运维： 环境一致性
面向架构： 自动化扩容（微服务）
```

![](./Docker_狂神.assets/Snipaste_2022-06-14_15-39-47-1746170427319-5.jpg)

![](./Docker_狂神.assets/Snipaste_2022-06-15_10-58-19-1746170427319-6.jpg)

> 1. 容器
> 2. 外部访问容器服务(网络访问 docker  run  -p)
> 3. 容器数据保存到外部(数据持久化  docker  run  -v)，容器之间访问 (数据卷容器)
> 4. 镜像构建和dockerfile（自动构建）

```bash
1)、创建容器:creat ；start(启动容器)； stop ；run（等于creat+start）；restart；rm删容器 ；logs ； port（容器端口映射）；inspect(检查，查看容器信息)； ps查看正运行容器 -a所有容器；    docker run --rm centos /bin/echo 'hehe' 容器运行完就删除。 docker run -d nginx容器运行在后台； 

进入容器：1）、attach(不可靠，不用);     2）、用(ns=namespace)nsenter,在util-linux软件包里； => inspect获取pid => nsenter -t 6863(pid) -m -u -i -n -p；  写个脚本进入容器！！！        3）、docker exec mydocker whoami，不进容器执行命令，返回一个结果；也可执行一个bash进去：docker exec -it mydocker /bin/bash;   ps -ef；  # docker cp container-id:<container_path><host_path> 复制容器文件到本地

2）、访问应用nginx:网络访问。
3）、数据持久化 

4）、镜像构建(docker commit)和dockerfile（自动构建 docker build -t mynginx:v2 .）：
5）、compose
6）、swarm集群

镜像管理：docker pull centos,  
不能连hub： rz到系统上, 本地导入image： docker load --input centos.tar(不解压); 镜像导出:docker save -o centos.tar  centos    
搜索docker search;    pull获取；   images查看；   rmi id删镜像；rm删容器  启动：docker run --name mydocker -t -i 镜像名称   /bin/bash;  #tty, i打开输入    显示运行的img:docker ps -a;    exit退出

启动容器：run --name hostname; 停止：stop 容器 id； 查看容器：ps -a -l（显示最新创建的容器）； 进入容器：exec |  attach  |nsenter;  删除容器：rm
```

```bash
1、启动：systemctl start docker；  docker images; c/s结构，服务停了，容器全停。 kvm所有服务运行在os之上，docker服务运行在docker engine之上，没法做到完全的隔离。启动后，自动创建docker0的网桥。
2、docker run --name mydocker -t -i 镜像名称   /bin/bash   #cat /proc/cpuinfo; top ;free -m; exit退出；

docker start mydocker; 再次启动容器，怎么进去：不可变基础设施(不能改我，重新开个容器）；常用nsenter脚本进去。

docker attatch mydocker(不可靠，不用)；用这个(ns=namespace)nsenter,yum install util-linux里面有；inspect获取pid；docker inspect -f "{{ .State.Pid }}" mydocker; 进入容器：nsenter -t 6863 -m -u -i -n -p； docker exec mydocker whoami，不进容器执行命令；也可进去：docker exec -it mydocker /bin/bash;   ps -ef

```

```shell
#!/bin/bash
# Use nsenter to access docker
docker_in(){
NAME_ID=$1		
PID=$(docker inspect -f "{{ .State.Pid }}" $NAME_ID)  #get PID
nsenter -t $PID -m -u -i -n -p
}
docker_in $1
```

产品交付：开源项目dockerfile；[Dockerfile之实战项目](https://blog.csdn.net/qq_15371293/article/details/122691380) [docker部署开源项目renrne-fast](https://blog.51cto.com/u_15303890/3184169)  [开源项目dockfile](https://www.baidu.com/s?ie=UTF-8&wd=开源项目dockfile)  [5款超好用的开源 Docker工具](https://www.jb51.net/article/206766.htm)   [Jenkins实战系列」（3）Jenkinsfile+DockerFile实现自动部署 - ](https://my.oschina.net/liboware/blog/5165765)  

docker数据管理：数据卷、数据卷容器;

Docker镜像构建：重点，2种方法：一种手动；一种dockfile

###### d、docker网络访问   (docker  run  -p)

容器映射端口后，外部才能访问：[Docker容器绑定外部IP和端口 ](https://www.cnblogs.com/linjiqin/p/8670798.html)

```bash
1、nat端口随机映射
网桥管理：brctl show; docker run -d  -P nginx(d后台 P nat随机端口映射)；    【查看端口：docker port 容器名 ；  docker ps;  netstat -ntlp; iptables -t nat -vnL (iptables内核集成的ip包过滤、配置内核防火墙的命令行)；】    ip ad li;     docker logs id   

2、指定映射
docker run -d -p 91:80 --name mynginx1 nginx  #91是映射的端口，80是容器里的端口
-p ip:hostPort:containerPost   #ip地址端口+容器端口   192.168.1.1:81:80

-p ip::containerPort   #iP+容器的端口
-p hostPort:containerPort:udp   #指定多个端口   -p 81:80  -p 443:443

```

![](./Docker_狂神.assets/Snipaste_2022-06-14_15-47-41-1746170427319-7.jpg)

###### e、docker数据管理(数据卷、数据卷容器)

[深入浅出Docker（一）](https://blog.csdn.net/albertlian/article/details/74278901) [ Docker核心技术（三）](https://www.kancloud.cn/huyipow/docker/503100) [Docker镜像与容器存储结构分析](https://www.51cto.com/article/458265.html)  [Docker虚拟化技术概述及部署安装](https://www.51cto.com/article/597108.html?mobile) [Docker存储方式选型建议](https://blog.51cto.com/u_15315026/3199557) [Docker几种存储驱动比较](https://blog.51cto.com/u_15127642/2755373) [联合文件系统 · Docker ](https://books.studygolang.com/docker_practice/underly/ufs.html) [Docker技术原理之Linux UnionFS（容器镜像）](https://www.jianshu.com/p/3ba255463047)

> AUFS (AnotherUnionFS) 是一种 Union FS, 简单来说就是支持将不同目录挂载到同一个虚拟文件系统下(unite several directories into a single virtual filesystem)的文件系统, 更进一步的理解, AUFS支持为每一个成员目录(类似Git Branch)设定readonly、readwrite 和 whiteout-able 权限, 同时 AUFS 里有一个类似分层的概念, 对 readonly 权限的 branch 可以逻辑上进行修改(增量地, 不影响 readonly 部分的)。
>
> 通常 Union FS 有两个用途, 一方面可以实现不借助 LVM、RAID 将多个disk挂到同一个目录下, 另一个更常用的就是将一个 readonly 的 branch 和一个 writeable 的 branch 联合在一起，Live CD正是基于此方法可以允许在 OS image 不变的基础上允许用户在其上进行一些写操作。Docker 在 AUFS 上构建的 container image 也正是如此
>
> 类似mount，mount一个目录到容器中。

```bash
下图：要让可写的永久生效，就有把它提交成镜像； 分层的。
1、把要持久化、永久保存的数据写入卷：-v /data;   -v src:dst
挂载数据卷：docker run -d --name nginx1 -v /data nginx;     #mount;看mount在主机的哪个目录：docker inspect -f {{.Mounts}} nginx2； 
第二种挂载目录方法：新建一目录/tian，挂到容器/data目录；docker run -d --name nginx3 -v /tian:/data nginx   #也可以挂载文件

2、数据卷容器：--volumes-from
让一个容器访问另一个容器的卷：docker run -it --name test2 --volumes-from test1 centos /bin/bash:   #这样，test2就能访问test1里面的卷。
```

![](./Docker_狂神.assets/Snipaste_2022-06-14_23-06-11-1746170427319-8.jpg)

###### f、docker镜像创建，重点

镜像构建和dockerfile（自动构建）   [dockerfile 详解 ](http://events.jianshu.io/p/c2d4d1c4cccf)   [dockerfile指令](https://blog.51cto.com/dihaifeng/1713512)  [Dockerfile指令详解](https://blog.51cto.com/u_15346415/4931877)    [Dockerfile指令](https://blog.51cto.com/u_14154700/2464276)  [ docker](https://blog.csdn.net/weixin_39827145/article/details/99829071)   [Docker镜像构建](https://blog.51cto.com/u_3664660/3213399)   [一张图学会Dockerfile](http://t.zoukankan.com/liujiacai-p-9153178.html)    

[$()命令替换](https://blog.csdn.net/manongxianfeng/article/details/113054828)

```bash
1、手动构建(docker commit)
杀死所有容器：docker kill $(docker ps -a -q); 删除：docker rm $(docker ps -a -q);
进入:docker run --name mynginx -it centos; 装epel源：rpm -ivh http://mirrors.aliyun.com/epel-release-latest-7.noarch.rpm
yum install nginx; nginx默认是守护进程，改到前台运行：etc/nginx/nginx.conf;加行 daemon off; 然后exit退出容器；

本地提交，把容器做成镜像：docker commit -m "my nginx"  容器id  oldboy/mynginx:v1  #oldboy仓库；v1标签(tag)； docker images

运行构建的镜像：docker run --name mynginxv1 -d -p 81:80 oldboy/mynginx:v1  nginx  #nginx启动的命令

2、自动构建
建目录：/dockerfile/nginx;建文件：默认在当前目录下读Dockerfile文件；
1，基础镜像信息 2， 维护者的信息 3，镜像操作指令 4，容器启动时执行指令 #也可以准备一个文件add加入进去。 expose 80对外80端口；cmd镜像启动的话，启动nginx命令；
构建：docker build -t mynginx:v2 .  # .是在当前目录找dockerfile    docker build -t NAME[：TAG] dockerfile路径    基于dockerfile创建镜像mynginx:v2

```

```bash
FROM centos
MAINTAINER WANG  XXX@163.COM
RUN rpm -ivh http://mirrors.aliyun.com/epel-release-latest-7.noarch.rpm
RUN yum install -y nginx && yum clean all
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

# ADD 可以把准备好的文件添加进容器
ADD index.html /usr/share/nginx/html/index.html #ADD <src> <dest>； 将<src>复制到容器中的<dest>
EXPOSE 80   #内部暴露的端口号，如果需要外部访问，还需要启动容器时增加-p或者-P参数进行分配
CMD ["nginx"]
```

g、实例

[使用 supervisor 管理进程](https://liyangliang.me/posts/2015/06/using-supervisor/)  [“Command “python setup.py egg_info“ failed with error code 1 in /tmp/pip-build-4YaSRl/pillow/“问题解决](https://blog.csdn.net/qq_40748967/article/details/121138465)  [ Command “python setup.py egg_info“ failed with error code 1 in /tmp/pip-build-*](https://blog.csdn.net/xiaojun1288/article/details/121357721?spm=1001.2101.3001.6650.15&utm_medium=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-15-121357721-blog-123750890.pc_relevant_antiscanv2&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-15-121357721-blog-123750890.pc_relevant_antiscanv2&utm_relevant_index=20)  [Docker容器的跨主机连接](https://blog.51cto.com/u_9033309/4903442)      [psmisc](https://www.jianshu.com/p/acdeb04b6c87)  [Psmisc](https://www.tqwba.com/x_d/jishu/318485.html)    [Docker设置镜像加速](https://www.cnblogs.com/satire/p/14953340.html)

[ Docker生产实践,下面的全在这个教程](https://blog.csdn.net/AlbenXie/article/details/80978494)    [Docker入门之docker-compose ](https://www.cnblogs.com/minseo/p/11548177.html) [Docker Compose ](https://m.runoob.com/docker/docker-compose.html)  [Docker](https://www.jianshu.com/p/ca1623ac7723) [Docker Compose](https://blog.csdn.net/wpc2018/article/details/122251426)   [开始使用 Docker Compose |Docker 文档](https://docs.docker.com/compose/gettingstarted/)  [Dockerfile 多阶段构建实践](https://www.cnblogs.com/qsing/p/15184539.html)   [Dockerfile最佳实践](https://zhuanlan.zhihu.com/p/102450025)   [docker基础学习](https://blog.51cto.com/dihaifeng/1713512)

```
在工作中，经常会碰到需要多个容器相互配合来完成某项任务的情况。例如要实现一个Web项目，除了Web服务容器本身，往往还需要再加上后端的数据库服务容器，甚至还包括负载均衡容器等。 Compose允许用户通过一个单独的docker-compose.yml模板文件（YAML 格式）来定义一组相关联的应用容器为一个项目（project）。
```

架构里分层设计：系统层、运行环境层、应用服务层

![image](./Docker_狂神.assets/Snipaste_2025-05-02_17-14-46.jpg)

```
# Docker for Centos  系统层级镜像
FROM centos
MAINTAINER shhnwangjian xxx@163.com

# EPEL
ADD epel.repo  /etc/yum .repos.d/
 
# Base pkg
RUN yum  install  -y wget supervisor git redis tree net-tools  sudo  psmisc mysql-devel && yum clean all

#docker build -t oldboy/centos:base .
```

```
rpm -ql psmisc |grep bin; psmisc软件包包含三个帮助管理/proc目录的程序，包含下列程序：fuser、 killall、pstree和pstree.x11（ 到pstree的链接 ）
fuser 显示使用指定文件或者文件系统的进程的PID
killall 杀死某个名字的进程，它向运行指定命令的所有进程发出信号
pstree 树型显示当前运行的进程
pstree.x11 与pstree功能相同，只是在退出前需要确认
```

```
# Base image python运行层级镜像
FROM oldboy/centos :base
MAINTAINER shhnwangjian xxx@163.com
 
# Python env
RUN yum  install  -y python-devel python-pip supervisor
 
# Upgrade pip
RUN pip  install  --upgrade pip
#docker build -t oldboy/python  .
```

构建带SSH功能的centos 7系统镜像：

```shell
# Base image
FROM centos
MAINTAINER shhnwangjian xxx@163.com
  
# EPEL
ADD epel.repo  /etc/yum .repos.d/
 
# Base pkg
RUN yum  install  -y openssh-clients openssl-devel openssh-server wget supervisor git  redis tree net-tools  sudo  psmisc mysql-devel && yum clean all
 
# For SSHD （key）
RUN  ssh -keygen -t rsa -f  /etc/ssh/ssh_host_rsa_key
RUN  ssh -keygen -t ecdsa -f  /etc/ssh/ssh_host_ecdsa_key
RUN  echo  "root:123456"  | chpasswd
#docker build -t oldboy/centos-ssh .
```

用supervisor来装：建一文件写python环境需要的依赖文件，requirements.txt； pip install -r  requirements.txt来安装这个文件；app-supervisor.ini写supervisor的配置(参考vim  /etc/supervisord.conf)      [ Docker生产实践（六）](https://blog.csdn.net/AlbenXie/article/details/80978494)

vim app.py ；  yum install python-pip；     python app.py

```
文件：app.py    app-supervisor.ini    Dockerfile   requirements.txt   supervisord.conf
```

```ini
[program:web-api]
command = /usr/bin/python2.7   /opt/app .py
process_name=%(program_name)s
autostart= true
user=www
stdout_logfile= /tmp/app.log
stderr_logfile= /tmp/app.error
 
[program:sshd]
command = /usr/sbin/sshd  -D
process_name=%(program_name)s
autostart=true
```

```shell
# Base image
FROM oldboy/python-ssh
MAINTAINER shhnwangjian xxx@163.com
 
# ADD user www
RUN  useradd  -s  /sbin/nologin  -M www
 
# ADD file
ADD app.py  /opt/app.py
ADD requirements.txt  /opt/
ADD supervisord.conf  /etc/supervisord.conf
ADD app-supervisor.ini  /etc/supervisord.d/
 
# Pip install
RUN  /usr/bin/pip2.7  install  -r  /opt/requirements .txt
 
# Port
EXPOSE 22 5000
 
# CMD
CMD [ "/usr/bin/supervisord" ,  "-c" ,  "/etc/supervisord.conf" ]
```

```bash
docker run --name web-api -d -p 88:5000 -p 8022:22 oldboy/web-api
```

###### g、docker registry 私有仓库

[Docker registry私有仓库（七）](https://blog.51cto.com/u_3664660/3213396)  [Docker Compose | 菜鸟教程 (runoob.com)](https://www.runoob.com/docker/docker-compose.html)  [Docker Registry | Docker Documentation](https://docs.docker.com/registry/)    沃通免费ssl证书     [Registry私有仓库搭建并认证](https://blog.csdn.net/bianaogong3055/article/details/100966163)    [私有仓库registry的搭建](https://blog.csdn.net/shgh_2004/article/details/80437469)   [Nginx+Docker Registry实战](https://edu.51cto.com/center/course/lesson/index?id=132439)    [ Harbor部署及使用](https://blog.csdn.net/Gf19991225/article/details/121982824)    [Harbor (goharbor.io)](https://goharbor.io/)  [Releases · goharbor/harbor (github.com)](https://github.com/goharbor/harbor/releases)  



VMware 一共有3个开源项目vic-product ：harbor、admiral、vic engine

registry太垃圾了，用Harbor（企业级 Registry 服务器）；

###### h、docker compose

[installing Docker Compose](https://docs.docker.com/compose/install/)  [Compose项目练习](https://docs.docker.com/compose/gettingstarted/)  [Flask-web框架](https://www.yiibai.com/flask/flask_overview.html) 

[Docker进阶篇](https://www.bilibili.com/video/BV1kv411q7Qc?spm_id_from=333.337.search-card.all.click)  [Docker入门-阿里云开发者社区](https://developer.aliyun.com/article/739756?spm=a2c6h.12873581.0.0.578719b4L4wbkX)  [Overview of Docker Compose](https://docs.docker.com/compose/)  [Obsidian 的 YAML Front matter 介绍 ](https://zhuanlan.zhihu.com/p/370113792) [Compose file version 3 reference ，yaml怎么写](https://docs.docker.com/compose/compose-file/compose-file-v3/#depends_on)   [Docker 生命周期](https://www.jianshu.com/p/226abfed2e46)  [Quick BI数据大屏可视化](https://developer.aliyun.com/article/951436?spm=a2c6h.12883283.index.94.7d0e4307RoRySt&scm=20140722.ID_951436.P_121.MO_938-ST_5186-V_1-ID_951436-OR_rec)  [一文读懂 Serverless ](https://baijiahao.baidu.com/s?id=1722335096951078263&wfr=spider&for=pc)

[阿里Nacos初体验](http://www.javashuo.com/article/p-qmhrhpps-ge.html)  [Nacos2.0的K8s服务发现生态应用及规划](https://baijiahao.baidu.com/s?id=1727408964632177350&wfr=spider&for=pc) [Nacos（阿里的微服务平台）](https://blog.csdn.net/u011616825/article/details/124727112) [一键wordpress](https://docs.docker.com/samples/wordpress/)

Using Compose is basically a three-step process:

1. Define your app’s environment with a `Dockerfile` so it can be reproduced anywhere.
2. Define the services that make up your app in `docker-compose.yml` so they can be run together in an isolated environment.
3. Run `docker compose up` and the [Docker compose command](https://docs.docker.com/compose/#compose-v2-and-the-new-docker-compose-command) starts and runs your entire app. You can alternatively run `docker-compose up` using the docker-compose binary.

单机用docker run；最终用集群的方式运行docker compose；

`compose是docker的开源项目，要先安装； => 就是一个二进制文件，赋权限直接执行，chmod +x`

 [app.py](https://docs.docker.com/compose/gettingstarted/)  : requirements.txt 依赖包 （flask    redis） ；   Dockfile文件；  `以前要运行应用，要打开依赖，然后互通；现在直接定义YAML文件。`  在swarm集群中，可以用 `docker service ls`服务命令； ` docker network ls`compose启动，会生成一个自己的网络 （项目中的内容都在同个网络，可以通过域名访问）；  

```bash
项目 => build生成镜像 =>run去执行； 用Compose定义运行多个容器(用yaml)；

1、应用app.py    #docker network ls/inspect docker网络
2、Dockerfile 应用打包为镜像   requirements.txt 依赖包  # Dockfile作用： 构建镜像，把项目打个包
3、Docker-compose yaml文件  （定义整个服务，需要的环境。web、redis）【完整的上线服务】   #以前要运行应用，要打开依赖，然后互通；现在直接定义YAML文件
4、启动     docker-compose up   关闭：stop、down
```

```bash
# syntax=docker/dockerfile:1    Dockfile文件
FROM python:3.7-alpine
WORKDIR /code
ENV FLASK_APP=app.py
ENV FLASK_RUN_HOST=0.0.0.0
RUN apk add --no-cache gcc musl-dev linux-headers
COPY requirements.txt requirements.txt     # requirements.txt  依赖包
RUN pip install -r requirements.txt 
EXPOSE 5000
COPY . .
CMD ["flask", "run"]
```

```yaml
version: "3.9"     #YAML文件
services:
  web:
    build: .
    ports:
      - "8000:5000"
  redis:
    image: "redis:alpine"
```

yaml规则：简化理解为只有3层： [YAML怎么写](https://docs.docker.com/compose/compose-file/compose-file-v3/#depends_on)  [ WordPress ](https://docs.docker.com/samples/wordpress/)

```bash 
version: ''  	#版本
services:    	#服务。  depends_on依赖，启动顺序； deploy部署副本，集群中用；
#其他配置：例：网络配置、卷挂载、全局规则等
```

```bash
一键wordpress：1、建项目目录  2、写yml文件  # 2个服务都是通过image来的，不需要dockfile文件。
```

> 1. Docker 镜像。 run =>容器
> 2. DockerFile 构建镜像 （服务打包）
> 3. Docker-compose 启动项目 （多个微服务/环境，通过compose编排）
> 4. Docker 网络

###### i、Docker Swarm集群 

[【狂神说Java】Docker进阶篇](https://www.bilibili.com/video/BV1kv411q7Qc?p=14)   [弹性、扩缩容](https://docs.docker.com/engine/swarm/) [How nodes work](https://docs.docker.com/engine/swarm/how-swarm-mode-works/nodes/)

`概述：创建服务 => 增加服务(扩容)`  

==现在已经不开发微服务了，用云原生，项目不用开发，去云原生平台下载云应用，改改配置，就变成自己的网站了==

==集群搭建==

```sh
docker swarm --help； ip addr；
1、生成主节点init,manager节点：docker swarm init  --advertise-addr 192.168.56.12； 
2、加入(管理者、worker)：让其它节点加入集群，获取令牌：docker swarm join-token manager（worker节点）； docker node ls ;
```

raft协议：一致性协议，保证大多数节点存活，才可以使用，高可用。集群至少>1台主节点存活。`docker swarm leave`

集群==弹性创建服务==：

```bash
告别docker run（启动单个容器）;      docker-compose up 启动一个项目，单机用！（多个容器，依赖）
集群下启动一个项目（作为一个服务）：swarm ： docker service --help ; k8s下也是服务 ;创建、动态扩展、动态更新服务   

1、通过service来启动项目:灰度发布、金丝雀发布； docker service create -p 8888:80 --name mynginx nginx
docker run 容器启动！不具有扩缩容器
docker service 服务！具有扩缩容器，滚动更新！  #docker service ps nginx；       docker service ls
2、扩容，增加3个副本：docker service update --replicas 3 mynginx； scale也是扩缩容：docker service scale mynginx=3;扩3个副本。  #docker service rm mynginx移除服务
```

概念总结：

```bash
swarm：集群的管理和编号。docker初始化一个swarm集群，其他节点可加入（管理者、工作者）
Node：docker节点，多个节点组成一个网络集群(管理、工作者)
Service：任务，核心，可在管理节点或工作节点来运行。

扩展：
调整服务以什么方式运行：服务分为可在全局节点运行的，和只能在副本上运行的： --mode string  (docker service create --mode replicated --name mytom tomcat:7)
网络模式：docker service  inspect mynginx里面"PublishMode":"ingress";    #docker network ls;   docker network inspect ingress ; yum install bridge-utils ;  iptables -nL -t nat转发信息 ； ip netns ;   
Swarm、Overlay、ingress（特殊的Overlay网络，具有负载均衡功能!IPVS VIP）
```

Docker Stack项目部署

```
单机部署项目:docker-compose up -d wordpress.yaml
集群部署:docker stack deploy  wordpress.yaml
```

Docker Secret

安全!配置密码,证书!   `docker secret --help`

docker  config --help 配置

```
展望:微服务 ==> 云原生时代；云应用； 10台机器以上，k8s；  Etcd项目
Go语言，必须掌握；天生的并发语言。  
学习语言：入门、基础语法、高级对象、操作数据库、框架
```

##### 2.3 ==Kubernetes (K8S)== 

[==Kubernetes (K8S) 3 小时上手==](https://www.bilibili.com/video/BV1Tg411P7EB/?spm_id_from=333.788.recommend_more_video.5&vd_source=7346303e5e18677d7261c2c0c109ecfd)   [==Kubernetes（K8S）易文档==](https://k8s.easydoc.net/docs/dRiQjyTY/28366845/6GiNOzyZ/9EX8Cp45)   [Kubernetes官网](https://kubernetes.io/zh-cn/) [深入理解Kube-APIServer](https://blog.csdn.net/chengyinwu/article/details/122561308)  [MongoDB可视化工具Robo 3T ](https://blog.csdn.net/qq_40814565/article/details/119669308)   [442个作者100页论文！谷歌耗时2年发布大模型新基准BIG-Bench|bench|big|文献](https://www.163.com/dy/article/H9J75T2M0511DSSR.html)

[ Kubernetes 要替换 Docker](https://blog.csdn.net/kevin_tech/article/details/118097816) [Kubernetes弃用Docker](https://developer.51cto.com/article/710688.html)   [docker-ce镜像](https://developer.aliyun.com/mirror/docker-ce?spm=a2c6h.13651102.0.0.4b251b11JYi2Ge) 

服务网格实现：[云原生Istio介绍](https://blog.csdn.net/ZGL_cyy/article/details/130467090)  [Istio太复杂了,那么试下Linkerd ](https://zhuanlan.zhihu.com/p/469824488)  [Linkerd](https://www.modb.pro/db/49977)  [Istio 是啥](https://www.cnblogs.com/lidabo/p/16453818.html) [Istio 官网](https://istio.io/latest/zh/docs/setup/getting-started/#download)  [十分钟Istio安装、部署、验证、卸载](https://www.bilibili.com/video/BV1Hj411S7cX/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd) [Docker可视化管理工具](https://www.bilibili.com/video/BV15p4y1N7fy/?spm_id_from=333.999.0.0&vd_source=7346303e5e18677d7261c2c0c109ecfd)

[微服务架构 ](https://www.bilibili.com/video/BV1et411T7Rt/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd) [微服务架构](https://www.bilibili.com/video/BV1JE411b7T2/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd) 

命令：[常用命令](https://blog.csdn.net/qq_33313357/article/details/123274532)  [命令](https://cloud.tencent.com/developer/article/1876774) 

[什么是OpenStack](https://zhuanlan.zhihu.com/p/613456473)  [Istio与OpenStack和Kubernetes怎么配合 ](https://www.yisu.com/zixun/599633.html)  [通过istio部署微服务实现灰度发布](https://www.cnblogs.com/yangmeichong/p/16613591.html) [基于 Istio 的灰度发布实现](https://www.cnblogs.com/gaoyanbing/p/17291054.html) 

[Koodo Reader](https://www.koodoreader.com/zh)

k8s 1.24新版：[容器运行时](https://kubernetes.io/zh-cn/docs/setup/production-environment/container-runtimes/)   [使用部署工具安装 Kubernetes](https://kubernetes.io/zh-cn/docs/setup/production-environment/tools/)  [K8S 1.24.0 安装部署 ](https://www.it610.com/article/1529602716295262208.htm) [初识 Containerd](https://zhuanlan.zhihu.com/p/361325982) [Docker 被 K8S 抛弃了！转型 Containerd ](https://zhuanlan.zhihu.com/p/380878219) [Kubernetes 1.24 - 走向成熟的 Kubernetes ](https://baijiahao.baidu.com/s?id=1731954957677687678&wfr=spider&for=pc)  [cri-docker.md](https://github.com/DaoCloud-OpenSource/docs/blob/main/kubernetes/sig-release/v1.24/cri-docker.md)  

视频教程：[Kubernetes (K8S)_我第一次跟着学的](https://www.bilibili.com/video/BV1Tg411P7EB?p=8&vd_source=7346303e5e18677d7261c2c0c109ecfd)  [前面视频的文档_ 易文档](https://k8s.easydoc.net/docs/dRiQjyTY/28366845/6GiNOzyZ/9EX8Cp45)  [尚硅谷Kubernetes教程(K8s入门到精通)](https://www.bilibili.com/video/BV1w4411y7Go/?spm_id_from=333.788.recommend_more_video.4&vd_source=7346303e5e18677d7261c2c0c109ecfd)    [minikube start | minikube (k8s.io)](https://minikube.sigs.k8s.io/docs/start/)   [K8s入门进阶实战全套课程，带你轻松搞定K8s](https://www.bilibili.com/video/BV1ZA4y1Z7dK?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd)   [Kubernetes 是什么？ | Kubernetes](https://kubernetes.io/zh-cn/docs/concepts/overview/what-is-kubernetes/) [2022最适合运维开发人员学的kubernetes（k8s）教程](https://www.bilibili.com/video/BV1Bu41167wW?p=18&vd_source=7346303e5e18677d7261c2c0c109ecfd)  [企业级容器云架构师docker+k8s](https://www.bilibili.com/video/BV1c64y1t7Ga/?spm_id_from=333.788.recommend_more_video.10&vd_source=7346303e5e18677d7261c2c0c109ecfd)  [docker compose_搜索](https://search.bilibili.com/all?keyword=docker compose&from_source=webtop_search&spm_id_from=333.1007)  [K8s](https://www.bilibili.com/video/BV1wv4y1G7xk?spm_id_from=333.851.b_7265636f6d6d656e64.7&vd_source=7346303e5e18677d7261c2c0c109ecfd) 

k8s.easydoc.net/docs

> -  kubernetes组成架构。
> -  用 3 种方式安装 kubernetes 集群。  包括 minikube，云平台搭建，裸机搭建（3 台服务器）
> -  
> -  部署项目到集群中，怎么对外暴露服务端口
> -  怎么部署数据库这种有状态的应用，以及如何数据持久化
> -  集群中配置文件和密码文件的使用
> -  使用 Helm 应用商店快速安装第三方应用
> -  怎么使用 Ingress 对外提供服务

是一个为 **容器化** 应用提供集群部署和管理的开源工具，由 Google 开发,Google  2014 年开源.   k8s不需要先装Docker,两者之间没有依赖关系的,都可以独立运行.

###### a. **主要特性：**

- 高可用，不宕机，自动灾难恢复
- 灰度更新，不影响业务正常运转
- 一键回滚到历史版本
- 方便的伸缩扩展（应用伸缩，机器加减）、提供负载均衡
- 有一个完善的生态

应用部署：`传统部署 => 虚拟机部署 => 容器部署`

概念：

重要概念 Pod

> master：主节点，控制平台，不需要很高性能，不跑任务，通常一个就行了，也可以开多个主节点来提高集群可用度。
> worker：工作节点，可以是虚拟机或物理计算机，任务都在这里跑，机器性能要好点；很多个，可以不断加机器扩大集群；每个工作节点由主节点管理。

豆荚，K8S 调度、管理的最小单位，一个 Pod 可以包含一个或多个容器，每个 Pod 有自己的虚拟IP。一个工作节点可以有多个 pod，主节点会考量负载自动调度 pod 到哪个节点运行。

![](./Docker_狂神.assets/kwoccq7d-1746170427319-10.jpg)

Kubernetes 组件

`kube-apiserver` API 服务器，提供对外接口，用来控制集群
`etcd` 键值数据库，保存k8s 所有集群数据的后台数据库,类似redis
`kube-scheduler` 调度 Pod 到哪个节点运行
`kube-controller(c-m)` 集群控制中心，
`cloud-controller` 云控制平台，跟云平台、云服务商交互，例如请求创建一个磁盘

![](./Docker_狂神.assets/kwonmx7e-1746170427319-11.png)

###### b.安装

[Minikube 快速入门](https://www.jianshu.com/p/ef400bfea973)  [minikube start)](https://minikube.sigs.k8s.io/docs/start/)   [usermod](https://www.runoob.com/linux/linux-comm-usermod.html) [ newgrp登入群组](https://www.runoob.com/linux/linux-comm-newgrp.html)   [K8s](https://blog.csdn.net/qq_16860629/article/details/120074449)  [kubernetes(github.com)](https://github.com/kubernetes/kubernetes)  [ nohup ](https://www.runoob.com/linux/linux-comm-nohup.html) [nohup和&](https://blog.csdn.net/hl449006540/article/details/80216061)  [Docker CE是什么](https://www.php.cn/docker/488462.html) 

[gcr.io/google-containers(k8s谷歌仓库)](https://console.cloud.google.com/gcr/images/google-containers/GLOBAL) [kubernetes镜像-aliyun](https://developer.aliyun.com/mirror/kubernetes?spm=a2c6h.13651102.0.0.4a141b11b7ujwr)    [国内镜像源（阿里、网易、清华、中科大）](https://blog.csdn.net/sirobot/article/details/106309305)  [docker-ce镜像](https://developer.aliyun.com/mirror/docker-ce?spm=a2c6h.13651102.0.0.4b251b11JYi2Ge)

使用：[ minikube安装](https://fanfanzhisu.blog.csdn.net/article/details/109271315?spm=1001.2101.3001.6650.4&utm_medium=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~default-4-109271315-blog-114059004.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~default-4-109271315-blog-114059004.pc_relevant_default&utm_relevant_index=5)   [minikube](http://fancyerii.github.io/2020/08/28/minikube/) [minikube 搭建本地k8s 环境](https://blog.51cto.com/u_15162069/2803715)  

问题：[The “docker“ driver should not be used with root privileges.](https://www.cnblogs.com/stonezpl0202/p/15187963.html)   [centos7使用Minikube](https://zhuanlan.zhihu.com/p/241030384)  [ root privileges](https://blog.csdn.net/fly_leopard/article/details/108790217) [ root privileges](https://blog.csdn.net/fly_leopard/article/details/108790217)  [ The connection to the server localhost:8080 ](https://blog.csdn.net/CEVERY/article/details/108753379) [centos7快速搭建出Kubernetes](https://zhuanlan.zhihu.com/p/241030384)  [ minikube dashboard启动不了](https://blog.csdn.net/u013887008/article/details/115265782)

无法访问gcr.io：[minikube](https://blog.csdn.net/u010953609/article/details/121536434)  [ gcr.io 镜像下载失败](https://blog.csdn.net/davidzzc/article/details/124868759) [改cgroup](https://blog.csdn.net/believe_ordinary/article/details/119046138) [ 国内拉取google kubernetes镜像](https://blog.csdn.net/networken/article/details/84571373) 

```bash
minkube:   #sudo usermod -aG docker $USER && newgrp docker
1、安装 
2、minikube start   # 启动集群。useradd => passwd => su =>sudo usermod -aG docker $USER && newgrp docker

minikube start  --image-mirror-country='cn' --image-repository='registry.cn-hangzhou.aliyuncs.com/google_containers' --base-image='registry.cn-hangzhou.aliyuncs.com/google_containers/kicbase:v0.0.30' --driver=docker

kubectl get node			# 查看节点。kubectl 是一个用来跟 K8S 集群进行交互的命令行工具
minikube stop				# 停止集群
minikube delete --all		# 清空集群 
minikube dashboard			# 安装集群可视化 Web UI 控制台
minikube node add #加节点
```

```bash
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64/
enabled=1
gpgcheck=1
repo_gpgcheck=1   #systemctl daemon-reload   restart     docker info | grep Mirrors -A1
gpgkey=https://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg https://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
EOF	 #官网未开放同步, 可能会索引gpg检查失败,用 yum install -y --nogpgcheck kubelet kubeadm kubectl 安装
setenforce 0 
yum install -y kubelet kubeadm kubectl    
systemctl enable kubelet && systemctl start kubelet
```

```
X11转发功能是端口转发的一种特殊情况。X11协议有PC X Server（服务端）软件使用，从远程服务器连接到本地PC，与电子邮件或telnet等其他客户端程序相反。通过使用X11转发，你可以跳过设置运行X Server（服务端）软件所需的复杂端口转发规则
```

```
无法访问dashboard: nohup kubectl proxy --port=9999 --address='192.168.56.15' --accept-hosts='^.*'  >/dev/null 2>&1&
```

裸机搭建

主节点需要组件

- docker（也可以是其他容器运行时）
- kubectl 集群命令行交互工具
- kubeadm 集群初始化工具

工作节点需要组件 [文档](https://kubernetes.io/zh/docs/concepts/overview/components/#node-components)

- docker（也可以是其他容器运行时）
- kubelet 管理 Pod 和容器，确保他们健康稳定运行。
- kube-proxy 网络代理，负责网络相关的工作

###### c. 1.24初始化出错

[ k8s初始化 报错-用低版本](https://blog.csdn.net/weixin_66536807/article/details/124903478)     [ Kubernetes 生产环境安装部署](https://www.kancloud.cn/caibenxiang/k8s_proc_install/815283) [Kubelet 启动异常排查](https://copyfuture.com/blogs-details/202204151344503841)   [kubelet的配置参数](http://www.javashuo.com/article/p-akkpnovv-ht.html)   [容器运行时 | Kubernetes](https://kubernetes.io/zh-cn/docs/setup/production-environment/container-runtimes/)   [使用部署工具安装 Kubernetes](https://kubernetes.io/zh-cn/docs/setup/production-environment/tools/)      

[ k8s安装步骤  ](https://blog.csdn.net/jiandanfeng2/article/details/120272683) [部署 Kubernetes 1.24](https://blog.csdn.net/u012562943/article/details/124998093)   [初始化k8s集群时报错](https://blog.csdn.net/curry10086/article/details/107579113?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2~default~CTRLIST~Rate-1-107579113-blog-120342716.pc_relevant_antiscanv2&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2~default~CTRLIST~Rate-1-107579113-blog-120342716.pc_relevant_antiscanv2)   [not ready](https://blog.csdn.net/hebian1994/article/details/121936540)



```
Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

Alternatively, if you are the root user, you can run:

  export KUBECONFIG=/etc/kubernetes/admin.conf

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 192.168.56.20:6443 --token 8q1op7.ejvb4psaolecsov8 \
	--discovery-token-ca-cert-hash sha256:bf4a9d351eb74767f642a9f56c9df8d74eb4ce348eac18bb576d13cde359c7e6 
# 忘记了重新获取：kubeadm token create --print-join-command
```

###### d. 实例

[使用腾讯云GPU服务器实现边云协同推理](https://cloud.tencent.com/developer/article/2003794)    [kubeadm 部署k8s集群 ](http://t.zoukankan.com/liweiming-p-12674947.html)  [使用 kubeadm 安装 k8s](https://segmentfault.com/a/1190000041553731)  [flannel网络详解](https://www.modb.pro/db/40951)

仓库：[Helm官网](https://helm.sh/zh/) [Artifact Hub应用中心](https://artifacthub.io/) 

包管理：[Homebrew-Mac](https://www.jianshu.com/p/f4c9cf0733ea)    [chocolatey_win](https://www.jianshu.com/p/f6c4d261f356)   [Scoop-win](https://blog.csdn.net/qq_43741794/article/details/113079959)   [Scoop](https://zhuanlan.zhihu.com/p/463284082)  [ Ubuntu中snap](https://blog.csdn.net/icanflyingg/article/details/122943909) gofish

[Chocolatey安装](https://blog.csdn.net/weixin_42261369/article/details/119573222) [Chocolatey ](https://chocolatey.org/install#individual) [升级到 PowerShell 5.1 ](http://t.zoukankan.com/jiangyunfeng-p-12572054.html)   [Windows 系统缺失的包管理器：Chocolatey、WinGet 和 Scoop ](https://sspai.com/post/65933)  [chocolatey改安装目录-商用版)](https://docs.chocolatey.org/en-us/features/install-directory-override)  [ Chocolatey 安装位置更改-个人](https://blog.csdn.net/yihuajack/article/details/123852060)  [ Scoop](https://www.limufang.com/post/569.html)  [Scoop](https://scoop.sh/#/apps?s=0&d=1&o=true)  [dorado](https://github.com/chawyehsu/dorado/blob/master/README.zh-Hans.md)   [再谈谈 Scoop 这个 Windows 下的软件包管理器](https://chawyehsu.com/blog/talk-about-scoop-the-package-manager-for-windows-again)  [Scoop](https://zhuanlan.zhihu.com/p/463284082)

` win设变量： & setx.exe ChocolateyInstall E:\Chocolatey /M ;   refreshenv   `

```bash
1. 初始化集群：kubeadm init --image-repository=registry.aliyuncs.com/google_containers
2. node加入集群：kubeadm token create --print-join-command    #kubectl get node

3. 部署应用到集群：
直接命令运行一个pod：kubectl run testapp --image=ccr.ccs.tencentyun.com/k8s-tutorial/test-k8s:v1  #kubectl get pod -o wide ;         也可用yaml文件写：kubectl  apply  -f ./pod.yaml

部署多个pod用yaml：Deployment文件，用标签关联  # kubectl get deployment ; kubectl describe pod [pod-name]pod详细信息；  kubectl logs [pod-name] -f ;  

进入容器：kubectl exec -it [pod-name] -- bash  -c ; tail -f app.log 
扩容： kubectl scale deployment test-k8s --replicas=10
pod端口映射到外部，用来访问服务：kubectl port-forward [pod-name]  8080:8080 ; kubectl logs pod/[pod-name]

```

```yaml
  #Deployment部署
apiVersion: apps/v1
kind: Deployment
metadata:
  # 部署名字
  name: test-k8s
 #----------------------------------------------------------------------------------------------- 
spec:
  replicas: 2
  # 用来查找关联的 Pod，所有标签都匹配才行
  selector:
    matchLabels:
      app: test-k8s
  # 定义 Pod 相关数据
  template:
    metadata:
      labels:
        app: test-k8s
  #----------------------------------------------------------------------------------------------      
    spec:
      # 定义容器，可以多个
      containers:
      - name: test-k8s # 容器名字
        image: ccr.ccs.tencentyun.com/k8s-tutorial/test-k8s:v1 # 镜像

```

```yaml
1. 部署，创建pod：kubectl apply -f app.yaml    #  kubectl delete deployment test-k8s;   kubectl get deployment;  kubectl describe pod/pod-name; 

2. 回滚指定版本
查看历史  kubectl rollout history deployment test-k8s

现存问题： 用服务Service部署，创建服务也用yaml文件
每次只能访问一个 pod，没有负载均衡自动转发到不同 pod
访问还需要端口转发
Pod 重创后 IP 变了，名字也变了

3. service（yaml）
kubectl apply -f app.yaml ； kubectl apply -f service.yaml    #kubectl get service(svc) ；kubectl describe svc test-k8s(service-name) ;
service通过label，关联pod； 请求先到service,再把请求转发到不同pod上。 pod再连接mongodb服务，再连接到mongodb-pod。

4. 部署有状态的应用（yaml）
StatefulSet 用来管理有状态的应用，例如数据库、Redis ，不能随意扩充副本 。 StatefulSet 会固定每个 Pod 的名字。 #无状态应用(可以随意扩充副本，每个副本都是一样的，可替代的)
yaml类型： kind: StatefulSet；  #kubectl get statefulset ; 要连接指定 Pod，pod-name.service-name

问题： 【数据还是在pod里面，重建会丢】，可以选择云存储、本地磁盘、NFS。

5. 数据持久化
minikube 提供了 hostPath 存储(yaml);不推荐使用。 
声明一个PVC,然后挂载PV。 三个yaml文件写在一起，用---分隔符

问题：当前数据库的连接地址是写死在代码里的，另外还有数据库的密码需要配置。用配置文件解决（ConfigMap）。

6. 配置文件 ConfigMap & Secret
yaml文件里设置ConfigMap,用来配置变量。  # kubectl get configmap [name] -o yaml
重要数据，例如密码、TOKEN，我们可以放到yaml里的kind: secret 中

然后在app.yaml文件里引用configmap\secret定义的变量
```

[Helm | 安装Helm](https://helm.sh/zh/docs/intro/install/) 

```
仓库：Helm & 命名空间
1. 使用脚本安装
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh

2. 使用二进制版本安装
3. 包管理器安装
```

如果想直接执行安装，运行`curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash`



#### 3、YAML语法

[YAML 入门教程](https://www.runoob.com/w3cnote/yaml-intro.html)

YAML 支持以下几种数据类型：

- 对象：键值对的集合，又称为映射（mapping）/ 哈希（hashes） / 字典（dictionary）
- 数组：一组按次序排列的值，又称为序列（sequence） / 列表（list）
- 纯量（scalars）：单个的、不可再分的值

##### 1、对象

冒号结构表示 key: value，冒号后面要加一个空格； 也可以使用 key:{key1: value1, key2: value2, ...}。
还可以使用缩进表示层级关系；

```
key: 
    child-key: value
    child-key2: value2
```

较为复杂的对象格式，可以使用问号加一个空格代表一个复杂的 key，配合一个冒号加一个空格代表一个 value：

```
?  
    - complexkey1
    - complexkey2
:
    - complexvalue1
    - complexvalue2
```

意思即对象的属性是一个数组 [complexkey1,complexkey2]，对应的值也是一个数组 [complexvalue1,complexvalue2]

##### 2、数组

以 **-** 开头的行   `- A`；多维数组，可以使用行内表示：`key: [value1, value2, ...]`；

数据结构的子成员是一个数组，则可以在该项下面缩进一个空格。

```yaml
-
 - A
 - B
 - C
```

数组也可以使用流式(flow)的方式表示：

```
companies: [{id: 1,name: company1,price: 200W},{id: 2,name: company2,price: 500W}]
```

##### 3、复合结构

数组和对象可以构成复合结构，例：

```yaml
languages:
  - Ruby
  - Perl
  - Python 
websites:
  YAML: yaml.org 
  Ruby: ruby-lang.org 
  Python: python.org 
  Perl: use.perl.org
```

转换为 json 为：

```json
{ 
  languages: [ 'Ruby', 'Perl', 'Python'],
  websites: {
    YAML: 'yaml.org',
    Ruby: 'ruby-lang.org',
    Python: 'python.org',
    Perl: 'use.perl.org' 
  } 
}
```

##### 4、引用

**&** 用来建立锚点（defaults），**<<** 表示合并到当前数据，***** 用来引用锚点。

#### 4.  CloudStack   P152 

5.  OpenStack   P166-182 

[第七章 创建第一台Openstack云主机](https://www.cnblogs.com/Mr-hu/articles/7076627.html)   [老男孩OpenStack企业私有云实战培训课程](https://edu.51cto.com/course/1469.html)  [曝光：Linux企业运维实战 ](https://www.xz577.com/e/17504.html#xz)  [Linux系统常规分区和LVM分区 ](https://www.gzy2000.cn/2020/03/107.html)     [centos7系统详细安装 ](https://blog.csdn.net/shenyuanhaojie/article/details/119066003)    [MySQL授权命令grant的使用方法](https://blog.csdn.net/a8039974/article/details/84988161?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~Rate-1.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~Rate-1.pc_relevant_default&utm_relevant_index=2)

[基于OpenStack构建企业私有云（1）实验环境准备 - 新运维社区 ](https://www.unixhot.com/article/407)  [（2）KeyStone](https://www.unixhot.com/article/409)

[openstack 和cloudstack之间的比较](https://blog.csdn.net/carolzhang8406/article/details/56480024)

```
第一章	Openstack介绍
第二章	Openstack环境准备
第三章	Openstack验证服务Keystone 		(共享服务:所有子项都要用到的服务),认证服务
第四章	Openstack镜像服务Glance			(提供虚拟机镜像)虚拟镜像的注册和存储管理；( Ceilometer 监控和数据采集，计量服务)
	 
第五章	Openstack计算服务Nova   		创建虚拟机(提供vm实例，cpu、内存等；存储项目cinder等提供硬盘)
第六章 openstack网络服务neutron 		创建网卡、子网等；提供vm网络链接；

第七章 创建第一台openstack云主机
第八章	Openstack管理服务Horizon		管理，提供web页面；
```

openstack简化资源的管理和分配；compute计算  networking网络 storage存储

存储：swift，对象存储，适用"一次写入，多次读取"，例如图片服务器； 		Cinder 块存储，提供存储资源池；

高层服务：Heat 自动化部署组件；		Trove 提供数据库应用服务；

##### <font color=#0099ff size=5>a.   基础服务 mysql RabbitMQ </font>

RabbitMQ消息队列是openstack各个服务之间进行通信的交通枢纽，例如订阅一个主题，大家互相发消息就能聊天了； web不能访问是防火墙没开端口

[防火墙：firewall-cmd命令](https://blog.csdn.net/weixin_44256848/article/details/121094904)  [RabbitMQ消息队列（三）-Centos7下安装RabbitMQ3.6.1](https://www.cnblogs.com/wyt007/p/9073258.html)   [iptables详解](https://blog.csdn.net/weixin_44792344/article/details/109674599)   [rabbitmq.config配置参数详解](https://blog.csdn.net/qq_18863573/article/details/103298361)  [RabbitMQ消息队列（四）-服务详细配置与日常监控管理 ](https://www.cnblogs.com/wyt007/p/9073316.html)  [linux安装RabbitMQ教程](http://www.codebaoku.com/it-linux/it-linux-112105.html)   [OpenStack Docs: 消息队列](https://docs.openstack.org/mitaka/zh_CN/install-guide-rdo/environment-messaging.html)  [阿里云NTP服务器 ](https://help.aliyun.com/document_detail/92704.html)

```
firewall-cmd --permanent --add-port=15672/tcp      netstat -nupl (-ntlp)    firewall-cmd --list-all  查看是否开通UDP 123端口
firewall-cmd --permanent --add-port=5672/tcp
systemctl restart firewalld.service
NTP时间服务器：生产要保证openstack所有节点的时间是一致的；时间不一致，无法创建虚拟机； yum install ntpdate
消息队列端口：5672
```

```
数据库安全设置后， 接着对后面用到的服务创建数据库，并进行用户的授权
MySQL 赋予用户权限命令可概括为：grant 权限 on 数据库对象 to 用户
mysql -u root -p；	create database keystone;	
grant all on keystone.* to 'keystone'@'localhost' identified by 'keystone';
grant all on keystone.* to 'keystone'@'%' identified by 'keystone';
{glance;  nova;  nova_api;   neutron;  cinder}
```

cat  /etc/hosts    

##### <font color=#0099ff size=5>b. 认证 keystone </font>

认证、服务目录、SOA相关知识  

 [linux mysql常用的命令](https://www.cnblogs.com/wrhbk/p/14784068.html)

服务目录：提供一个服务目录，包括所有服务项目与相关API的端点  

```
keystone.conf配置：connection = mysql+pymysql://keystone:KEYSTONE_DBPASS@controller/keystone   #用户名：密码@mysql_ip地址/数据库名称
正则列出所有配置： grep '^[a-z]'  keystone/keystone.conf
验证keystone连接数据库成功：mysql -h 192.168.56.11 -ukeystone -pkeystone -e "use keystone;show tables;"
```

```
进程：ps aux  |  grep memcached;    rpm -ql memcached 
查看日志：less /var/log/keystone/keystone.log
服务有问题，先在配置里打开debug=true;vim /etc/keystone/keystone.conf
```

## 五、架构畅谈

## 六、狂神Docker

**小结**： 镜像、容器、数据卷、网络、dockerFile(构建镜像)；  

[官网安装文档](https://docs.docker.com/engine/install/centos/)  [本地和云上的使用](https://www.bilibili.com/video/BV1eS4y1e7eu?p=54&vd_source=7346303e5e18677d7261c2c0c109ecfd)  [ Docker入门笔记 -易文档](https://docker.easydoc.net/doc/81170005/cCewZWoN/UlEl1cy7) [Docker视频-广州云科](https://www.bilibili.com/video/BV11L411g7U1?p=8&vd_source=7346303e5e18677d7261c2c0c109ecfd) 

[狂神Docker入门视频](https://www.bilibili.com/video/BV1og4y1q7M4?p=40&vd_source=7346303e5e18677d7261c2c0c109ecfd)  [狂神docker笔记](https://blog.51cto.com/u_16099220/8806106)  [Swarm集群、Stack、Secret、Config--(狂神说docker学习笔记)](https://blog.csdn.net/weixin_44589991/article/details/121704538) 
[10个Docker容器集群编排工具](https://cloud.tencent.com/developer/article/1603451)   [Docker集群与编排-KuangStudy视频](https://www.kuangstudy.com/course/play/1573900140073697282)   [docker swarm 集群服务编排部署指南（docker stack）](https://zhuanlan.zhihu.com/p/620868766) [容器的监控、编排、集群管理](https://www.bilibili.com/video/BV1hD4y1h7Sw/?p=12&vd_source=7346303e5e18677d7261c2c0c109ecfd)  

[黑马docker ](https://www.bilibili.com/video/BV1YC4y1H715/?p=9&vd_source=7346303e5e18677d7261c2c0c109ecfd)  [DockerSwarm与Overlay网络](https://www.bilibili.com/video/BV1EN411M7bf/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd)   [狂神-Docker笔记](https://www.cnblogs.com/lixiaojia/p/14191010.html)   [Docker监控工具](https://cloud.tencent.com/developer/news/21530)

 [Jenkins实现自动化CI,CD部署](https://notes.xiyankt.com/#/其它/Jenkins)  [k8s--集群搭建](https://www.cnblogs.com/zouzou-busy/p/16109720.html)

[VMware开源的企业级DockerRegistry项目](https://blog.51cto.com/u_16099349/9781652)

[什么是Podman——取代Docker的容器引擎](https://juejin.cn/post/7127086876506193950)

[把vmware workstation的虚拟机做成docker镜像:将虚拟机导出为OVF格式](https://blog.csdn.net/ihateright/article/details/131168229)  

- 安装fzf  
- k8s命令补全 ： install bash-completion
- 安装k8s命名空间切换：kubens
- 让kube-flannel命名空间下的pod启动起来

### 1、入门

#### 1、基础

##### 1、学习大纲

- DockerFile:把微服务构建成镜像
- IDEA整合Docker：把微服务发到Docker
- Docker Compose:管理集群,容器编排
  - Docker Swarm
- CI/CD：持续集成、持续部署; Jenkins

| ![](./Docker_狂神.assets/Snipaste_2024-02-26_16-19-15.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-02_16-57-07.jpg) |
| ---------------------------------------------------------- | ---------------------------------------------------------- |

##### 2、Docker为什么出现

发布一个项目：把项目带上运行环境打包,下载发布的dock镜像，直接运行

[Docker](https://www.docker.com/) [Docker_Docs](https://docs.docker.com/)  [Docker_Hub](https://hub.docker.com/)

##### 3、Docker历史及用途

| ![](./Docker_狂神.assets/Snipaste_2024-03-02_17-03-42.jpg) | ![运维](./Docker_狂神.assets/Snipaste_2024-03-02_17-10-01.jpg) |
| ---------------------------------------------------------- | ------------------------------------------------------------ |

##### 4、Docker的架构

| ![](./Docker_狂神.assets/Snipaste_2024-03-02_23-06-03.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-02_23-08-20.jpg) |
| ---------------------------------------------------------- | ---------------------------------------------------------- |

#### 2、安装卸载

[Install Docker Engine on CentOS](https://docs.docker.com/engine/install/centos/)   [阿里云镜像地址](https://developer.aliyun.com/mirror/docker-ce?spm=a2c6h.13651102.0.0.51b91b118nsCtm)  [验证软件包的安全性和完整性](https://developer.baidu.com/article/detail.html?id=379369)  [Docker uninstall](https://docs.docker.com/engine/install/centos/#uninstall-docker-engine)
[配置阿里云镜像加速器](https://help.aliyun.com/zh/acr/user-guide/accelerate-the-pulls-of-docker-official-images)   [国内docker镜像仓库](https://blog.51cto.com/u_16175441/7262747) 

[Harbor-企业级 Registry 服务器](https://www.oschina.net/p/harbor?hmsr=aladdin1e1) [**常用私有容器镜像仓库**](https://cloud.tencent.com/developer/article/1977116)  [解决Docker Hub国内无法访问](https://zhuanlan.zhihu.com/p/642560164?utm_id=0)  [Docker Proxy 镜像加速](https://dockerproxy.com/)
[reWASD键盘映射软件](https://www.bilibili.com/read/cv6616533/) [VirtualBox](https://blog.csdn.net/duleilewuhen/article/details/123910044) [Parallels苹果虚拟机](https://www.parallels.cn/) 

- **常用私有容器镜像仓库**
  - Harbor v1/v2：由 `VMware` 主导开发，并从 `CNCF` 云原生计算基金会孵化成功。
  - Red Hat Quay v3：由 `Red Hat` 开源的私有[容器镜像](https://cloud.tencent.com/product/tcr?from_column=20065&from=20065)仓库，类似于 `CoreOS` 的 Quay。
  - registry v2：`Docker` 公司发布的 v2 版本容器镜像仓库镜像，可直接运行提供服务。
  - docker-distribution：由 `docker-distribution` RPM 软件包提供，`systemd` 方式运行

quay.io:  iloveyou2024+_

```bash
# step 1: 删除旧的版本
# step 2: 安装必要的一些系统工具
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
# Step 3: 添加软件源信息
sudo yum-config-manager --add-repo https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
# Step 4：download.docker.com替换为mirrors.aliyun.com/docker-ce
sudo sed -i 's+download.docker.com+mirrors.aliyun.com/docker-ce+' /etc/yum.repos.d/docker-ce.repo
# Step 5: 更新软件包索引，并安装Docker-CE
sudo yum makecache fast
sudo yum -y install docker-ce
#官网
sudo yum -y install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
# Step 6: 开启Docker服务
sudo service docker start 官网 sudo systemctl start docker
docker version

#卸载docker
# 1、卸载依赖
sudo yum remove docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras
# 2、删除资源
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd

# 注意：
# 官方软件源默认启用了最新的软件，您可以通过编辑软件源的方式获取各个版本的软件包。例如官方并没有将测试版本的软件源置为可用，您可以通过以下方式开启。同理可以开启各种测试版本等。
# vim /etc/yum.repos.d/docker-ce.repo
#   将[docker-ce-test]下方的enabled=0修改为enabled=1
#
# 安装指定版本的Docker-CE:
# Step 1: 查找Docker-CE的版本:
# yum list docker-ce.x86_64 --showduplicates | sort -r
#   Loading mirror speeds from cached hostfile
#   Loaded plugins: branch, fastestmirror, langpacks
#   docker-ce.x86_64            17.03.1.ce-1.el7.centos            docker-ce-stable
#   docker-ce.x86_64            17.03.1.ce-1.el7.centos            @docker-ce-stable
#   docker-ce.x86_64            17.03.0.ce-1.el7.centos            docker-ce-stable
#   Available Packages
# Step2: 安装指定版本的Docker-CE: (VERSION例如上面的17.03.0.ce.1-1.el7.centos)
# sudo yum -y install docker-ce-[VERSION]

# 卸载
systemctl stop docker
sudo yum remove docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras		  # 卸载依赖
sudo rm -rf /var/lib/docker				# 删除目录
sudo rm -rf /var/lib/containerd

```

| ![](./Docker_狂神.assets/Snipaste_2024-03-03_00-50-18.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-16_15-38-47.jpg) |
| ---------------------------------------------------------- | ---------------------------------------------------------- |



#### 3、Docker原理

[qos服务质量](https://baike.baidu.com/item/qos/404053?fr=ge_ala)  [Host OS和Guest OS](https://blog.csdn.net/diandaoyi6500/article/details/116352950) [GuestOS](https://developer.aliyun.com/ask/354971)
[KVM](https://blog.csdn.net/sunr_/article/details/107909723) [KVM](https://blog.csdn.net/carolzhang8406/article/details/56667123) [KVM](https://wiki.archlinuxcn.org/wiki/KVM?rdfrom=https%3A%2F%2Fwiki.archlinux.org%2Findex.php%3Ftitle%3DKVM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)%26redirect%3Dno)  [KVM虚拟化技术](https://baijiahao.baidu.com/s?id=1767679875016831747&wfr=spider&for=pc) 

Docker是一个C-S结构的系统，Server的守护进程运行在主机上，通过Socket从客户端访问

Server接收Client指令,然后执行这个指令

| ![](./Docker_狂神.assets/Snipaste_2024-03-03_10-36-56.jpg)   | ![](./Docker_狂神.assets/Snipaste_2024-03-03_10-39-50.jpg) |
| ------------------------------------------------------------ | ---------------------------------------------------------- |
| ![为什么快](./Docker_狂神.assets/Snipaste_2024-03-03_10-42-08.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-03_10-44-07.jpg) |

#### 4、==Docker命令==

[docker_CLI](https://docs.docker.com/reference/cli/docker/image/)   [commandline](https://docs.docker.com/engine/reference/commandline/cli/)   [容器占用的磁盘空间](https://blog.51cto.com/u_16175510/8575986)  [Docker服务磁盘空间清理](https://cloud.tencent.com/developer/article/1853198?from=15425)  

[Is the docker daemon running](https://wenku.csdn.net/answer/d5243c046545433cafc5e3c23aa8c6bf) [用户添加到docker组](https://www.cnblogs.com/phpper/p/16608924.html)   

[Docker](https://www.helloworld.net/tutorial/docker/docker-hub)	

[Xshell自动补全](https://blog.csdn.net/zhouwenyuan1015/article/details/105752262)   [k8s命令补全](https://blog.csdn.net/weixin_45697293/article/details/118365185?spm=1001.2101.3001.6650.5&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-5-118365185-blog-126582047.235%5Ev43%5Epc_blog_bottom_relevance_base8&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-5-118365185-blog-126582047.235%5Ev43%5Epc_blog_bottom_relevance_base8&utm_relevant_index=6)  [kubernetes kubectl 命令补全](https://www.jianshu.com/p/86115d28adee) [source命令](https://blog.csdn.net/qq_47100953/article/details/126832801) [ source命令](https://blog.csdn.net/llg___/article/details/126250474)  [k8s命令补全](https://blog.csdn.net/xhx94/article/details/126582047) 

```bash
dnf install bash-completion
echo "source <(kubectl completion bash)" >> ~/.bashrc

# source <(kubectl completion bash)  激活 bash-completion
```



```sh
docker version
docker info
docker cmd --help
# 检查Docker守护进程是否运行
systemctl status docker
# 启动守护进程
systemctl start docker
# 检查docker守护进程日志
journalctl -u docker.service
# 将当前用户添加到docker组
sudo usermod -aG docker $USER

# 所有容器、镜像和数据卷占用的磁盘空间
docker system df

```

##### 1、镜像

```shell
docker images --help -a -q只显示镜像id
docker search mysql						# 搜索镜像
docker search mysql --filter=STARS=100	
docker pull mysql 						# 下载镜像，如果不加tag，默认下载latest版本
docker pull mysql:5.7 					# 下载指定版本(tag)
docker rmi -f  id 						# 删除镜像，通过id或仓库名
docker rmi -f $(docker images -aq)  	# 批量删除查询到的所有镜像
docker save & load						# 备份
```

##### 2、容器命令

**有了镜像才能创建容器，容器类似虚拟机，下载centos**

```shell
docker pull centos		# 下载镜像
```

**新建容器并启动**

[docker create 与 docker run异同](https://zhuanlan.zhihu.com/p/651163740) 

```bash
# 创建并运行一个新的容器, docker run 相当于执行了两个操作：create、 start
docker run  [OPTIONS] IMAGE [COMMAND] [ARG...]		
# 参数说明
--name="Name"		# 容器起个名字
-d					# 后台运行,detach
-it					# 交互方式运行，进入容器查看内容, interactive互动，TTY，Teleprinter终端
	docker run -it centos /bin/bash 进入容器，在bash下执行命令
-p					# 指定容器端口
	-p ip:主机端口：容器端口
	-p 主机端口：容器端口  例：3344:80，通过公网的3344访问容器中的80端口
-P					# 大写P,随机指定端口

# Create a new container,   创建一个新的容器但不启动它,  用docker start启动该容器
docker  create [OPTIONS] IMAGE [COMMAND] [ARG...]
```
常用命令

use `-d` with `--rm`, the container is removed when it exits or when the daemon exits

```sh
# --quiet	 Only display container IDs
docker ps							# 正在运行的容器,  List containers, 
exit								# 停止容器并退出
ctrl+p+q							# 容器不停止退出
docker rm id						# 删除容器
docker rm -f $(docker ps -aq) 		# 删除所有容器 force
docker ps -a -q |xargs docker rm 	# 用linux管道删除所有容器
docker start 容器id				   # 启动容器
docker restart id
docker stop id
docker kill id						# 强制停止
```

##### 3、其它命令

```sh
docker logs			# 日志
docker top id		# 查看容器内部的进程
docker inspect id	# 检查docker对象元数据; Return low-level information on Docker objects
```

| ![](./Docker_狂神.assets/Snipaste_2024-03-17_23-37-51.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-18_05-39-46.jpg) |
| ---------------------------------------------------------- | ---------------------------------------------------------- |

##### 4、进入运行的容器

容器通常使用后台运行，当修改配置，需要进入容器

```bash
docker exec -it 容器id /bin/bash	# 进入容器后开启一个新的终端，可以在里面操作,常用
docker attach 容器id				# 进入容器正在执行的终端，不会启动新的进程
```

##### 5、从容器内拷贝文件到主机

==主机上拷贝到容器内==用卷挂载； 
copy是手动的，以后用-v卷技术，==实现自动同步==

```sh
# docker cp 容器id：容器内路径  目的主机路径,   在主机上执行拷贝命令
docker cp sharp_heisenberg:/root/test  /root
```

#### 5、练习

##### 1、nginx

[curl_http命令行工具](https://www.cnblogs.com/qixing/p/11974684.html)  [docker run ](https://docs.docker.com/reference/cli/docker/container/run/) 

```bash
# 1.search nginx   2.pull 3.run 
#直接用run也会自动下载

# -p 127.0.0.1:8080:80/tcp , 主机:端口:容器端口
docker run -d --name nginx01 -p 3344:80 nginx
curl localhost:3344			# 本机访问，测试nginx服务
```

问题：每次改动nginx配置文件，都需要进入容器内部，十分麻烦，可以在容器外部提供一个映射路径，这样在容器外部修改文件，容器内部就自动修改，用 `-v` ==数据卷技术==

##### 2、tomcat

[Tomcat-配置文件](https://blog.csdn.net/huanshirenjian/article/details/89927468)  [tomcat-users.xml](https://www.cnblogs.com/TheGCC/p/14153635.html)  [容器中没有vi 解决方案](https://www.cnblogs.com/Baker-Street/p/17605274.html)  [docker 中没有vi如何编辑](https://blog.51cto.com/u_16175519/6774218)  [sed查找替换](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=sed查找替换&oq=sed&rsv_pq=9b24ca9600ee3129&rsv_t=e6b42s2l%2FzUxUFBHLkNcOM9CF%2BiFCyOLPfSA6CLZLgbPJsmhVe0qujXKJmA&rqlang=cn&rsv_enter=1&rsv_dl=tb&rsv_sug3=10&rsv_sug1=12&rsv_sug7=100&bs=sed) 

[Tomcat开启manager和host-manager界面](https://blog.csdn.net/weixin_46289254/article/details/130847534)   [Tomcat页面密码](https://blog.csdn.net/manyulanlanlu/article/details/132211113)   [配置启用manager/host-manager](https://www.cnblogs.com/bloglogs/p/16204953.html)

```bash
# 1.run  2.webapps目录下是空的

sed -i 's/foo/bar/g' example.txt  # 查找替换

docker run -it --rm tomcat:9.0		# 用完即删(^c)，测试用,容器停止就删除容器
# webapps目录下是空的，默认是最小镜像，不必要的都删除，保证最小可运行环境
cp -r webapps.dist/* webapps 

docker run -it -v /home/tomcat_conf:/usr/local/tomcat/conf --rm -p 8888:8080  tomcat /bin/bash
```

```xml
<!--先改webapp/manager/META-INF/context.xml，tomcat-users.xml-->
<tomcat-users xmlns="http://tomcat.apache.org/xml"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:schemaLocation="http://tomcat.apache.org/xml tomcat-users.xsd"
              version="1.0">
  <role rolename="manager-gui"/>
  <role rolename="manager-status"/>
  <role rolename="manager-script"/>
  <user username="admin" password="admin" roles="manager-gui,manager-status,manager-script"/>
  
  <!--开启host-manager,先改 webapp/host-manager/META-INF/context.xml-->
  <role rolename ="admin-gui"/>
  <role rolename ="admin-script"/>
  <user username ="host" password="host" roles="admin-gui,admin-script"/>
</tomcat-users>
```

##### 3、ES+Kibana

[全文搜索引擎 Elasticsearch ](https://www.ruanyifeng.com/blog/2017/08/elasticsearch.html) [Kibana用户手册 ](https://www.elastic.co/guide/cn/kibana/current/settings.html)  [Kibana可视化平台](https://zhuanlan.zhihu.com/p/518600840) [Elasticsearch官方](https://www.elastic.co/cn/elasticsearch) [ Kibana用户手册 ](https://www.elastic.co/guide/cn/kibana/current/introduction.html)

[ETL数据仓库工具Kettle](https://blog.csdn.net/smxzsp/article/details/108663208) [Kettle入门](https://www.jianshu.com/p/4d8171150faf?from=singlemessage&isappinstalled=0)  [数据可视化方案：Kettle+ES+Kibana](https://www.bilibili.com/video/BV1Xy4y1U7SN/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd) [Kibana](https://zhuanlan.zhihu.com/p/518600840)

Kibana 是一个为 [Logstash](http://www.oschina.net/p/logstash) 和 [ElasticSearch](http://www.oschina.net/p/elasticsearch) 提供的日志分析的 Web 接口。可使用它对日志进行高效的搜索、可视化、分析等各种操作

```bash
# 1.run 启动很卡  docker stats   2.增加内存限制，修改配置文件 -e 

# 暴露的端口很多，十分耗内存，es的数据需要放置到安全目录，用挂载； --net somenetwork 网络配置 
docker stats		# 查看内存

# 安装es时，可以先不用 --net somenetwork 参数
docker network create somenetwork
docker run -d --name elasticsearch --net somenetwork -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:tag（版本号,例如7.6.2）

docker stop elasticsearch
curl localhost:9200
# 启动es后，赶紧关闭，增加内存限制，修改配置文件 -e --env Set environment variables
docker run -d --name elasticsearch  -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" -e ES_JAVA_OPTS="Xms64m -Xmx512m" elasticsearch:7.6.2 

# Kibana连接ES：kibana通过内网地址，请求到ES； Veth Pair技术

```

Kibana如何连接es？  [Bridge & Veth Pair](https://zhuanlan.zhihu.com/p/661491415)

- 容器内部互相隔离，不能直接连，localhost:9200; 容器都搭建在linux上，能通过linux转发。

| ![](./Docker_狂神.assets/Snipaste_2024-03-04_20-02-46.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-04_20-03-44.jpg) |
| ---------------------------------------------------------- | ---------------------------------------------------------- |

#### 6、图形化Docker

[Portainer](https://blog.csdn.net/m0_67900727/article/details/123550536) [Portainer-运维派](https://www.yunweipai.com/34991.html)  [Portainer CE安装](https://docs.portainer.io/start/install-ce/server/docker/linux) [解决:Client sent an HTTP request to an HTTPS server](https://blog.csdn.net/qq_21277357/article/details/110126762) 
[Rancher的优点及不足](https://blog.csdn.net/belalds/article/details/81070191) [企业级Kubernetes 解决方案 | Rancher](https://www.rancher.cn/)  [使用Rancher部署k8s集群](https://zhuanlan.zhihu.com/p/403539342)  

![](./Docker_狂神.assets/Snipaste_2024-03-04_20-34-53.jpg)

```sh
# portainer Be商业版收费，用ce社区版
docker volume create portainer_data
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data  portainer/portainer-ce:latest

# -v 里面的数据挂载到本机  --privileged 授权
# 出现错误:把请求路径改为https://ip:端口去访问
```



### 2、进阶

#### 1、Docker镜像原理

UnionFS==联合文件系统==:分层的，例如：mysql、tomcat都有用到linux内核，mysql下载了centos，tomcat就不需要下载centos,这一层是共用的； ==方便文件复用,打包为镜像后,已经有的层不下载==;`镜像分层下载，应用相同的层直接复用`。

**bootfs、rootfs**

```
docker image inspect redis:latest
```

镜像层、容器层

| ![](./Docker_狂神.assets/Snipaste_2024-03-04_20-40-53.jpg)   | ![](./Docker_狂神.assets/Snipaste_2024-03-04_20-42-49.jpg)   |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![镜像加载原理](./Docker_狂神.assets/Snipaste_2024-03-04_20-45-35.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-04_20-49-40.jpg)   |
| ![](./Docker_狂神.assets/Snipaste_2024-03-04_20-50-41.jpg)   | ![镜像层只读，所有操作基于容器层](./Docker_狂神.assets/Snipaste_2024-03-04_20-53-46.jpg) |

#### 2、容器提交为镜像

把已经改变的容器提交为镜像：`commit      Create a new image from a container's changes`

![修改过的容器提交为镜像](./Docker_狂神.assets/Snipaste_2024-03-04_23-36-52.jpg)

#### 3、容器数据卷

==容器内数据挂到外面； 容器之间数据共享==

```bash
# 方式一
docker run -it -v 主机目录：容器目录
docker cp 8e7eb6a:/usr/local/tomcat/conf/*  /home/tomcat_conf
# -w 工作目录，docker23之后，能用相对路径； 主机目录不存在会自动创建
# As of Docker Engine version 23, you can use relative paths on the host.
docker  run  -v ./content:/content -w /content -i -t  ubuntu pwd

# 用这个命令能访问
docker run  -v /home/tomcat_conf:/usr/local/tomcat/conf --rm -d -p 8888:8080  tomcat

docker run -it -v /home/tomcat_conf:/usr/local/tomcat/conf --rm -d -p 8888:8080  tomcat /bin/bash

# 方式二 dockerfile

# 方式三 数据卷容器，多个容器之间同步数据卷
```

==MySQL同步数据==

```sh
# -e 配置环境，设密码;  mysql配置文件，data数据
docker run -d -p 3310:3306 -v /home/mysql/conf:/etc/mysql/conf.d  -v /home/mysql/data:/var/lib/mysql  -e MYSQL_ROOT_PASSWORD=123456 --name mysql01  mysql:latest
```



| ![](./Docker_狂神.assets/Snipaste_2024-03-05_16-25-46.jpg)   | ![Mounts](./Docker_狂神.assets/Snipaste_2024-03-05_16-29-15.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![mysql数据持久化](./Docker_狂神.assets/Snipaste_2024-03-05_16-38-25.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-05_16-45-26.jpg)   |

##### 1、具名和匿名挂载

==匿名挂载==： -v 只写容器内的路径

==具名挂载==：匿名挂载加上名字； `-v juming:/etc/nginx` 

==指定路径挂载==：`-v /home/mysql/conf::/etc/mysql/conf.d:ro` 

ro针对容器，只能从外面改，容器内部不能改

```sh
docker volume --help		# 查看卷
docker volume ls			# docker所有的卷
docker volume inspect `docker volume ls`

# 匿名卷默认挂载到： /var/lib/docker/volumes/xxx/_data
```

| ![](./Docker_狂神.assets/Snipaste_2024-03-18_18-13-04.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-05_16-50-00.jpg) |
| ---------------------------------------------------------- | ---------------------------------------------------------- |



##### 2、Dockerfile构建镜像时挂载卷

DockerFile用来构建docker镜像,==通过它生成镜像==(build命令)； 之前用commit

挂载2个匿名卷

```sh
docker  build [OPTIONS] PATH | URL | -		# Build an image from a Dockerfile
-t name:tag									# target
docker inspect 容器id		# 查看卷挂载到主机的哪个位置
```



![](./Docker_狂神.assets/Snipaste_2024-03-05_16-57-55.jpg)

##### 3、==数据卷容器==

多个容器挂载一个目录，用来在==容器之间同步数据==

多个容器之间同步数据卷,一个容器给其它容器共享数据

```bash
docker run -it --name docker01 kuang/centos:1.0
# --volumes-from 相当于继承docker01
docker run -it --name docker02 --volumes-from docker01 kuang/centos:1.0
```



| ![](./Docker_狂神.assets/Snipaste_2024-03-05_17-07-50.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-05_17-15-16.jpg) |
| ---------------------------------------------------------- | ---------------------------------------------------------- |
| ![](./Docker_狂神.assets/Snipaste_2024-03-05_17-16-33.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-05_17-10-43.jpg) |



#### 4、==Dockerfile==

[Dockerfile reference ](https://docs.docker.com/reference/dockerfile/)  [Docker](https://zhuanlan.zhihu.com/p/350042554)  [Dockerfile命令](https://www.jianshu.com/p/11265192400a)  

DockerFile用来构建镜像,通过它生成镜像； 之前用commit

docker Hub中99%镜像是从==基础镜像scratch==过来的,scratch镜像是一个空镜像，常用于多阶段构建

Dockerfile可以分为四部分：基础镜像信息、维护信息、镜像操作指令、启动时执行指令

```bash
# 文件名就是 Dockerfile
docker build -f dockerfile1 -t myttian/centos .			# -t 镜像名  -f dockerfile
# 查看镜像构建过程
docker history image-id
```

- add 		经tomcat等集成到镜像,添加内容;  	# `在镜像层的基础上添加其它层`
- copy 	   将文件拷贝到镜像中
- env 		构建时设置环境变量
- run         `镜像构建时要运行的命令`
  - RUN yum -y install net-tools
- cmd         `容器启动时要运行的命令`，只有最后一个会生效，可被替代;  ==替换命令==
  - CMD echo $MYPATH;   CMD /bin/bash
- entrypoint  容器启动时要运行的命令，==追加命令==
- workdir     镜像的工作目录
- expose      暴露端口
- label       生成镜像的元数据标签信息
- user        指定运行容器的用户名或ID

| ![](./Docker_狂神.assets/Snipaste_2024-03-05_22-12-21.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-05_22-14-27.jpg) |
| ---------------------------------------------------------- | ---------------------------------------------------------- |
| ![](./Docker_狂神.assets/Snipaste_2024-03-05_22-16-24.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-05_22-22-23.jpg) |
| ![](./Docker_狂神.assets/Snipaste_2024-03-19_10-33-26.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-19_11-39-23.jpg) |

##### 1、创建自己的centos

```sh
# 查看镜像构建过程
docker history id
```



| ![](./Docker_狂神.assets/Snipaste_2024-03-05_22-30-09.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-19_12-42-04.jpg) |
| ---------------------------------------------------------- | ---------------------------------------------------------- |

**CMD和ENTRYPOINT区别**

##### 2、构建自己的Tomcat镜像

[自定义tomcat环境镜像](https://www.kuangstudy.com/bbs/1485174981762945026)  [使用DockerFile构建属于自己的Docker镜像 ](https://www.kuangstudy.com/bbs/1374646712085262338)  [classpath下的dt.jar和tool.jar](https://blog.csdn.net/u013479068/article/details/42128531)
[Tomcat对应版本](https://tomcat.apache.org/whichversion.html)  [JDK Releases](https://www.java.com/en/releases/matrix/)  [JDK Releases](https://www.java.com/releases/)  [jdk Download](https://www.oracle.com/downloads/)  
[在Docker中设置动态环境变量](https://cloud.tencent.cn/developer/information/在Docker中设置动态环境变量) 

1. 下载tomcat.tar、jdk.tar
2. 写Dockfile, 添加jdk，tomcat
3. 构建镜像， `docker build -t diytomcat .`
4. 启动镜像  `把tomcat项目目录和日志挂载到主机`
5. 发布项目
   1. 需要一个WEB-INF/web.xml文件，和一个首页

ADD添加到文件会自动解压

```dockerfile
FROM centos:centos7
MAINTAINER myttian

COPY readme.txt /usr/tomcat/readme.txt

ADD jdk-21_linux-x64_bin.tar.gz /usr/tomcat/
ADD apache-tomcat-10.1.19.tar.gz /usr/tomcat/

RUN yum install -y vim

ENV MYPATH /usr/tomcat

WORKDIR $MYPATH

ENV JAVA_HOME /usr/tomcat/jdk-21.0.2
ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
ENV CATALINA_HOME /usr/tomcat/apache-tomcat-10.1.19
ENV CATALINE_BASH /usr/tomcat/apache-tomcat-10.1.19
ENV PATH $PATH:$JAVA_HOME/bin:$CATALINA_HOME/lib:$

EXPOSE 8080

CMD  /usr/tomcat/apache-tomcat-10.1.19/bin/startup.sh && tail -F  /usr/tomcat/apache-tomcat-10.1.19/bin/logs/catalina.out
```
把tomcat项目目录 和 日志挂载到主机
```shell
# 导出日志
docker run -d -p 9090:8080 --name mytomcat -v /home/myttian/build/tomcat/test:/usr/tomcat/apache-tomcat-10.1.19/webapps/test -v /home/myttian/build/tomcat/tomcatlogs:/usr/tomcat/apache-tomcat-10.1.19/logs  diytomcat:1.0
```
发布一个tomcat项目： web.xml   [tomcat web.xml](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=tomcat%20web.xml%E4%BD%9C%E7%94%A8&oq=tomcat%2520web.xml&rsv_pq=aa22bb9600108370&rsv_t=c1b1BU8t0UTzyuCxDnwVBXSrAZx365WutZOhIYbTV%2F%2BjKVWW5YwOYUtJYGM&rqlang=cn&rsv_enter=1&rsv_dl=tb&rsv_sug3=6&rsv_sug1=2&rsv_sug7=100&rsv_sug2=0&rsv_btype=t&inputT=2509&rsv_sug4=3968)  [Tomcat中Web.xml文件的作用是什么](https://www.yisu.com/ask/26765952.html)

- Web.xml文件是==Servlet规范中定义的配置文件==，用于配置Web应用程序的部署信息。在Tomcat中，Web.xml文件用于配置Servlet、Filter、Listener等组件的映射关系，配置Servlet的初始化参数、URL映射和访问权限等信息
- 通过Web.xml文件，可以对Web应用程序的行为进行灵活的控制和配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                      http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0"
         metadata-complete="true">
</web-app>
```



| ![Dockfile文件](./Docker_狂神.assets/Snipaste_2024-03-05_23-10-28.jpg) | ![ ](./Docker_狂神.assets/Snipaste_2024-03-05_23-14-07.jpg) |
| ------------------------------------------------------------ | ----------------------------------------------------------- |

##### 3、发布镜像到dockerhub\阿里云

1. 注册帐号
2. 在docker-hub上提交自己的镜像

```sh
docker login -u myid
# 添加标签，给镜像改名
docker tag f855e kuangshen/tomcat:1.0

docker push kuangshen/tomcat:1.0

# docker tag local-image:tagname   new-repo:tagname
# docker push new-repo:tagname
```

**发布到阿里云**

1. 先==创建命名空间==： 相当于一个项目，里面有很多镜像; 用来隔离,防止冲突;  类似于建一个项目文件夹 
2. ==创建镜像仓库==
3. 登录，push镜像： 参考官方文档

| ![发布到github](./Docker_狂神.assets/Snipaste_2024-03-06_00-15-57.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-06_00-22-51.jpg) |
| ------------------------------------------------------------ | ---------------------------------------------------------- |
| ![](./Docker_狂神.assets/Snipaste_2024-03-06_00-30-01.jpg)   | ![](./Docker_狂神.assets/Snipaste_2024-03-06_00-31-37.jpg) |

##### 4、指令说明

**RUN**     
[RUN指令](https://blog.csdn.net/chengqiuming/article/details/79028168) [Dockerfile命令](https://www.jianshu.com/p/11265192400a)

```dockerfile
# 格式有2种： 前者将在shell终端中运行，即/bin/sh -c;  后者使用exec执行，可以使用其他终端
# 命令较长时，使用\换行
# exec形式作为json数组解析，需要符号"而不是'
# shell形式，环境变量会起作用(解释环境变量)
# exec的shell执行，环境变量起作用
RUN <command>（shell形式，/bin/sh -c 的方式运行，避免破坏 shell 字符串）
RUN ["executable", "param1", "param2"]（exec 形式）
```

**CMD**

[CMD、ENTRYPOINT指令](https://zhuanlan.zhihu.com/p/548188679)

- Dockerfile中只能有一条 CMD指令。如果列出多个CMD，则只有最后一个CMD才会生效
- CMD 主要目的是==为执行中的容器提供默认值==。这些默认值可以包含可执行文件，也可以省略可执行文件，在这种情况下，还必须指定  ENTRYPOINT 指令

cmd三种写法：

1. CMD  ["executable", "param1", "param2"]		exec方式，推荐
2. CMD  ["param1", "param2"]                      为 ENTRYPOINT 提供默认参数
3. CMD  command  param1  param2                   shell 格式

ENTRYPOINT两种写法:

1. ENTRYPOINT  ["executable", "param1", "param2"]  exec方式，推荐

2. ENTRYPOINT  command  param1  param2             shell格式

```bash
# CMD用于指定容器启动时运行的命令。可以有多个CMD指令，但只有最后一个CMD指令会生效。CMD可以包含参数，如果在运行docker run命令时指定了参数，将会覆盖CMD中指定的参数。

# ENTRYPOINT用于指定容器启动时运行的可执行文件或脚本。和CMD一样，只有最后一个ENTRYPOINT指令会生效。ENTRYPOINT指令不会被覆盖，而是被附加到docker run命令的参数之前。

# 总结起来，CMD用于定义默认的容器启动命令，可以被覆盖，而ENTRYPOINT用于定义容器启动的主要命令，不会被覆盖。通常情况下，CMD用于提供默认的命令参数，而ENTRYPOINT用于指定容器启动的主要命令

#shell格式的ENTRYPOINT指令， 所设置命令、参数可被 docker run命令行参数中指定要运行的命令 覆盖, 但需要使用 --entrypoint 选项进行显式覆盖。否则将会忽略命令行参数
docker run --name demo3C --rm -it --entrypoint ifconfig demo3:test
# 使用 --entrypoint 选项进行显式覆盖命令时，还可以传递参数
docker run --name demo3D --rm -it --entrypoint ping demo3:test bing.com

# 对于exec格式的ENTRYPOINT指令，如果没有使用--entrypoint。当通过 docker run传递参数时, 其会被追加
docker run --name demo4E --rm -it demo4:test -H -m

# 组合使用，通过exec格式的ENTRYPOINT设置固定的命令、参数，而利用exec格式的CMD 设置默认的可变参数
ENTRYPOINT ["top", "-b"]
CMD ["-H"]
```



#### 5、==Docker网络==

[没有ip_addr安装iproute](https://blog.csdn.net/lnh1998/article/details/131293754) 

**docker0网卡：172.17.0.1，相当于路由器、网关，docker安装就有，  不支持容器名连接访问**

**学习容器编排、集群部署前提**

**桥接模式，用的veth-pair技术**:  容器带的网卡，都是一对的。

- docker如何处理容器网络访问？
  - --link: 通过服务名字连接，不需要通过ip
  - 自定义网络：把容器加入自定义网络(1个网络)
  - 网络连通：网段不相同，多网络互联(例如：2个大的网络)


==PublishMode网络模式==：

- Overlay：让集群的网络形成一个整体，绑定一起

- ingress：特殊的Overlay网络！负载均衡的功能！IPVS VIP

==虽然docker在4台机器上，实际网络是同一个！  ingress网络，是一个特殊的Overlay网络;  Overlay可使多个相互ping不通的机器联通并变成一个整体==

```bash
# 先删干净测试环境
docker rm -f $(docker ps -aq)
docker rmi -f $(docker images -aq)

ip addr  # lo 本机回环地址
# 容器启动时，docker会给容器分配一个ip，6:eth0@if7, 只要安装了docker，就会有一个网卡docker0桥接模式，使用的技术是veth-pair技术; 主机ping容器，可以ping通，主机网络和容器网络是连通的; 
# 容器和容器之间是相互ping通的
# 桥接: 中间有个桥，类似中间有个代理;  NAT是直连
# 只要容器删除，对应的网桥一对就没了
```

Swarm 集群产生两种不同类型的流量：  [网络](https://zhuanlan.zhihu.com/p/620868766?utm_id=0) 

- ==控制和管理层面==：包括 Swarm 消息管理等，例如请求加入或离开Swarm，这种类型的流量总是被加密的。(涉及到==集群内部==的hostname、ip-address、subnet、gateway等)
- ==应用数据层面==：包括==容器与客户端的通信==等。（涉及到防火墙、端口映射、网口映射、VIP等）

Swarm Service 中有三个重要的网络概念：

- Overlay networks ：管理 Swarm 中 Docker ==守护进程间的通信==。 将服务附加到 overlay 网络上，==使服务与服务之间能够通信==
- ingress network ：是一个特殊的 overlay 网络，用于==服务节点间的负载均衡==。
  - 当Swarm ==节点==在发布的端口上==接收到请求时==，它==将请求交给IPVS 模块==。==IPVS跟踪参与该服务的所有IP地址，选择其中一个==，并通过 ingress 网络将==请求路由到它==
  - 初始化或加入 Swarm 集群时会自动创建 ingress 网络，大多数情况下，用户不需要自定义配置，但是 docker 17.05 和更高版本允许你自定义。
- docker_gwbridge ：是一种桥接网络，将 overlay 网络（包括 ingress 网络）连接到一个单独的 Docker 守护进程的物理网络。默认情况下，服务正在运行的每个容器都连接到本地 Docker 守护进程主机的 docker_gwbridge 网络。
  - docker_gwbridge 网络在初始化或加入 Swarm 时自动创建。大多数情况下，用户不需要自定义配置，但是 Docker 允许自定义。

| ![代表3个网络](./Docker_狂神.assets/Snipaste_2024-03-06_09-39-36.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-06_09-40-52.jpg)   |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](./Docker_狂神.assets/Snipaste_2024-03-06_10-19-02.jpg)   | ![容器和容器之间是相互ping通的](./Docker_狂神.assets/Snipaste_2024-03-06_10-27-54.jpg) |
| ![vethpair成对网卡,桥接: 中间有个桥](./Docker_狂神.assets/Snipaste_2024-03-06_10-28-19.jpg) | ![NAT是直连](./Docker_狂神.assets/Snipaste_2024-03-06_10-32-08.jpg) |

##### 1、--link容器通过名字互联

新建容器，ip会改变，所以==通过服务名字(--name xx)==来访问服务，实现高可用

docker0：172.17.0.1  不支持容器名连接访问， 所以--link新手使用，正常用自定义网络

```sh
# 通过 --link 解决网络连通问题,不需要通过ip
# 反向也要配置，不然tomcat01连不通tomcat02
docker run -P -d --name tomcat02 --link tomcat01  diytomcat:1.0
docker exec -it tomcat02 ping tomcat01

# 查看网络信息
docker network ls     # bridge
docker network inspect 87d52
docker network rm 87d52			# 移除网络

# 为什么能访问，因为用了--link后，hosts文件里添加了对应的ip映射
docker exec -it tomcat02 cat /etc/hosts
```



| ![](./Docker_狂神.assets/Snipaste_2024-03-06_10-42-29.jpg)   | ![](./Docker_狂神.assets/Snipaste_2024-03-06_10-44-43.jpg) |
| ------------------------------------------------------------ | ---------------------------------------------------------- |
| ![hosts文件里添加了对应的ip](./Docker_狂神.assets/Snipaste_2024-03-06_10-45-39.jpg) |                                                            |

##### 2、自定义网络互联

单网络：==创建一个网络==，把容器加入这个网络(1个网络)

如果要redis网络和mysql网络等多网络互联(例如：2个大的网络)，用下一节讲的网络连通:==连接一个容器到一个网络 connect==

==PublishMode网络模式==：

- 桥接: 通过一个中间的，搭桥访问

- Overlay：让集群的网络形成一个整体，绑定一起

- ingress：特殊的Overlay网络！负载均衡的功能！IPVS VIP

```sh
# 创建一个网络，里面的容器网络互联，如果要redis网络和mysql网络等多网络互联，用下一节讲的网络连通
docker network create --driver bridge --subnet 10.0.0.0/16 --gateway 10.0.0.1 mynet
# 自定义网络里添加容器
docker run -d -P --name tomcat01 --net mynet diytomcat:1.0
docker run -d -P --name tomcat02 --net mynet diytomcat:1.0
# 可以相互ping通
docker exec -it tomcat01 ping tomcat02
```



| ![](./Docker_狂神.assets/Snipaste_2024-03-06_10-49-12.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-06_10-57-45.jpg)   |
| ---------------------------------------------------------- | ------------------------------------------------------------ |
| ![](./Docker_狂神.assets/Snipaste_2024-03-06_10-59-47.jpg) | ![多网络互联](./Docker_狂神.assets/Snipaste_2024-03-20_17-41-05.jpg) |

##### 3、网络连通

多网络互联： 网段不相同； ==连接一个容器到一个网络== connect

- 将tomcat01容器放到mynet网络下，`一个容器2个ip`：公网ip、私网ip； 例如阿里云，公网ip、私网ip

```sh
# 连接一个容器到一个网络 connect
# 将tomcat01容器放到mynet网络下，一个容器2个ip：公网ip、私网ip
# 网卡和网卡不能打通，但容器和网络可以打通
docker network connect mynet tomcat01
docker network inspect mynet
```



| ![网段不相同](./Docker_狂神.assets/Snipaste_2024-03-20_19-06-13.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-06_11-14-19.jpg) |
| ------------------------------------------------------------ | ---------------------------------------------------------- |

##### 4、其它视频教程

[VMware虚拟网络](https://zhuanlan.zhihu.com/p/496397159)   [docker的6种网络驱动视频教程](https://www.bilibili.com/video/BV13N411f7ju/?spm_id_from=333.999.0.0&vd_source=7346303e5e18677d7261c2c0c109ecfd)  [VM虚拟机的三种网络连接模式](https://baijiahao.baidu.com/s?id=1764251813478817549&wfr=spider&for=pc)  [Overlay network driver](https://docs.docker.com/network/drivers/overlay/) 

==vmware网络==

- 宿主机2个网卡，一个真实网卡，一个vmware虚拟网卡
- ==桥接== : 和宿主机用一个网络,  类似于把物理主机虚拟为一个交换机，物理主机和 虚拟机都连接到这个交换机上，所以所有桥接下的网卡与网卡都是交换模式的，相互可以访问而不干扰。在桥接模式下，虚拟机ip地址需要与主机在同一个网段，如果需要联网，则网关与DNS需要与主机网卡一致;  虚拟机的网络特性跟主机除了ip外几乎一致
- ==NAT==: 内网IP地址==转换成外部网络中使用的IP地址==，把不可路由的IP地址转化成可路由的IP地址，==对外部网络隐蔽内部网==; 虚拟机可以通过主机访问外网，外网无法访问虚拟机
  - 宿主机上的VMnet8虚拟网卡连接到VMnet8交换机上，来与虚拟机进行通信，但VMnet8虚拟网卡仅仅是用于和VMnet8虚拟交换机网段通信用的，它并不为VMnet8网段提供路由功能，处于虚拟NAT网络下的虚拟机是使用虚拟的NAT服务器连接的Internet的
  - NAT模式下，宿主机需要开启VMware NAT Service和VMware DHCP Service
- HOST：Host-Only模式其实就是NAT模式去除了虚拟NAT设备，然后用VMnet1虚拟网卡连接VMnet1虚拟交换机来与虚拟机通信，Host-Only模式将虚拟机与外网隔开，使得虚拟机成为一个独立的系统，只与主机相互通讯

==docker网络==

- macvlan：因为有些老的应用用的mac地址，访问机器的mac地址。
- overlay：覆盖网络，集群模式使用

| ![bring](./Docker_狂神.assets/bring.png)                   | ![](./Docker_狂神.assets/netka.png)              |
| ---------------------------------------------------------- | ------------------------------------------------ |
| ![NAT](./Docker_狂神.assets/nat.png)                       | ![only-host](./Docker_狂神.assets/onleyhost.png) |
| ![](./Docker_狂神.assets/Snipaste_2024-03-22_14-14-16.jpg) |                                                  |



#### 6、练习

小结：

- 集群部署：手动运行6个redis容器，组成3主3从集群
- SpringBoot微服务用dockerfile， 打包成Docker镜像

##### 1、Redis集群部署

[redis-cli命令](https://redis.com.cn/topics/rediscli.html)  [redis集群模式(cluster)](https://blog.csdn.net/qq_59727955/article/details/126284272)  [docker构建单机高可用redis集群](https://www.bilibili.com/video/BV1kU4y1b744/?spm_id_from=333.999.0.0&vd_source=7346303e5e18677d7261c2c0c109ecfd) 

哨兵、分片集群, 分片+高可用+负载均衡

**小结**：3主3从，6个redis;  1个主有1个从做备份,主挂了，从要替代主redis

- 用6个redis容器创建集群： 6个redis配置

==集群发展历史：单机、主从、哨兵、高可用==

```bash
# 1. 创建redis网络
docker network create --subnet 172.38.0.0/24 redis
# 2. 创建6个redis服务配置文件： redis要写配置文件，用脚本一次写完6个:循环6次
# 3. 启动6个redis容器: --ip 绑定的ip； 通过redis.conf启动
# 4. 进入redis-1容器，创建集群
docker exec -it redis-1 /bin/sh
redis-cli ...
# 5. 测试集群
```

```bash
# 通过脚本创建6个redis的配置;  启动6个redis服务
for port in $(seq 1 6); do \
mkdir -p /mydata/redis/node-${port}/conf
touch /mydata/redis/node-${port}/conf/redis.conf		# node-1
cat << EOF >/mydata/redis/node-${port}/conf/redis.conf
port 6379
bind 0.0.0.0
cluster-enabled yes
cluster-config-file nodes.conf
cluster-node-timeout 5000
cluster-announce-ip 172.38.0.1${port}	# 172.38.0.11
cluster-announce-port 6379
cluster-announce-bus-port 16379
appendonly yes
EOF
# 通过redis.conf启动一个容器
## 16371,  redis:5.0.9-alpine3.11: 用的redis版本
## redis-server /etc/redis/redis.conf :  通过redis.conf 启动redis
docker run -p 637${port}:6379 -p 1637${port}:16379 --name redis-${port}  -v 	/mydata/redis/node-${port}/data:/data -v /mydata/redis/node-${port}/conf/redis.conf:/etc/redis/redis.conf -d --net redis --ip 172.38.0.1${port} redis:5.0.9-alpine3.11 redis-server /etc/redis/redis.conf 
done

# 1. 创建集群：
1. 进入 docker exec -it redis-1 /bin/sh

# 1.1 redis-cli通过集群方式连接redis,创建一个集群，切片为1，3主3从
redis-cli --cluster create  172.38.0.11:6379 172.38.0.12:6379 172.38.0.13:6379 172.38.0.14:6379 1
72.38.0.15:6379 172.38.0.16:6379 --cluster-replicas 1

# 2. 测试集群
redis-cli -c  # -c连接的是集群，否则连的是单机
cluster info;cluster nodes
set name myttian ; 停止存name的容器，从redis启用； get name
```



| ![](./Docker_狂神.assets/Snipaste_2024-03-20_19-23-01.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-06_11-20-30.jpg) |
| ---------------------------------------------------------- | ---------------------------------------------------------- |

![创建集群](./Docker_狂神.assets/Snipaste_2024-03-20_19-59-34.jpg)

##### 2、SpringBoot微服务打包Docker镜像

1. 构建springboot项目
2. 打包应用: jar包
3. 编写dockerfile
   1. idea装个插件：`Docker integration`，dockerfile代码会高亮
   2. 把打包的jar和dockerfile上传到linux的idea目录

4. 在idea目录下==构建docker镜像== : `docker build  -t kuangshen666 .`
5. 发布运行
   1. push到公有云，pull拉镜像

6. 用镜像创建容器： docker run  ; 测试：curl localhost:8080

| ![](./Docker_狂神.assets/Snipaste_2024-03-06_11-45-29.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-20_20-09-25.jpg) |
| ---------------------------------------------------------- | ---------------------------------------------------------- |

### 3、高阶

[Docker集群与编排-KuangStudy视频](https://www.kuangstudy.com/course/play/1573900140073697282)  [Docker集群与编排](https://www.bilibili.com/video/BV1kv411q7Qc?p=4&vd_source=7346303e5e18677d7261c2c0c109ecfd)    [精品：云原生技术社](https://space.bilibili.com/1683316278/video?tid=0&pn=1&keyword=&order=pubdate) 

[Swarm集群、Stack、Secret、Config--(狂神说docker学习笔记)](https://blog.csdn.net/weixin_44589991/article/details/121704538)   [狂神-Docker-compose笔记](https://www.cnblogs.com/lixiaojia/p/14191010.html) 
[10个Docker容器集群编排工具](https://cloud.tencent.com/developer/article/1603451) [狂神docker笔记](https://blog.51cto.com/u_16099220/8806106)  [docker swarm 集群服务编排部署指南（docker stack）](https://zhuanlan.zhihu.com/p/620868766) 
[容器的监控、编排、集群管理](https://www.bilibili.com/video/BV1hD4y1h7Sw/?p=12&vd_source=7346303e5e18677d7261c2c0c109ecfd)  

[【千锋教育】Git+Jenkins+Harbor+Docker实现CICD](https://www.bilibili.com/video/BV1np4y1k7fN/?spm_id_from=333.999.0.0&vd_source=7346303e5e18677d7261c2c0c109ecfd)  [千锋教育Linux私有云](https://www.bilibili.com/video/BV1L4411a7SC/?spm_id_from=333.999.0.0&vd_source=7346303e5e18677d7261c2c0c109ecfd) [jenkins](https://www.bilibili.com/video/BV1rV411k758/?spm_id_from=333.999.0.0&vd_source=7346303e5e18677d7261c2c0c109ecfd)  [千锋教育Java微服务架构(springboot+springcloud+docker+iToken）](https://www.bilibili.com/video/BV1mt41127Rj/?spm_id_from=333.999.0.0&vd_source=7346303e5e18677d7261c2c0c109ecfd) 
[正向代理与反向代理](https://zhuanlan.zhihu.com/p/568566767?utm_id=0)   [反向代理](https://blog.csdn.net/m0_64346035/article/details/125336358)  [Tomcat和Nginx区别](https://blog.csdn.net/q2444154408/article/details/131005621) 

[什么是Docker Harbor](https://www.bilibili.com/video/BV1SE411P76u/?spm_id_from=333.999.0.0&vd_source=7346303e5e18677d7261c2c0c109ecfd)   [RPC原理手写、Netty进阶、Dubbo源码](https://www.bilibili.com/video/BV1pp421U7w4/?spm_id_from=333.1007.tianma.1-3-3.click&vd_source=7346303e5e18677d7261c2c0c109ecfd) 

[Docker Toolbox](https://blog.csdn.net/q7w8e9r4/article/details/133811016)  [Docker Toolbox安装](https://zhuanlan.zhihu.com/p/652616380) 

Docker Compose：几百个微服务，一个一个run，很麻烦；写个Yaml，一键启动；**打包**

Docker Swarm：**集群部署**

CI/CD:Jenkins；**持续集成/持续部署**

docker stack:类似docker compose；  secret权限认证； docker config

| ![](./Docker_狂神.assets/Snipaste_2024-03-06_16-36-15.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-21_19-32-20.jpg) |
| ---------------------------------------------------------- | ---------------------------------------------------------- |

#### 1、==容器编排compose==(service)

compose: 组成;构成

视频： [Docker集群与编排](https://www.kuangstudy.com/course/play/1573900140073697282)    [wordpress部署](https://www.bilibili.com/video/BV1ed4y1o7HF/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd)  

[狂神说docker compose笔记](https://blog.csdn.net/weixin_44589991/article/details/121493578)  [使用docker-compose 部署 Jenkins](https://www.cnblogs.com/studyjobs/p/18050720)  [docker compose jenkins](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=docker%20compose%20jenkins&oq=docker%2520compose&rsv_pq=931f63b00144ef83&rsv_t=2f2duOLj3iw0b7HdWQkmjLJ7X4ZfgdHZncosfhAUycqNij5mm27peBZSZRU&rqlang=cn&rsv_enter=0&rsv_dl=tb&rsv_sug3=9&rsv_sug1=8&rsv_sug7=100&rsv_btype=t&inputT=28081&rsv_sug4=38798) 

[docker编排参数](https://blog.51cto.com/xcbeyond/6241408)  [Docker compose 配置文件](https://blog.csdn.net/boonya/article/details/125310018) [docker容器编排](https://www.cnblogs.com/zcyy/articles/15768684.html)  [Docker-compose](https://blog.csdn.net/LYX_WIN/article/details/80806178)   [swarm集群服务编排部署](https://zhuanlan.zhihu.com/p/620868766?utm_id=0) 

以前是写dockerfile，然后build，而且是单个容器；非常麻烦；

一个项目运行需要**几百个微服务，一个一个run，很麻烦;       compose定义和运行多个容器**；    compose相当于项目应用上线到单机运行

==Compose高效管理容器，定义运行多个容器==; 就是**k8s中的服务**

1. 写一个dockerfile文件，保证项目在任何地方都可以运行
2. ==定义服务==，把我们的应用写在 `docker-compose.yml` 中
3. 用`docker-compose up` 启动项目
4. 项目启动后，不可能是单机运行，用集群的方式部署：买4台阿里云

**安装**

Install the Compose plugin: [installing Docker Compose](https://docs.docker.com/compose/install/)  [Compose项目练习](https://docs.docker.com/compose/gettingstarted/)  [Flask-web框架](https://www.yiibai.com/flask/flask_overview.html) 
[compose容器快速编排](https://www.jb51.net/server/305669owh.htm)  

```sh
yum update
yum install docker-compose-plugin
docker compose version
```

web服务，redis服务

```yaml
services:
  web:
    build: .
    ports:
      - "8000:5000"
  redis:
    image: "redis:alpine"
```

**小结：** 

- Docker-Compose的工程配置文件默认为docker-compose.yml
- 使用一个Dockerfile模板文件，可以让用户很方便的定义一个单独的应用容器。
- Compose允许用户通过一个单独的docker-compose.yml模板文件（YAML 格式）来定义一组相关联的应用容器为一个项目（project）。

**docker-compose分三层：project，service，container**

- project：代表多个service组成的项目，默认是用工作目录的名称作为project的工程名称
- service：一个 service 可以包含一个或多个容器，在里面可以定义网络模式端口镜像数据卷等参数
- container：可以直接由一个已存在的镜像运行实现，也可以通过dockerfile构建镜像实现

==单机模式下，可以使用 Docker Compose 来编排多个服务==。Docker ==Swarm 只能实现对单个服务的简单部署==。而Docker Stack 只需对已有的 docker-compose.yml 配置文件稍加改造就可以完成 Docker 集群环境下的多服务编排。

单机模式（Docker Compose）是一台主机上运行多个容器，==每个容器单独提供服务==；集群模式（swarm + stack）是多台机器组成一个集群，==多个容器一起提供同一个服务==

| ![](./Docker_狂神.assets/Snipaste_2024-06-21_07-09-00.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-06-21_07-10-59.jpg) |
| ---------------------------------------------------------- | ---------------------------------------------------------- |
| ![](./Docker_狂神.assets/Snipaste_2024-06-21_07-15-29.jpg) |                                                            |



#### 2、==集群部署:swarm==

==购买4台阿里ECS==: 按量付费;  实例选共享型便宜，1核2G,否则docker卡死;  要在同一安全组；  4台设一样的自定义密码

==4台机器安装docker== 

视频：[【狂神说Java】Docker进阶篇](https://www.bilibili.com/video/BV1kv411q7Qc?p=14)   [云原生运维课swarm](https://www.bilibili.com/video/BV1Zm4y1X7pB/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd)  

[狂神：Swarm集群、Stack、Secret、Config学习笔记](https://blog.csdn.net/weixin_44589991/article/details/121704538)  

[弹性、扩缩容](https://docs.docker.com/engine/swarm/) [How nodes work](https://docs.docker.com/engine/swarm/how-swarm-mode-works/nodes/)     

- swarm运行在云上： Deploy your app to the cloud
- swarm运行在生产环境： Deploy your app in production

##### 1、集群搭建

**小结：** `docker swarm通过命令创建集群`    `docker swarm init`

==现在已经不开发微服务了，用云原生，项目不用开发，去云原生平台下载云应用，改改配置，就变成自己的网站了==

raft协议：一致性协议，保证大多数节点存活，才可以使用，高可用。集群至少>1台主节点存活。`docker swarm leave`

操作只能在管理节点，工作节点只工作；

- init初始化集群、 join加入集群、离开、解锁、更新集群(CRUD)
- init初始化，生成主节点: 一般最少3个主节点
- 其它机器加入集群

```sh
docker swarm --help； ip addr；
# --advertise-addr 广播地址 ，阿里云用私网地址，不会产生公网流量，省钱 
1、生成主节点init,manager节点
docker swarm init  --advertise-addr 192.168.1.130 

2、加入(管理者、worker)：让其它节点加入集群，获取令牌
docker swarm join-token manager #生成主节点命令; （worker节点）
docker node ls 
```

raft协议：一致性协议，保证大多数节点存活，才可以使用，高可用。集群至少>1台主节点存活。`docker swarm leave`

##### 2、部署应用到集群(==service==)

[swarm部署nginx集群](https://www.bilibili.com/video/BV1PB4y1w7mW/?spm_id_from=333.999.0.0&vd_source=7346303e5e18677d7261c2c0c109ecfd) 

==单服务部署==： 把应用部署到集群中，使用docker service； 多服务部署用stack

```bash
# docker service --help; update包含scale功能，比它功能更强大； ps列出任务，服务装在哪些节点上
docker service ps my_nginx my_nginx

# docker service create --help; 相当于run，--replicas 任务数量
docker service create --name my_nginx  -p 81:80 --replicas 4 nginx

# 2种扩缩容方法：scale update
docker service update --replicas 3 my_nginx
docker service scale my_nginx=5
```



| ![](./Docker_狂神.assets/Snipaste_2024-03-21_14-21-27.jpg) | ![卸载docker](./Docker_狂神.assets/Snipaste_2024-03-21_14-23-06.jpg) |
| ---------------------------------------------------------- | ------------------------------------------------------------ |
| ![](./Docker_狂神.assets/Snipaste_2024-06-21_07-47-51.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-23_18-43-13.jpg)   |



###### 弹性创建服务

通过service来启动项目:灰度发布、金丝雀发布

```sh
docker service create -p 8888:80 --name my-nginx nginx
# docker run 		容器启动！不具有扩缩容器
# docker service 	服务！具有扩缩容器，滚动更新！
```



```bash
告别docker run（启动单个容器）;      docker-compose up 启动一个项目，单机用！（多个容器，依赖）
集群下启动一个项目（作为一个服务）：swarm ： docker service --help ; k8s下也是服务 ;创建、动态扩展、动态更新服务   

1、通过service来启动项目:灰度发布、金丝雀发布； docker service create -p 8888:80 --name mynginx nginx
docker run 容器启动！不具有扩缩容器
docker service 服务！具有扩缩容器，滚动更新！  #docker service ps nginx；       docker service ls
2、扩容，增加3个副本：docker service update --replicas 3 mynginx； scale也是扩缩容：docker service scale mynginx=3;扩3个副本。  #docker service rm mynginx移除服务
```

| ![](./Docker_狂神.assets/dockerservice.png) | ![](./Docker_狂神.assets/docknet.png) |
| ------------------------------------------- | ------------------------------------- |

==Overlay可使多个相互；ping不同的机器联通并变成一个整体==

==PublishMode网络模式==：

- Overlay：让集群的网络形成一个整体，绑定一起

- ingress：特殊的Overlay网络！负载均衡的功能！IPVS VIP

==虽然docker在4台机器上，实际网络是同一个！  ingress网络，是一个特殊的Overlay网络==

概念总结：

```bash
swarm：集群的管理和编号。docker初始化一个swarm集群，其他节点可加入（管理者、工作者）
Node：docker节点，多个节点组成一个网络集群(管理、工作者)
Service：任务，核心，可在管理节点或工作节点来运行。

扩展：
调整服务以什么方式运行：服务分为可在全局节点运行的，和只能在副本上运行的： --mode string  (docker service create --mode replicated --name mytom tomcat:7)
网络模式：docker service  inspect mynginx里面"PublishMode":"ingress";    #docker network ls;   docker network inspect ingress ; yum install bridge-utils ;  iptables -nL -t nat转发信息 ； ip netns ;   
Swarm、Overlay、ingress（特殊的Overlay网络，具有负载均衡功能!IPVS VIP）
```

#### 3、==Docker Stack==多服务部署

[stack部署视频 ](https://www.bilibili.com/video/BV1XN411f7hC/?spm_id_from=333.999.0.0&vd_source=7346303e5e18677d7261c2c0c109ecfd) [部署nginx+api-service实现负载均衡](https://www.cnblogs.com/JentZhang/p/18027763)  [stack部署](https://zhuanlan.zhihu.com/p/620868766?utm_id=0)   [Dockers Stack](https://blog.csdn.net/weixin_44589991/article/details/121704538) 

[DbVisualizer数据管理软件](https://zhuanlan.zhihu.com/p/634755951)  [docker stack](https://docs.docker.com/reference/cli/docker/stack/)   

[stack命令](https://zhuanlan.zhihu.com/p/620868766?utm_id=0)  

[使用NSIS打包程序](https://zhuanlan.zhihu.com/p/144079072) [NSIS打包环境搭建及入门](https://www.cnblogs.com/njabsky/p/13341682.html) 

- docker-compose 单机部署项目！
- Docker Stack部署，集群部署！

单机模式（Docker Compose）是一台主机上运行多个容器，==每个容器单独提供服务==；集群模式（swarm + stack）是多台机器组成一个集群，==多个容器一起提供同一个服务==

swarm只能将一个镜像发布到N个实例，没办法做集群的编排 

```yaml
# docker-compose.yml
mode: global	# 全局模式, 部署至每个节点。类似于k8s中的DaemonSet，会在每个节点上启动且只启动一个服务
placement: 		# 指定约束和偏好, constraints(约束)：表示服务可以部署在符合约束条件的节点上

# 部署应用
docker deploy -c docker-compose.yml stack-demo

# 其它命令
docker service ls
docker stack ls 
docker node ls
docker service ps servicename
docker stack ps stackname
```



```
单机部署项目:		docker-compose up -d wordpress.yaml
集群部署:		 docker stack deploy  wordpress.yaml
```

| ![yml文件里用deploy](./Docker_狂神.assets/stack.png)       | ![](./Docker_狂神.assets/stack1.png)                       |
| ---------------------------------------------------------- | ---------------------------------------------------------- |
| ![](./Docker_狂神.assets/Snipaste_2024-03-24_09-45-27.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-24_10-17-02.jpg) |

#### 4、Docker Secret

安全!配置密码,证书!   `docker secret --help`

==管理敏感数据存储== 

#### 5、docker  config

[docker config](https://blog.51cto.com/u_16213428/7822407) 

用于在 Docker Swarm 集群中存储和管理敏感数据和配置信息

#### 6、docker scout

[Docker中文网 ](http://docker.p2hp.com/) [docker scout](https://docs.docker.com/reference/cli/docker/scout/)  [Scout新工具优化容器应用程序开发流程](https://baijiahao.baidu.com/s?id=1779370001020463011&wfr=spider&for=pc)  [Docker监控工具](https://cloud.tencent.com/developer/news/21530)  

#### 7、小结 

弹性、扩缩容！集群！

以后告别docker run！

docker-compose up！启动一个项目。单机！

集群：swarm docker service

容器=》服务！

容器=》服务！=》副本！

redis服务=》10个副本（同时开启10个redis容器）

```
展望:微服务 ==> 云原生时代；云应用； 10台机器以上，k8s；  Etcd项目
Go语言，必须掌握；天生的并发语言。  
学习语言：入门、基础语法、高级对象、操作数据库、框架
```

==学习语言：入门、基础语法、高级对象、如何操作数据库、框架==

#### 8、==docker machine==

[Docker Machine视频](https://www.bilibili.com/video/BV1SE411P7dz/?spm_id_from=333.337.search-card.all.click&vd_source=7346303e5e18677d7261c2c0c109ecfd)  [精品：本地和云上的使用](https://www.bilibili.com/video/BV1eS4y1e7eu?p=54&vd_source=7346303e5e18677d7261c2c0c109ecfd)    [Docker Machine使用](https://www.cnblogs.com/javafirst0/p/10794727.html)   [Docker-Machine](https://blog.csdn.net/qq_41782425/article/details/105059554)  

[docker/machine安装](https://github.com/docker/machine/releases) [Machine菜鸟教程](https://www.runoob.com/docker/docker-machine.html)   [ssh免密码登录之不对称加密](https://www.cnblogs.com/ssgeek/p/9220916.html) [ssh命令](https://www.cnblogs.com/ftl1012/p/ssh.html)  

[Machine搭建Docker Swarm集群](https://blog.csdn.net/M82_A1/article/details/94719485)  [machine自动化部署docke](https://blog.csdn.net/dghfttgv/article/details/104304826) 

驱动：[docker-machine-driver-vmware](https://github.com/machine-drivers/docker-machine-driver-vmware?tab=readme-ov-file)  

[Docker Toolbox](https://blog.csdn.net/q7w8e9r4/article/details/133811016)   [Docker Desktop windows 7](https://blog.51cto.com/u_16175484/9645824)  [渗透测试工具Burp Suite](https://zhuanlan.zhihu.com/p/537832119)  

[docker-machine](https://blog.csdn.net/omaidb/article/details/133807589) [Machine的使用](https://www.cnblogs.com/zhizihuakai/p/11440115.html)  [vSphere安装](https://blog.csdn.net/weixin_49390750/article/details/132847694) [Docker Machine](https://www.cnblogs.com/zhujingzhi/p/9760198.html) [Docker](https://blog.csdn.net/weixin_45029822/article/details/108089667) [Machine](https://blog.csdn.net/m0_67401499/article/details/126598391)   [machine](https://blog.csdn.net/qq_38248841/article/details/115718472) 

[linux eval命令](http://www.mobiletrain.org/about/BBS/127777.html) 

是一个远程的管理工具,==创建已安装docker的机器==；  管==理宿主机==（上面有 Docker Engine 的主机）==的工具==

-  在远程主机上安装docker
   -  在node1上使用docker machine，给node2安装docker环境，前提：要配置免密码登录

-  在远程虚拟主机上安装docker

Docker Machine 最主要有两个作用：

- 使用 Docker Machine 方便在不同的环境中使用 Docker ，比如：Win/Mac
- 使用 Docker Machine 方便在云环境下==批量部署 Docker环境==，比如：私有云，公有云批量安装Docker环境
  - 使用docker-machine创建基于virtualbox的虚拟容器
  - 使用docker-machine创建基于vsphere的虚拟容器


通过（mac或者windows）安装docker后自带的docker-machine创建安装好docker的虚拟机

```

什么是docker-machine，简单来说就是快速创建一个docker容器环境的，在多台阿里云ECS安装上docker，
可以使用相关的命令同时给多主机上安装docker软件 不需要用传统的方式一台台的安装 
还有就是你要在本地快速创建docker集群环境，总不能一台一台创建虚拟机吧，所以docker-machine可以解决这个问题。
```



```bash
# 1. node1安装machine，加执行权限
# 2. 把docker-machine拷贝到bin目录，这样在任何地方都能执行machine命令
curl -L https://github.com/docker/machine/releases/download/v0.16.2/docker-machine-`uname -s`-`uname -m`  > /tmp/docker-machine  &&  chmod +x /tmp/docker-machine &&  cp /tmp/docker-machine /usr/local/bin/docker-machine

# 在node1上使用docker machine，给node2安装docker环境，前提：要配置免密码登录

# 创建test机器: --driver：创建机器的驱动类型
docker-machine create --driver virtualbox test
# 查看ip
docker-machine ip test
# 启动等,stop,ssh进入机器
docker-machine start test
docker-machine ssh test
```

在node1上使用docker machine，给node2安装docker环境，前提：要配置免密码登录

```sh
#  不对称加密: ==公钥相当于锁==，给别人，加密； ==私钥相当于钥匙==，自己用，解密; rsa算法
ssh-keygen -t rsa			# node1产生公钥私钥

# 公钥拷贝到192.168.1.131；  131 .ssh/生成authorized_keys文件
ssh-copy-id  -i .ssh/id_rsa.pub    root@192.168.1.131

# node2的密码使用node1的公钥加密
# 把加密字符串发给node1，node1用私钥解密
# 登录，退出exit

```



| ![](./Docker_狂神.assets/Snipaste_2024-03-24_11-04-32.jpg)   | ![使用docker machine](./Docker_狂神.assets/Snipaste_2024-03-24_12-32-54.jpg) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![要配置免密码登录](./Docker_狂神.assets/Snipaste_2024-03-24_12-33-26.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-24_13-08-21.jpg)   |
| ![](./Docker_狂神.assets/Snipaste_2024-03-24_13-09-53.jpg)   |                                                              |

#### 9、CI/CD

[持续集成（CI）/持续部署（CD）](https://zhuanlan.zhihu.com/p/42286143)	 [ci cd_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=ci%20cd)	[CI/CD（持续集成，持续交付，持续部署）](https://iyunwei.blog.csdn.net/article/details/147431169)	[什么是 CI/CD ](https://mp.weixin.qq.com/s?__biz=Mzk0MDI3MTE0MQ==&mid=2247499310&idx=1&sn=00de2c3d7c5d3d26dda6cb76b760a772)	[详解自动化开发之CI/CD](https://blog.csdn.net/kevinjin2011/article/details/125603446)	

[Jenkins_百度搜索](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=Jenkins&oq=ci%2520cd&rsv_pq=ae65f6f2000f9e0f&rsv_t=89d0I0f3p1GivR4aPtJE8g7JCktSxzLhwtL%2BDYC7cnodVU%2F2gWQmHUz1pTA&rqlang=cn&rsv_enter=1&rsv_dl=tb&rsv_sug3=14&rsv_sug1=15&rsv_sug7=100&rsv_sug2=0&rsv_btype=t&inputT=118891&rsv_sug4=118891)	

> 工厂里的装配线以快速、自动化、可重复的方式从原材料生产出消费品。
>
> 同样，软件交付管道以快速、自动化和可重复的方式从源代码生成发布版本。
>
> 如何完成这项工作的总体设计称为“持续交付”（CD）。启动装配线的过程称为“持续集成”（CI）。确保质量的过程称为“持续测试”，将最终产品提供给用户的过程称为“持续部署”。一些专家让这一切简单、顺畅、高效地运行，这些人被称为 *运维开发([DevOps](https://zhida.zhihu.com/search?content_id=8459043&content_type=Article&match_order=1&q=DevOps&zhida_source=entity))*践行者。

## 七、运维

[Ansible+shell](https://www.bilibili.com/video/BV1Ez4y1N784/?spm_id_from=333.999.0.0&vd_source=7346303e5e18677d7261c2c0c109ecfd)    [自动化运维工具——ansible](https://www.cnblogs.com/keerya/p/7987886.html) 

### 1、虚拟机

[Vagrant+VirtualBox](https://zhuanlan.zhihu.com/p/259833884)  [Vagrant和Docker的使用场景和区别](https://www.zhihu.com/question/32324376)   [实时消息传递服务器](https://zhuanlan.zhihu.com/p/657706550)   

#### 1、Vagrant

[官网](https://www.vagrantup.com/)  [Vagrant Boxes](https://app.vagrantup.com/boxes/search)   [vagrant doc](https://developer.hashicorp.com/vagrant/docs/cli/ssh)

[vagrant官网下载box](https://blog.csdn.net/shadow_zed/article/details/95032965) [vagrant](https://blog.csdn.net/weisheixiaoxin/article/details/102837269)  [如何在vagrant官网下载各种最新.box资源](https://blog.csdn.net/shadow_zed/article/details/95032965)

[Vagrant入门](https://www.bilibili.com/video/BV15t4y167zX/?spm_id_from=333.788&vd_source=7346303e5e18677d7261c2c0c109ecfd)  [Vagrant 自动化部署K3S集群](https://www.bilibili.com/video/BV1me411f7sU?p=9&vd_source=7346303e5e18677d7261c2c0c109ecfd)  [Vagrant上手](https://zhuanlan.zhihu.com/p/259833884)  [Vagrant搭建集群](https://cloud.tencent.com/developer/article/1421531) 

FAQ: [DKMS 框架](https://zhuanlan.zhihu.com/p/570367305)  [find命令](https://developer.aliyun.com/article/38079) [Please install the Linux kernel "header" files matching the current kernel](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=Please install the Linux kernel "header" files matching the current kernel for adding new hardware support to the system.&oq=This%20system%20is%20currently%20not%20set%20up%20to%20build%20kernel%20modules&rsv_pq=b9bd25fd004026e0&rsv_t=cfa1w8sp5%2B188dBh8HDjs0awKiUi7KaNI7yXOCelxkDoQ0y64iwEY9bDuDs&rqlang=cn&rsv_enter=0&rsv_dl=tb&rsv_sug3=2&rsv_btype=t)   [The vboxdrv kernel module is not loaded](https://www.jianshu.com/p/86b7c18f9e54)  [centos7 epel源](https://www.baidu.com/s?ie=utf-8&f=3&rsv_bp=1&tn=baidu&wd=centos7 epel源&oq=centos7%20dkms&rsv_pq=d03c3381001a2893&rsv_t=1183gu%2BXxCUNKEOWijd1MXFwzX0p5trljgyXVX4hSJj%2BGF4YVpbjRG6f3yg&rqlang=cn&rsv_enter=1&rsv_dl=ts_0&rsv_sug3=5&rsv_sug1=5&rsv_sug7=100&rsv_sug2=0&rsv_btype=t&prefixsug=centos7%20%20%26gt%3BP%26gt%3BL&rsp=0&inputT=5551&rsv_sug4=6602)  [Centos7配置阿里云yum源及epel源](https://blog.csdn.net/qq_42761569/article/details/128543321) 

```sh
# 需要安装dkms,在epel源中； 
yum install epel-release
yum repolist						# 检查EPEL源是否已经添加到你的系统中
cat /etc/yum.repos.d/epel.repo		# 确认EPEL源的具体信息，可以查看其对应的repo文件


# 需要安装与当前运行的Linux内核版本相匹配的“Linux内核头文件”。这通常发生在安装了新内核版本或升级了系统后，但相应的内核头文件没有安装，导致一些依赖于内核头文件的程序无法编译或运行
sudo yum install kernel-devel-$(uname -r)
find / -name "vboxdrv.sh"
./vboxdrv.sh setup
vagrant up
```

vagrant是创建和管理虚拟机的工具，它本身并不能创建和管理，依赖其它虚拟化技术的产品(调用别人的API)

| ![](./Docker_狂神.assets/Snipaste_2024-03-12_10-40-45.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-12_10-41-36.jpg) |
| ---------------------------------------------------------- | ---------------------------------------------------------- |
| ![](./Docker_狂神.assets/Snipaste_2024-03-13_12-09-47.jpg) | ![](./Docker_狂神.assets/Snipaste_2024-03-13_12-11-21.jpg) |

**概述**

Provisioners：对虚拟机进行配置，用哪种形式对虚拟机配置。

**安装**

要安装Vagrant 和 virtualbox

**创建**

需要一个基础镜像（Box文件）

**配置**

1. config.vm、 
2. config.ssh：配置ssh连接
3. config.vagrant

## 八、服务网格

