
## 1. vim /etc/gitlab/gitlab.rb
```

gitlab_rails['ldap_enabled'] = true
gitlab_rails['prevent_ldap_sign_in'] = false

###! **remember to close this block with 'EOS' below**
gitlab_rails['ldap_servers'] = YAML.load <<-'EOS'
   main: # 'main' is the GitLab 'provider ID' of this LDAP server
     label: 'LDAP'
     host: '172.10.3.227'
     port: 389
     uid: 'uid'
     bind_dn: 'cn=admin,dc=caibeike,dc=com'
     password: 'admin'
     encryption: 'plain' # "start_tls" or "simple_tls" or "plain"
     verify_certificates: true
     smartcard_auth: false
     active_directory: true
     allow_username_or_email_login: true
     lowercase_usernames: false
     block_auto_created_users: false
     base: 'ou=tech,dc=caibeike,dc=com'
     user_filter: '(&(uid=*)(description=*gitlab*))'
#     ## EE only
EOS
```


## 2. gitlab-ctl reconfigure
## 3. gitlab-rake cache:clear
## 4. gitlab-rake gitlab:ldap:check
## 5. gitlab-ctl restart
