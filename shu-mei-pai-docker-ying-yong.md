docker run -d -p 5000:5000 --name registry-ser --restart=always  -v /home/pi/dockerData/registry:/var/lib/registry  registry
 
  
docker run --name nextcloud -p 8081:80 -v  /home/pi/outdisk/nextcloud:/var/www/html --restart=always  -d nextcloud 


docker run --name mysql -d -v /home/pi/outdisk/mysql/conf:/etc/mysql/conf.d -v /home/pi/outdisk/mysql/data:/var/lib/mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root --restart=always  192.168.2.106:5000/qics/mysql:5.7_pi 


docker run --name es -p 9200:9200 -d --restart=always pestotoast/elasticsearch-armhf