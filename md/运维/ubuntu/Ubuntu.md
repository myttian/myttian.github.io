# Ubuntu简介

[ubuntu版本区别](https://www.jianshu.com/p/b47d349fcf57)  [Ubuntu Server 24.04 (Noble Numbat) Daily Build](https://cdimage.ubuntu.com/ubuntu-server/daily-live/current/)   [Ubuntu Server docs](https://ubuntu.com/server)  [中文Ubuntu](https://cn.ubuntu.com/kubernetes)

分区：[ubuntu server 分区](https://www.cnblogs.com/billhsu2009/p/7966170.html)   [server 2204](https://blog.csdn.net/ziqibit/article/details/129932038)  [server安装](https://www.cnblogs.com/ccnn9/p/17383015.html)

分2个：/, /boot 500M ext4（安装后启动：/boot用了103M,128有点少），swap怕内存不够崩溃可以分

/boot存放linux内核，最好大一些

**安装视频：** [好：ubuntu server简单安装](https://www.bilibili.com/video/BV1Hz4y117SZ/?vd_source=7346303e5e18677d7261c2c0c109ecfd)   [Ubuntu Server 22.04 LTS ](https://www.bilibili.com/video/BV1Bs4y1X7mH/?vd_source=7346303e5e18677d7261c2c0c109ecfd)   [Ubuntu Server](https://www.bilibili.com/video/BV19u411K7Ts/?vd_source=7346303e5e18677d7261c2c0c109ecfd) 

# 常用设置

## 免密登录

[ubuntu启用root登陆 ](https://www.cnblogs.com/beifangcc/p/17638205.html) 

ssh开启root登录：[ubuntu设置root登录](https://www.baidu.com/s?ie=UTF-8&wd=ubuntu%E8%AE%BE%E7%BD%AEroot%E7%99%BB%E5%BD%95)  [配置ssh](https://blog.csdn.net/zznn0306/article/details/135359894)  [openssh](https://www.8a.hk/news/content/7351.html)  [gitolite](https://www.baidu.com/s?ie=UTF-8&wd=gitolite)  [Ubuntu下使用SSH KEY](https://jingyan.baidu.com/article/5bbb5a1bff545613eba17915.html)

```sh
# ssh：远程登录服务器， Secure Shell,是一种安全的传输协议；  
# 安装ubuntu时，import ssh key： 用ssh key作验证，每次操作git库时免去输密码
sudo passwd root					# 设置root密码, 切换到root su -
sudo nano /etc/ssh/sshd_config		# 修改PermitRootLogin yes
```

## 设置主机名

[Linux修改主机名](https://www.jb51.net/server/304596xci.htm#_label3_1_0_1) 

```sh
# 方法1
hostnamectl set-hostname node1
# 方法2， 修改后更新 systemctl restart network
vi /etc/hostname
```

## 关闭swap

[ubuntu关闭swap](https://blog.csdn.net/u010953692/article/details/129241779) 

```sh
lsb_release -a
swapon --show
swapoff -a
# /etc/fstab注释掉： /swap.img	none	swap	sw	0	0
sysctl vm.swappiness=0	# 设置swap使用限制
```

##  grub

```sh
# 1./etc/default/grub
GRUB_CMDLINE_LINUX="net.ifnames=0 biosdevname=0"
grub-mkconfig -o /boot/grub/grub.cfg 或 sudo update-grub

# 2./etc/netplan/00-installer-config.yaml, ens => eth0
```

## 关防火墙

[SElinux_container-selinux](https://blog.csdn.net/qq_37382077/article/details/89740721) 

[selinux常用命令](https://www.cnblogs.com/languang9801/p/10959369.html)  [了解SELlinux](https://www.cnblogs.com/bkylee/p/5782796.html)  [ubuntu中selinux怎么打开和关闭](https://www.yisu.com/ask/63776969.html)  
[ubuntu用AppArmor代替SELinux:强制访问控制系统](https://cloud.tencent.com/developer/article/1188032) 
[Firewalls | ufw](https://ubuntu.com/server/docs/firewalls)   [AppArmor | Ubuntu](https://ubuntu.com/server/docs/apparmor)   [PAM和AppArmor](https://www.cnblogs.com/heyongshen/p/17803060.html) 

```sh
ufw status					# firewall status

# AppArmor有两种工作模式: enforce、complain， 强制模式下不符合策略的操作会被拒绝。投诉模式下不会组织不符合策略的操作，只会记录到日志
systemctl stop apparmor			# 停止
systemctl disable apparmor		# 禁用
aa-status						# 显示当前系统上运行的AppArmor策略状态

aa-complain <PROFILE_PATH>		# 将指定的AppArmor策略设置为投诉模式
apparmor_parser -r /path/to/profile		# 重新加载生效
aa-enforce <PROFILE_PATH>
```

# apt命令

[apt更新指定版本软件包](https://www.baidu.com/s?ie=UTF-8&wd=apt%E6%9B%B4%E6%96%B0%E6%8C%87%E5%AE%9A%E7%89%88%E6%9C%AC%E8%BD%AF%E4%BB%B6%E5%8C%85)   [apt-get（安装、卸载、更新、查询软件包）](https://www.cnblogs.com/ylxtiankong/p/14637333.html) 

```bash
apt-get install nginx=1.18.0			# 更新到指定版本
# 更新所有包到最新版本，不包括内核
sudo apt-get update
sudo apt-get upgrade

# 更新包括内核在内的所有包到最新版本
sudo apt-get update
sudo apt-get dist-upgrade
```



# linux常用命令

[journalctl（systemd服务默认日志管理工具）](https://blog.csdn.net/Dontla/article/details/132415985)  

# 网络配置

[ubuntu和centos设置永久路由route](https://blog.csdn.net/simplyou/article/details/135415159) 

[联网](https://wiki.ubuntu.org.cn/%E8%81%94%E7%BD%91)  [ubuntu配置ip_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=ubuntu%E9%85%8D%E7%BD%AEip)	

[ubuntu修改网卡名称ensX为eth0](https://www.cnblogs.com/wyzhou/p/10404565.html)  [ubuntu-22.04之 netplan网络配置](https://blog.csdn.net/u014163493/article/details/136381786?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-0-136381786-blog-129833500.235^v43^pc_blog_bottom_relevance_base9&spm=1001.2101.3001.4242.1&utm_relevant_index=3) [Ubuntu 20.04改网卡名称](https://zhuanlan.zhihu.com/p/642151238?utm_id=0) [Ubuntu16.04静态网络配置_/etc/network/if-up.d](https://blog.csdn.net/qq_40682522/article/details/78269830)   [Ubuntu20不再支持/etc/network/interfaces配置文件](https://blog.csdn.net/yunlin2000/article/details/125078396?spm=1001.2101.3001.6650.3&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-3-125078396-blog-45063817.235%5Ev43%5Epc_blog_bottom_relevance_base9&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-3-125078396-blog-45063817.235%5Ev43%5Epc_blog_bottom_relevance_base9&utm_relevant_index=6)  

```sh
# /etc/netplan/01-network-manager-all.yaml
# to 是那个网段的ip, via 是走的哪个网关 metric 是优先级 默认100 值越小优先级越大
# netplan apply,  route -n
network:
    version: 2
    renderer: networkd
    ethernets:
        eth0:
            dhcp4: no
            addresses: [192.168.1.10/24]
            gateway4: 192.168.1.1
            routes:
                - to: 172.16.0.0/16
                  via: 192.168.1.1
                  metric: 50
                - to: 10.0.0.0/8
                  via: 192.168.1.1
                  metric: 100
```

# 日志

[journalctl日志](https://www.baidu.com/s?ie=UTF-8&wd=journalctl%E6%97%A5%E5%BF%97%E4%BD%8D%E7%BD%AE)  [journalctl日志分析](https://cloud.tencent.com/developer/article/2295875) [Linux日志管理工具](https://cloud.tencent.com/developer/article/2089542?areaId=106001) 

```
systemctl status systemd-journald
journalctl -u service_name			# 查看指定服务
journalctl -xeu kubelet | grep -E 'Failed|error' -n		# n行号 i忽略大小写
```

# 官方手册

[Ubuntu中文论坛](https://forum.ubuntu.org.cn/)  [Ubuntu Community Hub](https://discourse.ubuntu.com/)  [Official Ubuntu Documentation](https://help.ubuntu.com/) [Ubuntu:非官方新手入门指南](https://wiki.ubuntu.org.cn/Ubuntu:%E9%9D%9E%E5%AE%98%E6%96%B9%E6%96%B0%E6%89%8B%E5%85%A5%E9%97%A8%E6%8C%87%E5%8D%97%EF%BC%88%E9%80%9A%E7%94%A8%E5%9E%8B%EF%BC%89)  

[Ubuntu 入门指南](https://blog.csdn.net/qq_42452134/article/details/135261561) 

#  未分

apt:

[bash的<<, <<<, < <()用法](https://www.cnblogs.com/wucaiyun1/p/15978482.html)    [ubuntu24创建开机服务](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=ubuntu24%E5%88%9B%E5%BB%BA%E5%BC%80%E6%9C%BA%E6%9C%8D%E5%8A%A1&rn=20&oq=ubuntu24%25E5%2588%259B%25E5%25BB%25BA%25E6%259C%258D%25E5%258A%25A1&rsv_pq=cb09a44b0001f3fd&rsv_t=b0d6%2BksjzSTGb%2FRcv%2FryS8KOghxUd53iiXKVZz19XemHKNBaafUmhcp8zTI&rqlang=cn&rsv_enter=0&rsv_dl=tb&rsv_btype=t&inputT=1779&rsv_sug3=10&rsv_sug1=8&rsv_sug7=100&bs=ubuntu24%E5%88%9B%E5%BB%BA%E6%9C%8D%E5%8A%A1)  [创建一个开机服务](https://download.csdn.net/blog/column/12420034/136518010)  [创建一个服务](https://www.baidu.com/s?ie=UTF-8&wd=%E4%BE%8B%E5%A6%82%E7%94%A8%E4%BA%8E%E5%88%9B%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%90%8D%E4%B8%BAmy_network_app.service%E7%9A%84systemd%E6%9C%8D%E5%8A%A1%EF%BC%8C%E8%AF%A5%E6%9C%8D%E5%8A%A1%E5%B0%86%E5%9C%A8%E7%B3%BB%E7%BB%9F%E5%90%AF%E5%8A%A8%E6%97%B6%E8%BF%90%E8%A1%8C%E4%B8%80%E4%B8%AA%E7%BD%91%E7%BB%9C%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F) 

```sh
apt update, apt-get update
apt list --upgradable
# 解压zip
unzip file.zip -d /path	
7z x file.zip				# p7zip
```

[认识rancher](https://www.cnblogs.com/zhangxingeng/p/11753959.html) [在SELinux模式下安装Rancher-RHEL/CentOS](https://blog.51cto.com/u_14966640/8587020) 

[openSUSE Download](https://download.opensuse.org/update/)  [kubernetes镜像-阿里巴巴开源镜像站](https://developer.aliyun.com/mirror/kubernetes?spm=a2c6h.12873639.article-detail.8.28e74579dQ2dwL)  [cri-o/packaging](https://github.com/cri-o/packaging)  

[grep命令](https://www.cnblogs.com/wordless/p/16208858.html) [正则表达式](https://www.runoob.com/regexp/regexp-metachar.html)  [精品：Psmisc-Linux 构建指南](https://www.kancloud.cn/wizardforcel/lfs/196911)   [curl 用法](https://www.ruanyifeng.com/blog/2019/09/curl-reference.html)  [MobaXterm-xshell](https://b.hnhj9.cn/1/mx/) 
