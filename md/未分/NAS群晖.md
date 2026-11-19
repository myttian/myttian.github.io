### 一. 黑群晖

[【虚拟机】安装黑群晖6.17](https://blog.csdn.net/xmzmqx/article/details/106334122?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-1-106334122-blog-116211112.pc_relevant_default&spm=1001.2101.3001.4242.2&utm_relevant_index=3)  [下载中心 - DS3615xs | Synology 群晖科技](https://www.synology.cn/zh-cn/support/download/DS3615xs?version=6.1#utilities)    

视频： [黑群晖半洗白-利用docker ](https://www.bilibili.com/read/cv7448789/) 

[ CentOS7 磁盘管理](https://blog.51cto.com/u_11990719/3160378)  [ Centos7磁盘管理](https://blog.csdn.net/zhj_1121/article/details/124580169)  

#### 1. 安装6.17

[docker国内加速](http://t.zoukankan.com/edda-p-13365394.html) [群晖docker套件加速下载注册表](https://www.jianshu.com/p/93e32ab0764b)  [黑群晖NAS安装方法](http://t.zoukankan.com/EasonJim-p-9754412.html) [ minikube启动出错](https://blog.csdn.net/believe_ordinary/article/details/119046138) [改docker配置](https://k8s.easydoc.net/docs/dRiQjyTY/28366845/6GiNOzyZ/nd7yOvdY)  [CentOS7 启动docker.service失败](https://segmentfault.com/q/1010000002392472) [How to change the cgroup driver from cgroupfs systemd in docker](https://www.devopsschool.com/blog/how-to-change-the-cgroup-driver-from-cgroupfs-systemd-in-docker/)

[检查cgroup v2 是否安装](http://t.zoukankan.com/rongfengliang-p-10930455.html)

```
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": [
  "https://paegq6fr.mirror.aliyuncs.com",
  "http://f1361db2.m.daocloud.io",
  "https://registry.docker-cn.com",
  "http://hub-mirror.c.163.com",
  ],
  "dns": ["8.8.8.8","8.8.4.4"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

```bash
# kubernetes 官方推荐 docker 等使用 systemd 作为 cgroupdriver，否则 kubelet 启动不了
cat <<EOF > daemon.json
{
  "registry-mirrors": [
  "https://paegq6fr.mirror.aliyuncs.com",
  "http://f1361db2.m.daocloud.io",
  "https://registry.docker-cn.com",
  "http://hub-mirror.c.163.com",
  ],
  "exec-opts": ["native.cgroupdriver=systemd"]
}
EOF
mv daemon.json /etc/docker/

# 重启生效，配置国内镜像，并且镜像文件为/etc/docker/daemon.json，修改后缀为.conf即可正常启动docker服务
#vi /usr/lib/systemd/system/docker.service； ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock --exec-opt native.cgroupdriver=systemd
systemctl daemon-reload
systemctl restart docker
docker info|grep Cgroup
```

```bash
grep cgroup /proc/filesystems； #检查cgroup v2 

查找Docker-CE的版本:
# yum list docker-ce.x86_64 --showduplicates | sort -r
安装指定版本的Docker-CE: (VERSION例如上面的17.03.0.ce.1-1.el7.centos)
# sudo yum -y install docker-ce-[VERSION]
```

准备：

synology-assistant(官网下载)

 XPEnology_DS3615xs_DSM_6.1.x-quicknick-3.0(用里面.vmdk引导)

DSM_DS3615xs_15284.pat

1. vmware使用现有磁盘装入.vmdk，添加20G sata磁盘；
2. 开启vmware，待出现booting the rernel，在物理机安装synology-assistant，本工具会自动查找局域网的群晖系统，会看到DSM未安装，并选中右击选择安装*.pat。
3. 待安装完成，在synology-assistant中会看到“状态”为“已就绪”，右击选择联机，在打开的浏览器中输入用户名密码登陆。
4. 关闭自动更新：控制面板—更新和还原—更新设置—仅重要更新即可，再选择—任务计划—选中并删除掉更新的计划

#### 2.外网访问

[外网访问NAS黑群晖6.17](https://blog.csdn.net/xmzmqx/article/details/106341502?ops_request_misc=%7B%22request%5Fid%22%3A%22165475342616781818713873%22%2C%22scm%22%3A%2220140713.130102334.pc%5Fblog.%22%7D&request_id=165475342616781818713873&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_ecpm_v1~rank_v31_ecpm-1-106341502-null-null.nonecase&utm_term=外网访问黑群晖&spm=1018.2226.3001.4450)  

EZ-internet

#### 3. Docker

[黑群晖半洗白-利用docker](https://www.bilibili.com/read/cv7448789/)  [1.【home-assistant】智能家居系统](https://www.bilibili.com/video/BV1EV411t7QD?spm_id_from=333.999.0.0)  [入坑Homeassistant ](https://www.bilibili.com/video/BV1VL411P7ZF/?spm_id_from=333.788.recommend_more_video.16)   [Vtiger CRM 安装使用常见问题及解答 FAQ ](https://maie.name/711.html) [群晖基础教程 docker参数](https://www.bilibili.com/video/BV1P5411u7Tj/?spm_id_from=333.788.recommend_more_video.13&vd_source=7346303e5e18677d7261c2c0c109ecfd)

[docker-vtiger (github.com)](https://github.com/Websoft9/docker-vtiger/blob/main/README-zh.md)   [VtigerCRM | PHP 开源应用](https://support.websoft9.com/docs/lamp/installation/zh/vtiger.html#vtigercrm-初始化安装向导)    [ 企业管理软件：镜像部署与使用实战 ](https://www.kancloud.cn/websoft9/enterprise-software-practice/608307)   [vtigercrm学习](https://www.cnblogs.com/xubuhang/p/3998109.html) [轻松安装VtigerCRM ](https://cloud.tencent.com/developer/article/1829948)   

#### 4. 宝塔面板

[忘记宝塔面板密码](https://www.bt.cn/bbs/thread-1172-1-1.html)  [宝塔面板下载](https://www.bt.cn/new/download.html)  [crm系统VtigerCRM 7.3 保姆级安装教程](https://blog.csdn.net/microspore/article/details/108994796) 

unzip 需要解压的.zip文件 -d 解压后的目录位置

### 二、免费开源NAS

#### 1. NextCloud

[NextCloud安装](https://cloud.tencent.com/developer/article/1897454) 

