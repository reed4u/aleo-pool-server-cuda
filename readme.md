# Aleo Mining Pool Server

## Introduction

A mining pool server for the Aleo network.

# Aleo Install

## 1. Prerequisites

### 1.1 build & package tool
```
$sudo su
$apt update
$apt install build-essential
$apt-get install pkg-config libssl-dev
```
- gcc-10 버전
```
$MAX_GCC_VERSION= 10
$sudo apt install gcc-$MAX_GCC_VERSION g++-$MAX_GCC_VERSION
$sudo ln -s /usr/bin/gcc-$MAX_GCC_VERSION /usr/local/cuda/bin/gcc 
$sudo ln -s /usr/bin/g++-$MAX_GCC_VERSION /usr/local/cuda/bin/g++
$sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-10 10 --slave /usr/bin/g++ g++ /usr/bin/g++-10
$sudo update-alternatives --config gcc
```

- NVIDIA CUDA 설치
```
$sudo apt update
$sudo apt install nvidia-driver-430
$sudo reboot 
$wget https://developer.download.nvidia.com/compute/cuda/11.2.2/local_installers/cuda_11.2.2_460.32.03_linux.run
$sudo sh cuda_11.2.2_460.32.03_linux.run
```
- bashrc에 다음과 같이 추가
```
export PATH=/usr/local/cuda-11.2/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```
- gcc 링크
```
$sudo ln -s /usr/bin/gcc-10 /usr/local/cuda/bin/gcc
$sudo ln -s /usr/bin/g++-10 /usr/local/cuda/bin/g++
```
### 1.2 Rust 설치
```
$curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
$source "$HOME/.cargo/env"
```
### 1.3 Go 설치
```
$wget -c https://golang.org/dl/go1.18.1.linux-amd64.tar.gz -O - | sudo tar -xz -C /usr/local
$echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc && source ~/.bashrc
```

## 2. Aleo-pool-server-cuda 설치
### install
```
$git clone https://github.com/reed4u/aleo-pool-server-cuda.git
$cd aleo-pool-cuda
$cargo update
$cargo build
```
- 데이터베이스 기능을 끌 수 있음 | gpu 사용
```
$cargo build --release --no-default-features
```
### Usage
```
$cargo run -- --address <ADDRESS> --port <PORT> --api-port <API PORT>
```
or
```
$target/release/snarkos --operator aleo1cev9umxxxxxxx......xxxx --trial
```

### System requirements

- Rust 1.59+ (Not sure what's strictly required)

Optional:

- PostgreSQL 11+ (Still not sure what's strictly required)
- PL/Python 3.6+

## License

AGPL-3.0-or-later
