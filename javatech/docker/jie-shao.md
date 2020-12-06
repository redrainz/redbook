1. docker与虚拟机
    1. 虚拟机：虚拟机是目前在IT架构中运用最广泛的一种虚拟化技术，它的目的主要是通过软件模拟的具有完整硬件系统功能的、运行在一个完全隔离环境中的完整计算机系统，并且提高服务器的利用率。看一下虚拟机的架构图：
    ![](/assets/20200804230340578.png)
    2. docker是一个应用容器引擎，让开发者可以打包应用以及依赖包到一个可移植的镜像中，然后发布到任何流行的Linux或Window机器上，也可以实现虚拟化。我们再来看一下Docker的架构图：
    ![](/assets/2020080423032037.png)
    3. 对比图：
    ![](/assets/截屏2020-12-06 10.33.28.png)
2. docker的下载安装
    1. https://docs.docker.com/get-docker/
3. docker的官方仓库
    1. https://hub.docker.com/
4. docker的使用（gitlab）
    1. 查找镜像 `docker search gitlab`
    2. 下载镜像 `docker pull gitlab/gitlab-ce`
    3. 查看镜像列表 `docker images`
    4. 生成容器并运行 `docker run --name gitlab -d -p 8081:80 gitlab/gitlab-ce`
    5. 查看正在运行的容器列表 `docker ps`
    6. 查看容器运行日志 `docker logs gitlab`
    7. 停止容器 `docker stop gitlab`
    8. 删除容器 `docker rm gitlab`
    9. 删除镜像 `docker rmi gitlab`
5. 自己打包镜像
    1. 编写Dockerfile
    ```yml
        FROM openjdk:8
        MAINTAINER redrain
        WORKDIR /app
        ADD dockerdemo-0.0.1-SNAPSHOT.jar /app
        EXPOSE 8080
        CMD java -jar dockerdemo-0.0.1-SNAPSHOT.jar
    ```
    2. 打包镜像 `docker build -t demo:1.0 .`
    3. 生成容器并运行 `docker run --name demo -d -p 8081:8080 demo:1.0`
6. 本地仓库
    1. 搭建简单的本地仓库
    ```
     docker pull registry
     docker run --name registry -p  5000:5000  registry
     docker build -t localhost:5000/demo:1.0 .
     docker push  localhost:5000/demo:1.0
     docker pull localhost:5000/demo:1.0     
     docker run --name demo -d -p 8081:8080 localhost:5000/demo:1.0  
    ```
7. idea对docker的支持
