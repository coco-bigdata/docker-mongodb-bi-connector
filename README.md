# Mongodb BI Connector

this docker image for mongodb-bi-connector.

## Security / Auth

This bi-connector assume that your mongodb server can connect without any authentication (trusted network).
"*Authentication in MongoDB is fairly complex*". Thats the reason to make this bi-connector is simple as possible for now.

## docker-compose example

```
version: "3"
services:
  mongodb:
    image: mongo
    container_name: mongodb
    restart: always
    ports:
      - 27017:27017
    volumes:
      - "./mongodb/configdb:/data/configdb"
      - "./mongodb/db:/data/db"
      - /etc/localtime:/etc/localtime
    networks:
      - sgcc-network
    # command: mongod --auth
    environment:
      - MONGO_INITDB_ROOT_USERNAME=root       #初始化管理员用户名和密码
      - MONGO_INITDB_ROOT_PASSWORD=123456
      - TZ="Asia/Shanghai"
    tty: true
  
  mongodb-bi-connector:
    image: yiluxiangbei/mongodb-bi-connector:v2.14.4
    container_name: mongodb-bi-connector
    restart: always
    ports:
      - 3307:3307
    environment:
      MONGODB_HOST: mongodb
      MONGODB_PORT: 27017
      MONGO_USERNAME: root
      MONGO_PASSWORD: 123456

```
