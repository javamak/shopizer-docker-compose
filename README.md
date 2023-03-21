# Docker commands to run Shopizer

## Build Commands

docker build -t shopizerecomm/shopizer .

docker build -t shopizerecomm/shopizer-shop-reactjs .

## Run Commands to start each container seperately

docker run -d -p 8080:8080 shopizerecomm/shopizer:latest

docker run -d -e "APP_MERCHANT=DEFAULT" -e "APP_BASE_URL=http://localhost:8080" -p 9080:80 shopizerecomm/shopizer-shop-reactjs
docker run -e "APP_BASE_URL=http://localhost:8080/api" -p 82:80 shopizerecomm/shopizer-admin

## Compose Commands

docker-compose up -d
docker-compose down -d
docker-compose exec -it shopizer-shop /bin/bash -- to validate
