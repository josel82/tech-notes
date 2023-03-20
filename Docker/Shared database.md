# Shared database
#Docker #DevOps #Networking 

1. Create a network
```bash
docker network create mysql-network
```
This command will create a bridged network with name "mysql-network"

2. Set up the database stack 
`docker-compose.yaml`
```yaml
version: '3.1'
services:
	db:
		image: yobasystems/alpine-mariadb
		environment:
			- MYSQL_ROOT_PASSWORD: password
		volumes:
			- ./data/example/mysql:/var/lib/mysql
		restart: always
	phpmyadmin:
		image: phpmyadmin
		restart: always
		ports:
			- 8080:80
		environment:
			- PMA_ARBITRARY=1
networks:
	default:
		name: mysql-network
		external: true 
```

3. Configure database
Log in to Phpmyadmin and create databases, users and passwords for the respective services
`http://host_ip:8080` 


4. Add other containers
```bash
docker run --rm \
-p 8081:80 \
-e WORDPRESS_DB_HOST=db \
-e WORDPRESS_DB_USER=wordpress_usr \
-e WORDPRESS_DB_PASSWORD=wordpress123 \
-e WORDPRESS_DB_NAME=wordpress_db \
-v $(pwd)/data/wordpress:/var/www/html \
--network mysql-network \
--name wordpress \
-d wordpress
```
or
`docker-compose.yaml`
```yaml
version: '3'
services:
	wordpress:
		image: wordpress
		restart: always
	    ports:
	      - 8081:80
	    environment:
	      WORDPRESS_DB_HOST: db
	      WORDPRESS_DB_USER: wordpress_usr
	      WORDPRESS_DB_PASSWORD: wordpress123
	      WORDPRESS_DB_NAME: wordpress_db
	    volumes:
	      - ./data/wordpress:/var/www/html
networks:
	default:
		name: mysql-network
		external: true
```
then run:
```bash
docker-compose up -d
```
