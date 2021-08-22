## Prerequisites
- Docker Engine 20.10.7
- Docker Compose 1.29.2

## Networking
```
docker network create nihon
```
## Izanagi
### PostgreSQL
```
docker pull postgres

docker run \
  --name izanagi-postgres \
  --net nihon \
  -e POSTGRES_USER=izanagi \
  -e POSTGRES_DB=izanagidb \
  -e POSTGRES_HOST_AUTH_METHOD=trust \
  -p 5432:5432 \
  -d \
  postgres

docker run \
  --name izanagi-postgres \
  --net nihon \
  -e POSTGRES_USER=izanagi \
  -e POSTGRES_DB=izanagidb \
  -e POSTGRES_HOST_AUTH_METHOD=trust \
  -p 5432:5432 \
  --mount type=volume,source=izanagi-postgres-data,target=/var/lib/postgresql/data \
  -d \
  postgres

docker ps
docker logs -f izanagi-postgres
```
### Izanagi
```
cd ~/working_directory
git clone https://github.com/hirooka/izanagi
cp ~/Dockerfile ~/working_directory/izanagi/
cp ~/tuner.json ~/working_directory/izanagi/src/main/resources/
cd izanagi
docker build . -t $USER/izanagi:1.0.0-SNAPSHOT

docker run \
    --name izanagi \
    --net nihon \
    --privileged \
    --mount type=bind,source=/dev/,target=/dev/ \
    --mount type=bind,source=/var/run/pcscd/pcscd.comm,target=/var/run/pcscd/pcscd.comm \
    --mount type=bind,source=/etc/localtime,target=/etc/localtime:ro \
    -p 8081:8081 \
    -d \
    -it $USER/izanagi:1.0.0-SNAPSHOT

docker run \
    --name izanagi \
    --net nihon \
    --privileged \
    --mount type=bind,source=/dev/,target=/dev/ \
    --mount type=bind,source=/var/run/pcscd/pcscd.comm,target=/var/run/pcscd/pcscd.comm \
    --mount type=bind,source=/etc/localtime,target=/etc/localtime:ro \
    -p 8081:8081 \
    -it $USER/izanagi:1.0.0-SNAPSHOT \
    /bin/bash

docker ps
docker logs -f izanagi

docker exec -it izanagi /bin/bash
```
## Izanami
### MongoDB
```
docker pull mongo

docker run \
  --name izanami-mongo \
  --net nihon \
  -d \
  mongo

docker run \
  --name izanami-mongo \
  --net nihon \
  --mount type=volume,source=izanami-mongo-data,target=/data/db \
  -d \
  mongo

```
### Izanami
```
cd ~/working_directory
git clone https://github.com/hirooka/izanami
cd izanami
docker build . -t $USER/izanami:1.0.0-SNAPSHOT

docker run \
  --name izanami \
  --net nihon \
  --gpus all \
  --privileged \
  --mount type=bind,source=/dev/,target=/dev/ \
  --mount type=bind,source=/opt/izanami/video,target=/opt/izanami/video \
  --mount type=bind,source=/etc/localtime,target=/etc/localtime:ro \
  -p 8080:8080 \
  -d \
  -it $USER/izanami:1.0.0-SNAPSHOT

docker run \
  --name izanami \
  --net nihon \
  --gpus all \
  --privileged \
  --mount type=bind,source=/dev/,target=/dev/ \
  --mount type=bind,source=/opt/izanami/video,target=/opt/izanami/video \
  --mount type=bind,source=/etc/localtime,target=/etc/localtime:ro \
  -p 8080:8080 \
  -it $USER/izanami:1.0.0-SNAPSHOT \
  /bin/bash

docker ps
docker logs -f izanami

docker exec -it izanami /bin/bash
```
## Tsukuyomi
```
cd ~/working_directory
git clone https://github.com/hirooka/tsukuyomi
cd tsukuyomi
docker build . -t $USER/tsukuyomi:1.0.0-SNAPSHOT

docker run \
  --name tsukuyomi \
  --net nihon \
  --privileged \
  --mount type=bind,source=/etc/localtime,target=/etc/localtime:ro \
  -p 80:3000 \
  -d \
  -it $USER/tsukuyomi:1.0.0-SNAPSHOT

docker ps
docker logs -f tsukuyomi

docker exec -it tsukuyomi /bin/bash
```
## Memo
```
docker ps
docker ps -a
docker rm `docker ps -a -q`

docker network prune
docker volume prune
docker image prune

docker rmi -f `docker images -aq`
```
