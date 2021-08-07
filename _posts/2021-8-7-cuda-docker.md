# CUDA & Docker

-- How to make CUDA work inside Docker



## CUDA Versions

`nvidia-smi` shows the currently installed driver version and a "CUDA version". That CUDA version is *not* the currently installed version of CUDA; instead it is the maximum version of CUDA supported by this particular driver.

The actual CUDA library is installed seperately, usually from the package `cuda-toolkit`. There can be multiple copies of `cuda-toolkit`(e.g. one per conda environment). If the package takes up too much space, consider using a "base" image, such as `nvidia/cuda:10.1-base-ubuntu18.04`. 



## Expose GPU to a container

1. Install `nvidia-container-toolkit`.

```bash
# Add the package repositories
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list

sudo apt-get update && sudo apt-get install -y nvidia-container-toolkit
sudo systemctl restart docker
```

2. Run containers with `--gpus all` or `--gpus device=0,1,2,3`.

Reference: [Stack overflow answer](https://stackoverflow.com/a/58432877).

