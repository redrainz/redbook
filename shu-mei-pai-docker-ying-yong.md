 docker run --name nextcloud -p 8081:80 -v  /home/pi/outdisk/nextcloud:/var/www/html --restart=always  -d nextcloud 


docker run --name mysql -d -v /home/pi/outdisk/mysql/conf:/etc/mysql/conf.d -v /home/pi/outdisk/mysql/data:/var/lib/mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root --restart=always  qics/mysql:5.7_pi 