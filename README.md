# Nihon

Video streaming system: [Izanagi](https://github.com/hirooka/izanagi), [Izanami](https://github.com/hirooka/izanami) and [Tsukuyomi]((https://github.com/hirooka/tsukuyomi)) work together on Docker with Docker Compose.

## Prerequisites

- Linux PC (Ubuntu 20.04)
- NVIDIA GPU (GeForce 10 series) and its driver
- Docker 20.10.12
- Docker Compose 1.29.2

## Getting Started

You create working directory and build [Izanagi](https://github.com/hirooka/izanagi), [Izanami](https://github.com/hirooka/izanami), [Tsukuyomi](https://github.com/hirooka/tsukuyomi) Docker image.

```
mkdir ~/working directory
cd ~/working directory
# clone Izanagi and build on ~/working directory/izanagi
# clone Izanami and build ~/working directory/izanami
# clone Tsukuyomi and build ~/working directory/tsukuyomi
```

Then you can start system via

```
cd ~/working directory
git clone https://github.com/hirooka/nihon
cd nihon
docker-compose up
```

You can stop system via

```
docker-compose stop
```