1. 赋予脚本文件（例：test.sh，路径：./home/pi/test.sh）可执行权限

  `sudo chmod 777 test.sh`
2. 打开/etc/rc.local文件

  `sudo vim /etc/rc.local`
3. 在/etc/rc.local文件中（语句exit 0 之上一行）添加执行脚本命令

`su - pi -c "/bin/bash /home/pi/start.sh"`
`su - root -c "/bin/bash /home/pi/frp_0.31.2_linux_arm/start.sh"`