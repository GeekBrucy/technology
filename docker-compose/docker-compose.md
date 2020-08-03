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
use docker-compose execute the following
> because gitlab requires port 22, the default ssh port is 22 as well. So 
> the default ssh needs to be changed to some other port
```sh
# open sshd_config
vi /etc/ssh/sshd_config
# find PORT setting and change it to something else

# restart ssh
systemctl restart sshd
```

```yml
version: '3.4'
services:
 gitlab:
  image: 'gitlab/gitlab-ce:latest'
  container_name: "gitlab"
  restart: always
  privileged: true
  hostname: 'gitlab'
  environment:
   TZ: 'Australia/Canberra'
   GITLAB_OMNIBUS_CONFIG: |
    external_url 'http://192.168.199.110'
    gitlab_rails['time_zone'] = 'Australia/Canberra'
    gitlab_rails['smtp_enable'] = true
    gitlab_rails['gitlab_shell_ssh_port'] = 22
  ports:
   - '80:80'
   - '443:443'
   - '22:22'
  volumes:
   - /opt/docker_gitlab/config:/etc/gitlab
   - /opt/docker_gitlab/data:/var/opt/gitlab
   - /opt/docker_gitlab/logs:/var/log/gitlab
```
### 2. Build Gitlab-Runner