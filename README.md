# Installation
## Install Linux Mint 20.04

### Update Kernal to 5.11
Need latest kernel for NVIDIA Driver Support

## Install NVIDIA Drivers

## Install Docker-CE
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(. /etc/os-release; echo "$UBUNTU_CODENAME") stable"
sudo apt-get update
sudo apt-get -y install docker-ce
sudo usermod -aG docker $USER
newgrp docker

docker --version
docker run --name docker-nginx -p 80:80 nginx

## Install NVIDIA Container Manager
https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#docker
### Add Repository
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add - \
   && curl -s -L https://nvidia.github.io/nvidia-docker/$ubuntu20.04/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
curl -s -L https://nvidia.github.io/nvidia-container-runtime/experimental/$distribution/nvidia-container-runtime.list | sudo tee /etc/apt/sources.list.d/nvidia-container-runtime.list
sudo apt-get update
sudo apt-get install -y nvidia-docker2
sudo systemctl restart docker
sudo docker run --rm --gpus all nvidia/cuda:11.0-base nvidia-smi

# Running ML

# Start Docker
## Docker Image(https://ngc.nvidia.com/catalog/containers/nvidia:tensorflow)
docker run -p 8888:8888 --gpus all -it -v ~/Docker/:/workspace nvcr.io/nvidia/tensorflow:21.07-tf1-py3

## Run jupyter notebook
jupyter notebook --port=8888 --ip=0.0.0.0 --allow-root --no-browser .
