- ## Spring Boot Dockerfile

```yml
    FROM  maven:3-jdk-8

    WORKDIR /app

    ADD demo-0.0.1-SNAPSHOT.jar /app

    EXPOSE  8080

    CMD [ "java","-jar","/app/demo-0.0.1-SNAPSHOT.jar" ]
```

- ## React Dockerfile

```yml
    FROM nginx:latest

    WORKDIR /usr/share/nginx/html


    RUN rm -rf /usr/share/nginx/html/

    COPY build/. /usr/share/nginx/html/

    EXPOSE 80

    CMD /bin/sh -c 'nginx -g "daemon off;"'
```

- ## React docker-build.sh

```sh
    #!/usr/bin/env bash
    npm run build

    rm -rf docker/build

    cp -r build docker/

    cd docker/

    docker build -t react:v1.0 .

    docker stop react

    docker rm react

    docker run --name react -p 80:80 -d  react:v1.0
```