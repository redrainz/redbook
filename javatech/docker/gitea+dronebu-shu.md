```yml
version: "2"
services: 
  gitea:
    image: gitea/gitea:latest
    container_name: gitea
    environment:
      TZ: Asia/Shanghai
    volumes:
      - /var/lib/gitea:/data
    restart: always
    networks:
      - default
    ports:
      - "10022:22"
      - "10080:3000"
 
  drone-server:
    image: drone/drone:latest
    container_name: drone-server
    ports:
      - "8080:80"
      - "8000:8000"
      - "9000:9000"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /dnmp/drone/:/var/lib/drone/:rw
    restart: always
    environment:
      - DRONE_GITEA_SERVER=http://23.105.206.60:10080
      - DRONE_GIT_ALWAYS_AUTH=false
      - DRONE_RUNNER_CAPACITY=2
      - DRONE_SERVER_HOST=23.105.206.60
      - DRONE_SERVER_PROTO=http
      - DRONE_RPC_SECRET=9c3921e3e748aff725d2e16ef31fbc42
      - DRONE_TLS_AUTOCERT=false
      - DRONE_LOGS_DEBUG=true
      - TZ=Asia/Shanghai
    restart: always
    networks:
      - default
 
  drone-agent:
    image: drone/agent:latest
    container_name: drone-agent
    command: agent
    restart: always
    depends_on:
      - drone-server
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    environment:
      #- DRONE_RPC_SERVER=http://23.105.206.60:9000
      - DRONE_RPC_SERVER=drone-server:9000
      - DRONE_RPC_SECRET=9c3921e3e748aff725d2e16ef31fbc42
      - DRONE_RUNNER_CAPACITY=2
      - DRONE_RUNNER_NAME=23.105.206.60
      - DRONE_LOGS_DEBUG=true
      - TZ=Asia/Shanghai
    restart: always
    networks:
      - default

```