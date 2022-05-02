# Procedure

## AMD64 + Ubuntu 22.04 (amd64)
```
mkdir ~/working_directory

cd ~/working_directory
git clone https://github.com/hirooka/izanagi
cd izanagi
cp ~/Dockerfile .
cp ~/tuner.json src/main/resources/
docker build . -t $USER/izanagi:1.0.0-SNAPSHOT

cd ~/working_directory
git clone https://github.com/hirooka/izanami
cd izanami
docker build . -t $USER/izanami:1.0.0-SNAPSHOT

cd ~/working_directory
git clone https://github.com/hirooka/tsukuyomi
cd tsukuyomi
docker build . -t $USER/tsukuyomi:1.0.0-SNAPSHOT

cd ~/working_directory
git clone https://github.com/hirooka/nihon
cd nihon
docker-compose up -d
```
## Raspberry Pi 4 + Ubuntu 20.04.2 (arm64)
```
mkdir ~/working_directory

cd ~/working_directory
git clone https://github.com/hirooka/izanagi
cd izanagi
cp ~/Dockerfile .
cp ~/tuner.json src/main/resources/
sed -i -e 's/java-11-openjdk-amd64/java-11-openjdk-arm64/g' Dockerfile
docker build . -t $USER/izanagi:1.0.0-SNAPSHOT

cd ~/working_directory
git clone https://github.com/hirooka/izanami
cd izanami
sed -i -e 's/hevc_nvenc/h264_v4l2m2m/g' src/main/resources/application.yml
sed -i -e 's/FROM nvidia\/cuda:11.4.1-devel-ubuntu20.04/FROM ubuntu:20.04/g' Dockerfile
sed -i -e 's/configure --enable-nonfree --enable-cuda-nvcc --enable-libnpp --extra-cflags=-I\/usr\/local\/cuda\/include --extra-ldflags=-L\/usr\/local\/cuda\/lib64 --nvccflags="-gencode arch=compute_52,code=sm_52 -O2"/configure/g' Dockerfile
sed -i -e 's/java-11-openjdk-amd64/java-11-openjdk-arm64/g' Dockerfile
docker build . -t $USER/izanami:1.0.0-SNAPSHOT

cd ~/working_directory
git clone https://github.com/hirooka/tsukuyomi
cd tsukuyomi
sed -i -e 's/#RUN apt-get update/RUN apt-get update/g' Dockerfile
docker build . -t $USER/tsukuyomi:1.0.0-SNAPSHOT

cd ~/working_directory
git clone https://github.com/hirooka/nihon
cd nihon
sed -i -e 's/image: mongo/image: mongo:bionic/g' docker-compose.yml
sed -i -e 's/deploy://g' docker-compose.yml
sed -i -e 's/resources://g' docker-compose.yml
sed -i -e 's/reservations://g' docker-compose.yml
sed -i -e 's/devices://g' docker-compose.yml
sed -i -e 's/- capabilities: [gpu]//g' docker-compose.yml
docker-compose up -d
```