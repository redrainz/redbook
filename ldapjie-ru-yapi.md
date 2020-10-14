
```
docker run -d  -p 9090:9090  silsuer/yapi --name yapi
```

```

{
   "port": "3000",
   "adminAccount": "me@jinfeijie.cn",
   "db": {
      "servername": "mongo",
      "DATABASE": "yapi",
      "port": "27017"
   },
 "ldapLogin": {
      "enable": true,
      "server": "ldap://172.10.3.227:389",
      "baseDn": "cn=admin,dc=caibeike,dc=com",
      "bindPassword": "admin",
      "searchDn": "ou=person,dc=caibeike,dc=com",   
      "searchStandard": "&(memberOf=ou=yapi,ou=sys,dc=caibeike,dc=com)(uid=%s)",
      "emailPostfix": "@caibeike.com",
      "emailKey": "mail",
      "usernameKey": "cn"
}}

```