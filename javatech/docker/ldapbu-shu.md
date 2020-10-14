## 1.docker-compose.yml
---


## 2.查询
进入容器 执行  `ldapsearch -x -H ldap://localhost:389 -b dc=caibeike,dc=com -D "cn=admin,dc=caibeike,dc=com" -w admin`

## 3.登录 
http://127.0.0.1:8080/   
用户DN: `cn=admin,dc=caibeike,dc=com`
用户密码: `admin`
