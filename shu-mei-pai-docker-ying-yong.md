docker run -d -p 5000:5000 --name registry-ser --restart=always  -v /home/pi/dockerData/registry:/var/lib/registry  registry
 
  
docker run --name nextcloud -p 8081:80 -v  /home/pi/outdisk/nextcloud:/var/www/html --restart=always  -d 192.168.2.106:5000/nextcloud:latest


docker run --name mysql -d -v /home/pi/outdisk/mysql/conf:/etc/mysql/conf.d -v /home/pi/outdisk/mysql/data:/var/lib/mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root --restart=always  192.168.2.106:5000/qics/mysql:5.7_pi 


docker run -d -p 5001:80 --name registry-web --link registry-ser -e REGISTRY_URL=http://192.168.2.106:5000/v2 chillout2k/registry-ui-arm32v6:master



docker run -d --name es  -p 9200:9200 -p 9300:9300 -v /home/pi/outdisk/elasticsearch/data:/usr/share/elasticsearch/data -v /home/pi/outdisk/elasticsearch/logs:/usr/share/elasticsearch/logs 192.168.2.106:5000/barasher/elasticsearch-arm:7.10.0