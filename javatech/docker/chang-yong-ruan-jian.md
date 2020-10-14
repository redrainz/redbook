
### mysql
1. macOs
```
docker run --name mysql -d -v /Users/redrain/dockerData/mysql/conf:/etc/mysql/conf.d -v /Users/redrain/dockerData/mysql/data:/var/lib/mysql  -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root mysql

```
2. linux
```
docker run --name mysql -d -v /Users/redrain/dockerData/mysql/conf:/etc/mysql/conf.d -v /Users/redrain/dockerData/mysql/data:/var/lib/mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root mysql
```

3. 设置
```
ALTER USER root@localhost IDENTIFIED WITH mysql_native_password BY 'root'; 

ALTER USER root@'%' IDENTIFIED WITH mysql_native_password BY 'root';

FLUSH PRIVILEGES;
```

### mongo
```
docker run -p 27017:27017 -v /home/redrain/docker/mongo:/data/db --name mongo -d mongo
```

### docker-registry

1. linux
```
docker run -d -v /home/redrain/docker/registry:/var/lib/registry -p 5000:5000 --restart=always --name registry registry
```

2. 配置
```
{"insecure-registries":[66.42.69.240:5000]}
```

### gitlab
```
docker run --detach --hostname 192.168.1.10   --publish 443:443 --publish 8080:80 --publish 2222:22   --name gitlab \
    --restart always \
    --volume /home/redrain/docker/gitlab/config:/etc/gitlab \
    --volume /home/redrain/docker/gitlab/logs:/var/log/gitlab \
    --volume /home/redrain/docker/gitlab/data:/var/opt/gitlab \
    gitlab/gitlab-ce:latest
	
docker run -d \
--name gitlab-runner \
--restart always \
-v /home/redrain/docker/gitlab-runner/config:/etc/gitlab-runner \
-v /home/redrain/.m2:/root/.m2 \
 -v /var/run/docker.sock:/var/run/docker.sock \
 -v /usr/bin/docker:/usr/bin/docker  \
 -v /usr/local/bin/docker-compose:/usr/local/bin/docker-compose  \
gitlab/gitlab-runner:latest

docker exec -it gitlab-runner gitlab-runner register
  
docker exec -it gitlab-runner gitlab-ci-multi-runner register

进入gitlab-runner容器生成的配置文件 cat /etc/gitlab-runner/config.toml，如下所示：
[[runners]]
  name = "dev_build_runner"
  url = "http://gitlab.XXX.top/"
  token = "9103bafa16b1f63232323434345"
  executor = "docker"
  [runners.docker]
    tls_verify = false
    image = "mvn:3-jdk-8"
    privileged = false
    disable_cache = false
    volumes = ["/cache","/opt/data/gitlab-runner/.m2:/root/.m2"]
    pull_policy = "if-not-present"
    shm_size = 0
  [runners.cache]
	
```

### jenkins
```
docker run -p 8081:8080 -p 50000:50000 -d  -v /home/redrain/docker/jenkins-home-docker:/var/jenkins_home --name jenkins  jenkinsci/blueocean

sudo chown -R 1000:1000 /home/redrain/docker/jenkins-home-docker
```