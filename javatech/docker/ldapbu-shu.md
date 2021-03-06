# ldap
---

```yml
version: '2'
services:
openldap:
image: osixia/openldap:1.4.0
container_name: openldap
environment:
LDAP_LOG_LEVEL: "256"
LDAP_ORGANISATION: "Caibeike Inc."
LDAP_DOMAIN: "caibeike.com"
LDAP_BASE_DN: ""
LDAP_ADMIN_PASSWORD: "admin"
LDAP_CONFIG_PASSWORD: "config"
LDAP_READONLY_USER: "false"
#LDAP_READONLY_USER_USERNAME: "readonly"
#LDAP_READONLY_USER_PASSWORD: "readonly"
LDAP_RFC2307BIS_SCHEMA: "false"
LDAP_BACKEND: "mdb"
LDAP_TLS: "true"
LDAP_TLS_CRT_FILENAME: "ldap.crt"
LDAP_TLS_KEY_FILENAME: "ldap.key"
LDAP_TLS_DH_PARAM_FILENAME: "dhparam.pem"
LDAP_TLS_CA_CRT_FILENAME: "ca.crt"
LDAP_TLS_ENFORCE: "false"
LDAP_TLS_CIPHER_SUITE: "SECURE256:-VERS-SSL3.0"
LDAP_TLS_VERIFY_CLIENT: "demand"
LDAP_REPLICATION: "false"


KEEP_EXISTING_CONFIG: "false"
LDAP_REMOVE_CONFIG_AFTER_SETUP: "true"
LDAP_SSL_HELPER_PREFIX: "ldap"
tty: true
stdin_open: true
# volumes:
# - /var/lib/ldap
# - /etc/ldap/slapd.d
# - /container/service/slapd/assets/certs/
ports:
- "389:389"
- "636:636"
# For replication to work correctly, domainname and hostname must be
# set correctly so that "hostname"."domainname" equates to the
# fully-qualified domain name for the host.
domainname: "caibeike.com"
hostname: "ldap"
phpldapadmin:
image: osixia/phpldapadmin:latest
container_name: phpldapadmin
environment:
PHPLDAPADMIN_LDAP_HOSTS: "openldap"
PHPLDAPADMIN_HTTPS: "false"
ports:
- "8080:80"
depends_on:
- openldap

```

## 2.查询

1. 进入容器 执行 `ldapsearch -x -H ldap://localhost:389 -b dc=caibeike,dc=com -D "cn=admin,dc=caibeike,dc=com" -w admin`

## 3.登录
1. http://127.0.0.1:8080/
2. 用户DN: `cn=admin,dc=caibeike,dc=com`
3. 用户密码: `admin`