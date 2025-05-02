# 简介

代理：[v2rayA/v2rayA](https://github.com/v2rayA/v2rayA/blob/main/README_zh.md)   [快速上手-v2rayA](https://v2raya.org/docs/prologue/quick-start/)   [V2ray](https://www.v2fly.org/guide/start.html)  [神一样的工具](https://www.v2fly.org/awesome/tools.html#%E7%AC%AC%E4%B8%89%E6%96%B9%E5%9B%BE%E5%BD%A2%E5%AE%A2%E6%88%B7%E7%AB%AF)    
[ubuntu设置socks5代理](https://www.baidu.com/s?ie=utf-8&f=3&rsv_bp=1&tn=baidu&wd=ubuntu%E8%AE%BE%E7%BD%AEsocks5%E4%BB%A3%E7%90%86&rn=20&oq=ubuntu%25E4%25BB%25A3%25E7%2590%2586%25E8%25AE%25BE%25E7%25BD%25AE&rsv_pq=a665cb2c00d639b9&rsv_t=3da5j61fJG%2BK0CeD6QUiEnYy%2B2I614jRZeif6dctBMqzO0PSnINnX5khEfw&rqlang=cn&rsv_enter=1&rsv_dl=ts_0&rsv_sug3=5&rsv_sug1=6&rsv_sug7=100&rsv_sug2=0&rsv_btype=t&prefixsug=ubuntu%25E8%25AE%25BE%25E7%25BD%25AEsoc&rsp=0&inputT=5042&rsv_sug4=5343)   [ubuntu搭建socks5代理服务器](https://www.volcengine.com/theme/2365101-U-7-1)   [Ubuntu中设置代理的3种方式](https://blog.csdn.net/tiansyun/article/details/137260116)   [ubuntu系统代理](https://blog.csdn.net/yubangfan/article/details/130890159) 

[windows代理软件](https://cloud.tencent.com/developer/article/2059535) 

翻墙

[Linux系统翻墙方法](https://github.com/Alvin9999/new-pac/wiki/Linux%E7%B3%BB%E7%BB%9F%E7%BF%BB%E5%A2%99%E6%96%B9%E6%B3%95) 

原理：[了解架构 | V2ray](https://www.v2fly.org/developer/intro/design.html) 

```sh
systemctl start v2raya.service 
http://192.168.1.130:2017/
# 为局域网中的其他机器提供代理: 打开“局域网共享”,  20170(socks5), 20171(http), 20172(带分流规则的http)
```

# 系统代理设置

[ubuntu系统代理设置](https://blog.csdn.net/yubangfan/article/details/130890159)  [Ubuntu中设置代理的方式](https://blog.csdn.net/tiansyun/article/details/137260116?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-0-137260116-blog-52463140.235^v43^pc_blog_bottom_relevance_base9&spm=1001.2101.3001.4242.1&utm_relevant_index=3)  

[Ubuntu设置全局socks代理](https://blog.csdn.net/weixin_45033342/article/details/118075525?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-0-118075525-blog-138450199.235^v43^pc_blog_bottom_relevance_base9&spm=1001.2101.3001.4242.1&utm_relevant_index=3) 

[ubuntu设置系统代理_百度搜索](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=ubuntu%E8%AE%BE%E7%BD%AE%E7%B3%BB%E7%BB%9F%E4%BB%A3%E7%90%86&oq=%25E9%2580%258F%25E6%2598%258E%25E4%25BB%25A3%25E7%2590%2586&rsv_pq=c8be33f1001aefca&rsv_t=fc0fSdoIhxqdb3GEOKk9V%2FAPzQrs2W6c16Ko7icNGIA5mJtMuwn0CTvG6GY&rqlang=cn&rsv_dl=tb&rsv_enter=1&rsv_sug3=27&rsv_sug1=3&rsv_sug7=100&rsv_sug2=0&rsv_btype=t&inputT=9121&rsv_sug4=14425) 

设置SOCKS5代理通常涉及到环境变量的设置

```sh
nano /etc/environment

```

# 透明代理

[Ubuntu使用Dante建立Socks5代理](https://blog.csdn.net/qq_44839815/article/details/138450199) 

# v2raya

[V2Ray 路由规则文件加强版](https://github.com/Loyalsoldier/v2ray-rules-dat) 

[V2Ray手动安装](https://3385706034.gitbook.io/note/v2ray-install) 

**排错：** [Special user nobody …”错误](https://1024.day/d/2674)   [systemd 报错 Special user nobody configured](https://www.vvave.net/archives/fix-the-systemd-error-special-user-nobody-configured-this-is-not-safe.html)

```sh
# vi /etc/systemd/system/v2ray.service，  User=nobody 改 DynamicUser=true

systemctl daemon-reload
```



# github不能访问

[GitHub 访问不了](https://www.zhihu.com/question/641492668/answer/3377851976) [GitHub520项目](https://search.gitee.com/?skin=rec&type=repository&q=github520) [521xueweihan/GitHub520](https://github.com/521xueweihan/GitHub520) [Linux缓存服务NSCD_让更新后的host生效](https://cloud.tencent.com/developer/article/2242697)  [NSCD--DNS缓存服务](https://blog.csdn.net/zzhongcy/article/details/89089404) [GitHub520使用](https://gitee.com/klmahuaw/GitHub520?_from=gitee_search)  [SwitchHosts管理hosts](https://github.com/oldj/SwitchHosts/blob/master/README.zh_hans.md)    

[GitHub.com - ipaddress.com查询](https://sites.ipaddress.com/github.com/)   [用git下载：Connection refused,修改hosts](https://baijiahao.baidu.com/s?id=1771113174952216681&wfr=spider&for=pc) 

[centos安装nscd 清除DNS缓存](https://blog.csdn.net/weixin_39857866/article/details/125819371)   [通过ipaddress更新github的hostsIP](https://zhuanlan.zhihu.com/p/681350679)  

[Elegycloud/clash-for-linux-backup](https://github.com/Elegycloud/clash-for-linux-backup)   [centos7设置代理上网](https://www.baidu.com/s?ie=UTF-8&wd=centos7%E8%AE%BE%E7%BD%AE%E4%BB%A3%E7%90%86%E4%B8%8A%E7%BD%91)  [CentOS7下代理配置](https://cloud.tencent.com/developer/article/1743003)  [Centos7 代理服务器上网](https://blog.csdn.net/justlpf/article/details/105427091) [centos7 设置网络代理 ](https://www.cnblogs.com/cxygg/p/17993107)   [V2Ray搭建详细图文教程 · 233boy/v2ray Wiki](https://github.com/233boy/v2ray/wiki/V2Ray%E6%90%AD%E5%BB%BA%E8%AF%A6%E7%BB%86%E5%9B%BE%E6%96%87%E6%95%99%E7%A8%8B) 

NSCD的主要作用是缓存名称服务查询的结果，可以加快名称服务查询的速度，查询结果不必每次都从网络或本地DB(**/var/cache/nscd**)中获取，所以能一定程度上减少对网络和本地[数据库](https://cloud.tencent.com/solution/database?from_column=20065&from=20065)的负载。也正因为此特性，如果缓存的查询结果过时或不准确，可能会导致应用程序出现错误或安全问题。此外，如果nscd服务出现故障，可能会导致名称服务查询失败或变慢。

同时，nscd可以缓存多种名字服务数据库，包括hosts、passwd、group、services、netgroup等。对于每种数据库，nscd都可以配置其缓存大小、生存时间等参数，以满足不同的需求。

总之，nscd是一个优秀的Name Service缓存守护进程，可以提高系统的名字服务性能，但是在实际应用中需要注意配置参数，避免出现缓存不一致等问题

**git设置代理**

[git设置代理和取消代理](https://blog.csdn.net/zwhfyy/article/details/130739079)   

**nscd**

```sh
yum -y install nscd
service nscd status  start   
nscd -i hosts					# 清除dns缓存
```




```sh
# kubeadm init搞了3天，最后上代理成功了，就是镜像下不了；  http://192.168.1.130:2017/
# v2rayA开放端口： 20170(socks5), 20171(http), 20172(带分流规则的http) 端口
# 临时代理
systemctl start v2raya.service
export http_proxy="192.168.1.130:20171"
export https_proxy="192.168.1.130:20172"
export ALL_PROXY=socks5://192.168.1.130:20170
# 设置开机自动启动
systemctl enable v2raya.service

# 取消代理
unset http_proxy
unset https_proxy
unset ALL_PROXY
```

# 节点订阅

订阅:[v2rayShare](https://v2rayshare.com/p/3314.html)   [v2ray节点订阅](https://github.com/aiboboxx/v2rayfree)  [clash节点](https://clashgithub.com/clashnode-20240614.html?feed_id=206&_unique_id=666b522ece106)   [v2ray节点订阅](https://github.com/aiboboxx/v2rayfree)   [免费节点订阅](https://www.freeclashnode.com/free-node/2024-4-28-free-subscribe-node.htm)   [anaer/Sub: 自用clash订阅链接](https://github.com/anaer/Sub?tab=readme-ov-file) 

# vpn

==出入站代理==： [入站代理 | Project X](https://xtls.github.io/config/inbound.html)     

[代理入站出站什么意思 - Google 搜索](https://www.google.com/search?q=%E4%BB%A3%E7%90%86%E5%85%A5%E7%AB%99%E5%87%BA%E7%AB%99%E4%BB%80%E4%B9%88%E6%84%8F%E6%80%9D&newwindow=1&sxsrf=ADLYWIKgqkfbch2wQ7DSgoyQ6l39mZCwxw%3A1720328215210&iflsig=AL9hbdgAAAAAZoouJzfwur40Zg0x5geLptQTRcNK393_&uact=5#ip=1)    [隧道技术和代理技术](https://swq111.online/index.php/2024/03/04/%E9%9A%A7%E9%81%93%E6%8A%80%E6%9C%AF%E5%92%8C%E4%BB%A3%E7%90%86%E6%8A%80%E6%9C%AF%EF%BC%88%E4%B8%80%EF%BC%89/)   [客户端出站vmess+tcp+tls 服务器入站vmess+tcp+tls. ](https://github.com/XTLS/Xray-examples/issues/171)  

==DNS分流== :  [Shadowrocket DNS分流](https://www.ahaspeed.com/zh-hans/blogs/shadowrocket-dnsruhefenliu) [DNS分流与泄露分析 ](https://apad.pro/dns-leak/)  [什么是dns分流 - Google 搜索](https://www.google.com/search?q=%E4%BB%80%E4%B9%88%E6%98%AFdns%E5%88%86%E6%B5%81&newwindow=1&sxsrf=ADLYWIISe_SQMm2tmmSnPRZz5CmuKnH5fQ%3A1720328994959&iflsig=AL9hbdgAAAAAZooxMvu7JAMd6S3v2DNuyvWZRIQRtgvE&uact=5)       [SmartDNS 从入门到精通（二：DNS分流）](https://yangpin.link/archives/1733.html) 

- **入站代理**： 保护服务器和==优化到服务器的流量==
  - 入站： ==进入==某个系统或网络==的数据流== 
  - **入站配置：  定义，如何处理进入代理服务器的数据**  
  - 阻挡或者允许特定程序或者端口进行连接
- **出站代理：** 控制和优化==从客户端到外部网络的流量== 
- **DNS分流**: 通过==不同的DNS==服务器来==解析不同的域名==;  实现网络连接的个性化管理
  - 分流器主要有两种用途： 分流哪些网站需要通过透明代理访问、分流DNS解决结果污染问题
  - 用户可以将常用的网站域名解析到速度较快的DNS服务器，而将广告和恶意域名解析到拥有过滤功能的DNS服务器，从而提高浏览速度和网络安全性
  - 用户希望加速访问视频网站，同时又想屏蔽广告
- ==路由==才是 sing-box 的核心配置 
  - 如何处理不同的网络请求
  - 处理复杂的路由需求，包括基于地理位置、IP 地址、端口号、域名等多种条件的==流量分流== 

## sing-box

[SagerNet/sing-box: The universal proxy platform](https://github.com/SagerNet/sing-box)      

[AMD64的4个架构级别 v1 v2 v3 v4_amd64 v3](https://blog.csdn.net/u010953692/article/details/130604154) 



|   程序   |           /usr/bin/sing-box            |
| :------: | :------------------------------------: |
|   配置   |       /etc/sing-box/config.json        |
| 工作目录 |           /var/lib/sing-box            |
| 查看日志 | journalctl -u sing-box --output cat -e |
| 实时日志 |    journalctl -u sing-box -o cat -f    |

[sing-box安装](https://blog.csdn.net/qq562920276/article/details/137365200) 

geoip database已经下载到/etc/sing-box/

```sh
# --purge会把配置也删除，保留配置请移除该参数
systemctl stop sing-box.service
systemctl disable sing-box.service
dpkg --purge sing-box
```



### 客户端

**windows**：  [hiddify](https://github.com/hiddify/hiddify-next/blob/main/README_cn.md)     [GUI.for.SingBox](https://github.com/GUI-for-Cores/GUI.for.SingBox) 

[nekoray](https://github.com/MatsuriDayo/nekoray?tab=readme-ov-file)  [客户端下载](https://butterfly.duckgogo.top/blog/download/)  [Sing-Box使用教程](https://butterfly.duckgogo.top/blog/sing-box-tutorial/)  [sing-box-yes](https://github.com/FranzKafkaYu/sing-box-yes) 

### 配置

[放弃fakeip，拥抱realip，最强网络代理工具sing-box](https://www.youtube.com/watch?v=BAfbkLizFGc&t=121s) 

[sing-box 的配置方法](https://icloudnative.io/posts/sing-box-tutorial/) 

#### DNS 配置

#### 路由配置

#### 入站配置

#### 出站配置