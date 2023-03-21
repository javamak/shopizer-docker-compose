# This project is for reducing Shopizer build effort using docker-compose. The official repos of Shopizer are avaiable as submodules in this git repo. Clone this repo recursively and run the maven and docker-commands as below to get the project up and running

## Open Issues

admin project is not working due to issues in the dockerfile present in the official repo.

## First, need some changes to the shopizer project as below

1. Open `shopizer\sm-core\src\main\resources\profiles\mysql\shopizer-core.properties` and uncomment below two lines

    ```
    config.cms.aws.bucket=
    config.cms.aws.region=
    ```

2. Comment below 3 lines in `shopizer\sm-shop\src\main\resources\profiles\mysql`

    ```
    db.jdbcUrl=jdbc:mysql://localhost:3306/SALESMANAGER?autoReconnect=true&serverTimeZone=UTC&useUnicode=true&characterEncoding=UTF-8
    db.user=shopizer_db_user
    db.password=shopizer_db_password
    ```

## Compose Commands

### Build the core project using Maven

`cd shopizer && mvnw clean install`

Run below commands from the root directory (where docker-compose.yml is present)

### To build all the Docker images

`docker-compose build`

### Start/stop the containers

`docker-compose up -d`

`docker-compose down -d`

### Command to bash into a running container

`docker-compose exec -it shopizer-shop /bin/bash`

## Commands to build the Docker images seperately

`cd shopizer && docker build -t shopizerecomm/shopizer .`

`cd shopizer-shop-reactjs && docker build -t shopizerecomm/shopizer-shop-reactjs .`

`cd shopizer-admin && docker build -t shopizerecomm/shopizer-admin .`

## Run Commands to start each container seperately

`docker run -d -p 8080:8080 shopizerecomm/shopizer:latest`

`docker run -d -e "APP_MERCHANT=DEFAULT" -e "APP_BASE_URL=<http://localhost:8080>" -p 9080:80 shopizerecomm/shopizer-shop-reactjs`

`docker run -e "APP_BASE_URL=<http://localhost:8080/api>" -p 82:80 shopizerecomm/shopizer-admin`
