# Docker-Compose
## 1. download docker-compose from github

## 2. Assign execute permission to the downloaded file (Linux only)

# docker-compose.yml
> DO NOT use tab in docker-compose.yml file
```yml
version: '3.4'
services:
  mysql:
    restart: always # the container will start up with docker
    image: mysql:8.0.21
    container_name: mysql_ctn
    ports:
      - 6033:3306
    environment:
      MYSQL_ROOT_PASSWORD: root
      TZ: Australia/Canberra
    volumes:
      - "F:/MyProj/learn_docker/docker_mysql_tomcat/db_data:/var/lib/mysql"
  
  tomcat:
    restart: always
    image: tomcat:latest
    container_name: tomcat_ctn
    ports:
      - 6437:8080
    environment:
      TZ: Australia/Canberra
    volumes:
      - "F:/MyProj/learn_docker/docker_mysql_tomcat/webapp_data:/usr/local/tomcat/webapps"
      - "F:/MyProj/learn_docker/docker_mysql_tomcat/webapp_logs:/usr/local/tomcat/logs"
```

# docker-compose commandss
> docker-compose command will seek docker-compose.yml file in current directory

```sh
# 1 start up containers based on docker-compose.yml
docker-compose up -d

# 2 Stop and remove containers
docker-compose down

# 3 Start/Close/restart existing containers created by docker-compose
docker-compose start|stop|restart

# 4 list containers maintained by docker-compose
docker-compose ps

# 5 check log
docker-compose logs -f
```

# docker-compose with Dockerfile
> use docker-compose.yml and Dockerfile to generate customised image and start the image

```yml
#yml file
version: '3.4'
services:
  webapp:
    restart: always
    build:
      context: ../                # dockerfile directory
      dockerfile: Dockerfile      # dockerfile file name
    image: webapp: 1.0.0
    container_name: webapp
    ports:
      - 1234:8080
    environment:
      TZ: Australia/Canberra
```

```sh
# Dockerfile
FROM some_docker_image:tag
COPY local_app_dir container_dir
```

# Docker CI, CD
## Preface
>Project Deployment  
>1. Compile the project  
>2. Upload the compiled file to the server  
>3. Move the compiled file to web server dir  
>4. Convert the compiled file and web server into an image via Dockerfile, and use docker-compose to run the container  

## CI (continuous integration)
### 1. Build Gitlab Server
