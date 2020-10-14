### jvm参数配置

```sh 
nohup mvn spring-boot:run  -Dspring-boot.run.jvmArguments="-Djava.net.preferIPv4Stack=true -Djava.awt.headless=true -Dfile.encoding=UTF-8 -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=18080 
-Dcom.sun.management.jmxremote.rmi.port=18081 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false -Djava.rmi.server.hostname=106.14.154.153 -server -Xdebug -Xnoagent -Djava.compiler=NONE
-Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=38080 -Dserver.port=8080 -Dspring.profiles.active=sit" >/dev/null 2>&1 &
```

```java
-Djava.net.preferIPv4Stack=true 
-Djava.awt.headless=true 
-Dfile.encoding=UTF-8 
-Dcom.sun.management.jmxremote 
-Dcom.sun.management.jmxremote.port=18080 
-Dcom.sun.management.jmxremote.rmi.port=18081
-Dcom.sun.management.jmxremote.authenticate=false
-Dcom.sun.management.jmxremote.ssl=false
-Djava.rmi.server.hostname=106.14.154.153 
-server 
-Xdebug 
-Xnoagent
-Djava.compiler=NONE
-Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=38080
-Dserver.port=8080 
-Dspring.profiles.active=sit
```