### linux用apt安装mysql-server

1. mysql5.7安装完成后普通用户不能进mysql
    * 原因：root的plugin被修改成了auth_socket，用密码登陆的plugin应该是mysql_native_password，直接用root权限登录就不用密码,修改root密码和登录验证方式。

2. 步骤
   
```yml
# 移除之前安装的mysql
sudo apt-get --purge remove mysql-server mysql-common mysql-client

#安装mysql-server
sudo apt-get install mysql-server mysql-common mysql-client

#更改mysql root账户认证模式
mysql
select user, plugin from mysql.user;
update mysql.user set plugin='mysql_native_password' where user='root';
flush privileges;
exit

#重启mysql-server
service mysql restart

#配置root远程登陆
grant all on *.* to root@'%' identified by '密码' with grant option;
flush privileges;
exit

#修改侦听地址127.0.0.1为0.0.0.0
vi /etc/mysql/mysql.conf.d/mysqld.cnf
bind-address = 0.0.0.0
```
