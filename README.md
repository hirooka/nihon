# Nihon

Video streaming system: [Izanagi](https://github.com/hirooka/izanagi), [Izanami](https://github.com/hirooka/izanami) and [Tsukuyomi]((https://github.com/hirooka/tsukuyomi)) work together on Docker with Docker Compose.

## Prerequisites

- Linux PC (Ubuntu 22.04)
- NVIDIA GPU (GeForce 10 series) and its driver (NVIDIA-SMI 510.60.02, Driver Version: 510.60.02, CUDA Version: 11.6)
- Docker 20.10.14
- Docker Compose v2.4.1

## Getting Started

You create working directory and build [Izanagi](https://github.com/hirooka/izanagi), [Izanami](https://github.com/hirooka/izanami), [Tsukuyomi](https://github.com/hirooka/tsukuyomi) Docker image.

```
mkdir ~/working_directory

# clone Izanagi and build on ~/working_directory/izanagi
cd ~/working_directory
git clone https://github.com/hirooka/izanagi
cd izanagi
cp ~/IdeaProjects/izanagi/Dockerfile .
cp ~/IdeaProjects/izanagi/src/main/resources/tuner.json src/main/resources/
docker build . -t $USER/izanagi:1.0.0-SNAPSHOT

# clone Izanami and build on ~/working_directory/izanami
cd ~/working_directory
git clone https://github.com/hirooka/izanami
cd izanami
docker build . -t $USER/izanami:1.0.0-SNAPSHOT

# clone Tsukuyomi and build on ~/working_directory/tsukuyomi
cd ~/working_directory
git clone https://github.com/hirooka/tsukuyomi
cd tsukuyomi
docker build . -t $USER/tsukuyomi:1.0.0-SNAPSHOT
```

Then you can start system via

```
cd ~/working_directory
git clone https://github.com/hirooka/nihon
cd nihon
docker compose up
```

You can clean system via

```
docker compose down
```