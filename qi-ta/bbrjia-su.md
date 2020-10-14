# 开启BBR

`https://raw.githubusercontent.com/teddysun/across/master/bbr.sh` BBR脚本链接

`curl -O https://raw.githubusercontent.com/teddysun/across/master/bbr.sh && sh bbr.sh` 脚本自动安装
# 验证
查看可以用的拥塞控制算法
sysctl net.ipv4.tcp_available_congestion_control
得到结果

net.ipv4.tcp_available_congestion_control = reno cubic bbr

查看现在使用的拥塞控制算法

sysctl net.ipv4.tcp_congestion_control
得到结果

net.ipv4.tcp_congestion_control = bbr

检查BBR是否正常运行

lsmod | grep tcp_bbr
tcp_bbr 20480 1

速度测试
创建一个文件,搭建http服务

dd if=/dev/zero of=500mb.zip bs=1024k count=500
访问 http://[your-server-IP]/500mb.zip 来测试下载速度~

