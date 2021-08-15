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
```
### Izanagi
```
docker build . -t $USER/izanagi:1.0.0-SNAPSHOT

docker run \
    --name izanagi \
    --net nihon \
    --privileged \
    --volume /dev/:/dev/ \
    --volume /var/run/pcscd/pcscd.comm:/var/run/pcscd/pcscd.comm \
    --volume /etc/localtime:/etc/localtime:ro \
    -p 8081:8081 \
    -d \
    -it $USER/izanagi:1.0.0-SNAPSHOT

docker run \
    --name izanagi \
    --net nihon \
    --privileged \
    --volume /dev/:/dev/ \
    --volume /var/run/pcscd/pcscd.comm:/var/run/pcscd/pcscd.comm \
    --volume /etc/localtime:/etc/localtime:ro \
    -p 8081:8081 \
    -it $USER/izanagi:1.0.0-SNAPSHOT \
    /bin/bash

docker logs izanagi

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
```
### Izanami
```
docker build . -t $USER/izanami:1.0.0-SNAPSHOT

docker run \
  --name izanami \
  --net nihon \
  --gpus all \
  --privileged \
  --volume /dev/:/dev/ \
  --volume /opt/izanami/video:/opt/izanami/video \
  --volume /etc/localtime:/etc/localtime:ro \
  -p 8080:8080 \
  -d \
  -it $USER/izanami:1.0.0-SNAPSHOT

docker run \
  --name izanami \
  --net nihon \
  --gpus all \
  --privileged \
  --volume /dev/:/dev/ \
  --volume /opt/izanami/video:/opt/izanami/video \
  --volume /etc/localtime:/etc/localtime:ro \
  -p 8080:8080 \
  -it $USER/izanami:1.0.0-SNAPSHOT \
  /bin/bash

docker logs izanami

docker exec -it izanami /bin/bash
```
## Tsukuyomi
```
docker build . -t $USER/tsukuyomi:1.0.0-SNAPSHOT

docker run \
  --name tsukuyomi \
  --net nihon \
  --privileged \
  --volume /etc/localtime:/etc/localtime:ro \
  -p 80:3000 \
  -d \
  -it $USER/tsukuyomi:1.0.0-SNAPSHOT

docker logs tsukuyomi

docker exec -it tsukuyomi /bin/bash
```
## Memo
```
docker ps
docker ps -a
docker rm `docker ps -a -q`
```
