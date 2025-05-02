Centos官方建议的方式来实现开机启动脚本：

1. 新建your_startup.service文件

   ```bash
   # touch /usr/lib/systemd/system/your_startup.service
   ```
   
2. 编辑your_startup.service文件

   ```bash
   [Unit]
   Description=start your_startup service
   Requires=graphical.target
   After=graphical.target
   [Service]
   Type=forking
   User=root
   Group=root
   Restart=always
   TimeoutSec=5
   IgnoreSIGPIPE=no
   KillMode=process
   GuessMainPID=no
   RemainAfterExit=no
   ExecStart=/etc/rc.d/init.d/your_startup.sh
   [Install]
   WantedBy=graphical.target
   ```
   
3. /etc/rc.d/init.d目录下创建启动脚本your_startup.sh；并编辑脚本

   ```bash
   #! /bin/bash
   #
   # description:      startup shell 
   
   sudo systemctl start nfs.service
   ```
3. your_startup.sh启动脚本增加执行权限

   ```shell
   # chmod 755 /etc/rc.d/init.d/your_startup.sh
   ```
   
4. 配置开机启动

   ```bash
   # systemctl enable /usr/lib/systemd/system/your_startup.service
   ```
   
5. 重启

6. 查看 your_startup.sh 是否成功启动？