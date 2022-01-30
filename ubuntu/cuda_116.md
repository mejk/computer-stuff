# CUDA 11.6 installation

Instractions for a quick installation. Don't use if you don't know what you're doing. Check the instructions, pre- and post-installation actions and info at 

- https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html
- https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/index.html
- https://developer.nvidia.com/cuda-downloads

## Get the CUDA toolkit 

From: https://developer.nvidia.com/cuda-downloads

Check the pre-requisistes and kernel compatibility from the NVIDIA pages before proceeding.

## On Ubuntu 20.04 LTS
```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin
sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/11.6.0/local_installers/cuda-repo-ubuntu2004-11-6-local_11.6.0-510.39.01-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2004-11-6-local_11.6.0-510.39.01-1_amd64.deb
sudo apt-key add /var/cuda-repo-ubuntu2004-11-6-local/7fa2af80.pub
sudo apt-get update
sudo apt-get -y install cuda
```
## On Ubuntu 18.04 LTS

```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-ubuntu1804.pin
sudo mv cuda-ubuntu1804.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/11.6.0/local_installers/cuda-repo-ubuntu1804-11-6-local_11.6.0-510.39.01-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1804-11-6-local_11.6.0-510.39.01-1_amd64.deb
sudo apt-key add /var/cuda-repo-ubuntu1804-11-6-local/7fa2af80.pub
sudo apt-get update
sudo apt-get -y install cuda
```

## This is not compulsory but if installed, it has to be done separately (=don't combine with the previous line). For both 20.04 LTS and 18.04 LTS

sudo apt-get install nvidia-gds 


## Make CUDA available 
```
export PATH=/usr/local/cuda-11.6/bin${PATH:+:${PATH}}
```

## Make CUDA permanently available
Path to CUDA has to be put in the `PATH` variable. Simply add the following in your `.profile`


```
PATH=/usr/local/cuda-11.6/bin${PATH:+:${PATH}}
```

## If things go wrong

See  https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#removing-cuda-tk-and-driver

### If you need to remove existing old CUDA tool kit. 

```
sudo apt-get --purge remove "*cuda*" "*cublas*" "*cufft*" "*cufile*" "*curand*" \
 "*cusolver*" "*cusparse*" "*gds-tools*" "*npp*" "*nvjpeg*" "nsight*"
```

### If you need to remove old nvidia drivers:

```
sudo apt-get --purge remove "*nvidia*"
```

### Cleanup
```
sudo apt-get autoremove
```
