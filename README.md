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