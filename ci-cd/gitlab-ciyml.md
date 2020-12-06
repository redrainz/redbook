## .gitlab-ci.yml

```yml
stages:
- test
- build
- deploy
- run

test:
  stage: test
  script:
  - echo "mvn test"
  - mvn clean
  - mvn test
  tags:
  - shell

build:
  stage: build
  script:
  - echo "mvn install"
  - mvn install
  - cp target/demo-0.0.1-SNAPSHOT.jar docker/
  - cd docker/
  - docker build -t 192.168.1.10:8082/demo/demo .
  tags:
  - shell
  only:
    refs:
    - master
    
deploy:
  stage: deploy
  script:
  - echo "push docker"
  - docker login -u redrain -p Rootroot1 192.168.1.10:8082
  - docker push 192.168.1.10:8082/demo/demo
  - docker rmi 192.168.1.10:8082/demo/demo
  tags:
  - shell
  only:
    refs:
    - master
    
run:
  stage: run
  script:
  - echo 'run'
  - docker-compose up -d
  tags:
  - shell
  only:
    refs:
    - master
    
```