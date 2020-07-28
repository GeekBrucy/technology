# Start mysql service
## 1. Pull mysql image
## 2. Start mysql instance(container)
```sh
docker run -d -p 3333:3306 --name CONTAINER_NAME -e MYSQL_ROOT_PASSWORD=YOUR_PWD IMAGE_ID/IMAGE_NAME:TAG
```