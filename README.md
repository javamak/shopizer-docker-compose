# This project is for reducing Shopizer build effort using docker-compose. The official repos of Shopizer are avaiable as submodules in this git repo. Clone this repo recursively and run the maven and docker-commands as below to get the project up and running

## Build Commands

cd shopizer && docker build -t shopizerecomm/shopizer .

cd shopizer-shop-reactjs && docker build -t shopizerecomm/shopizer-shop-reactjs .

cd shopizer-admin && docker build -t shopizerecomm/shopizer-admin .

## Run Commands to start each container seperately

docker run -d -p 8080:8080 shopizerecomm/shopizer:latest

docker run -d -e "APP_MERCHANT=DEFAULT" -e "APP_BASE_URL=http://localhost:8080" -p 9080:80 shopizerecomm/shopizer-shop-reactjs

docker run -e "APP_BASE_URL=http://localhost:8080/api" -p 82:80 shopizerecomm/shopizer-admin

## Compose Commands
cd shopizer && mvnw clean install 

Run below commands from the root directory (where docker-compose.yml is present)

docker-compose build

docker-compose up -d

docker-compose down -d

docker-compose exec -it shopizer-shop /bin/bash
