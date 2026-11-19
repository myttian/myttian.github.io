视频教程：

[go-gin-gorm-vue](https://www.gin-vue-admin.com/guide/video/golang.html) 

[百度网盘movie108-狂神](https://yun.baidu.com/disk/main?_at_=1720777188700#/index?category=all&path=%2F%E5%B7%A5%E5%AD%A6%2F%E8%AE%A1%E7%AE%97%E6%9C%BA%2Fgo%2F%E7%8B%82%E7%A5%9Eweb%E5%85%A8%E6%A0%88%E7%9B%B4%E6%92%AD%E8%AF%BE%28%E5%90%8E%E7%AB%AFGolang%29%20%E5%B8%A6%E6%BA%90%E7%A0%81)    

# orm框架

[Go语言Gin框架+Gorm实战CRUD](https://blog.csdn.net/ecloud_developer/article/details/135134752) 

[sqlx](https://cloud.tencent.com/developer/article/2343867)  [Go语言sqlx框架](https://blog.csdn.net/universsky2015/article/details/135786769)  [sqlx和gorm性能对比](https://cloud.tencent.com/developer/article/2056863) 

[xorm](https://cloud.tencent.com/developer/article/2343872) [XORM](https://blog.csdn.net/qq_45467608/article/details/137918926)   [xorm框架](https://www.cnblogs.com/yigongsui/articles/17158131.html) 

[web框架：Iris](https://blog.csdn.net/weixin_45565886/article/details/130691064)   [Iris](https://blog.csdn.net/gitblog_00051/article/details/139018445)   [iris框架的路由底层结构](https://cloud.tencent.com/developer/article/2211990) 

[Gin框架简介](https://www.kancloud.cn/jiajunxi/ginweb100/1801414)   [gin框架_百度搜索](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=gin%E6%A1%86%E6%9E%B6&oq=gin&rsv_pq=fa5dc64f003c3a05&rsv_t=7985Axg1294nSCJ5bTIwoJCKByJLxEafWc6ilOU7wv0QBooF9C8%2B%2FWfkvik&rqlang=cn&rsv_enter=1&rsv_dl=tb&rsv_sug3=7&rsv_sug1=3&rsv_sug7=100&bs=gin)  [gin框架](https://cloud.tencent.com/developer/article/2350920)   [gin框架的模板渲染的实现](https://www.jb51.net/jiaoben/301694vhb.htm) 

[Beego：Go 应用框架](https://cloud.tencent.com/developer/article/1541826)  [Beego](https://cloud.tencent.com/developer/article/1706320)  [Beego Architecture](https://blog.csdn.net/JunChow520/article/details/111720639)  [beego谁开发的](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&tn=baidu&wd=beego%E8%B0%81%E5%BC%80%E5%8F%91%E7%9A%84&oq=beego&rsv_pq=f629f15c0093c45f&rsv_t=9282kO9iNVtsuZnPmvlO9TYZmWtjmvpeZCejAAnymf9tpLfX%2BRr1gVSWMN0&rqlang=cn&rsv_enter=1&rsv_dl=tb&rsv_sug3=15&rsv_sug1=14&rsv_sug7=100&rsv_sug2=0&rsv_btype=t&inputT=8696&rsv_sug4=8696)  [Beego_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=Beego) 

跨平台文件监听:  [fsnotify库](https://cloud.tencent.com/developer/article/2328778)  [配置解决方案viper](https://cloud.tencent.com/developer/article/2328457)   [fsnotify_百度搜索](https://www.baidu.com/s?ie=UTF-8&wd=fsnotify) 

- Gin ： 构建 HTTP 服务器的 web 框架
- Gorm： Go 的一个 ORM（对象关系映射）库。它提供了一个简单易用的 API，用于与数据库交互
- sqlx: 基于 Go 语言的数据库访问库
- xorm:  Go语言 ORM（对象关系映射）库
- iris: 用Go开发的web应用框架，被称为速度最快的Go后端开发框架
- gin: 轻量级的Go语言Web框架
- beego: 快速开发 Go 应用的 HTTP 框架
- 

# iris框架

# Gin框架

# Beego框架

# GVA

[gin-vue-admin | GVA 文档站](https://www.gin-vue-admin.com/)     [项目介绍 | Gin-Vue-Admin](https://www.gin-vue-admin.com/guide/introduce/project.html)  

vue3 + vite + js(ts)

GVA技术选型：

- 前端：  用基于vue3的Element-Plus构建基础页面
- 后端：  用Gin快速搭建基础API，Gin是一个go语言编写的Web框架
- 数据库：采用MySql>5.7版本,数据库引擎 innoDBimportant，使用gorm实现对数据库的基本操作,目前已支持Sqlite,PostgreSQL(人大金仓),Mssql,Oracle
- 缓存：  使用Redis进行一系列缓存操作，默认关闭，如果需要可自行到配置中开启
- API文档：使用Swagger构建自动化文档
- 配置文件：使用fsnotify和viper实现yaml格式的配置文件
- 日志：   使用zap实现日志记录。