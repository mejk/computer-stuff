# Installation of CUDA and Nvidia drivers & TensorFlow (Ubuntu 20.04 LTS)

<tt>Updated: Mon 27 Jul 14:12:46 </tt>

**Notes:** 
- The current CUDA version at the time of writing is CUDA 11.0
- See the links for more information. The instructions here are from [NVIDIA CUDA Installation Guide for Linux](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).
- The instructions are for Ubuntu 20.04, but the links (to NVIDIA) provide instructions for other Ubuntu versions and Linux Distros.
- It is assumed that gcc/g++/python3 have been installed (versions are also checked below).
- The procedure below has been tested on:
  - Alienware R8 with NVIDIA RTX2070 Super running Ubuntu Budgie 20.04 LTS. 

- If you have an existing NVIDIA graphics driver, this procedure will also updated it. 

--------------------------------------------

## Links for more information. The instructions below are based on these:

- [How to install CUDA on Ubuntu 20.04 Focal Fossa Linux](https://linuxconfig.org/how-to-install-cuda-on-ubuntu-20-04-focal-fossa-linux)
- From NVIDIA: [NVIDIA CUDA Installation Guide for Linux](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html)
   - IMPORTANT: This page has a very useful table showing compatible Linux versions, kernels and compiler dependencies. Check that you have a compatible version! 
  
## Pre-requisites
1. All of this should be ok since the Ubuntu 20.04 LTS default gcc compiler and python versions are high enough (9.3 and 3.8, respective; note that python version 2 is no longer installed as a default). Let's check them using the following commands (see compatibility table at the above):
  ```
  gcc --version
  python3 --version
  ```
2. Check that your Ubuntu version (64 bit) and kernel are on the above list (if not, then updating is needed):
  ```
   uname -a
   ```
3. In addition to having a compatible kernel, kernel headers are also needed. The following command installs them:
 
   ```
   sudo apt install linux-headers-$(uname -r)
   ```
   If the proper headers were already installed, then there is nothing to do. If installation was needed, reboot after installation.
   
4. Check that there is an NVidia GPU:
  ```
  lspci | grep -i nvidia
  ```
If the command doesn't return info regarding an Nvidia GPU and you know that there is one, see the instructions here: [Verify You Have a CUDA-Capable GPU](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#verify-you-have-cuda-enabled-system).


This completes the pre-requisites. 

## Download the CUDA toolkit
- For more, see: [Choose an Installation Method & ownload the NVIDIA CUDA Toolkit](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#choose-installation-method)

Here is the link for downloads (and there are different options).
```
https://developer.nvidia.com/cuda-downloads
```
Below is a shortcut using a local deb file. 

Important: If there is a pre-existing CUDA installation it may need to be removed depending on how it was installed. If there is a previous installation uthat used a deb package, then everything is ok.  
  - For more, see: [Handle Conflicting Installation Methods](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#handle-uninstallation):

The following shorcut works for Ubuntu 20.04 and CUDA version 11.0. Local dev file is downloaded (very large, >2G), and [checksum verification](http://developer.download.nvidia.com/compute/cuda/11.0.2/docs/sidebar/md5sum.txt) is done. 

Create a directory for download (not really necessary), but makes things easier:
```
cd
cd Downloads
mkdir CUDA
cd CUDA
```

```
wget http://developer.download.nvidia.com/compute/cuda/11.0.2/local_installers/cuda-repo-ubuntu2004-11-0-local_11.0.2-450.51.05-1_amd64.deb
```
Check the MD5 checksum to ensure that the file is ok. For this particular version: 74b09b0a04adad8c283862a1641eaf6c 
```
 md5sum cuda-repo-ubuntu2004-11-0-local_11.0.2-450.51.05-1_amd64.deb
```
If the number matches, continue:
```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin
sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600
sudo dpkg -i cuda-repo-ubuntu2004-11-0-local_11.0.2-450.51.05-1_amd64.deb
sudo apt-key add /var/cuda-repo-ubuntu2004-11-0-local/7fa2af80.pub
sudo apt-get update
sudo apt-get -y install cuda
```
### Include CUDA in the `PATH` environment variable 

The installation is now done, but we must add CUDA to the `PATH` environment variable (for mreo details, see: [Mandatory Actions](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#mandatory-post)):

```
export PATH=/usr/local/cuda-11.0/bin${PATH:+:${PATH}}
```
If you want to make this permanent, edit your `.profile` file and add the above at the bottom of it.


### Install NVIDIA Persistence Daemon:
```
/usr/bin/nvidia-persistenced --verbose
```

### Verify the installation:
```
cat /proc/driver/nvidia/version
```

Note: if Nvidia graphics drivers were previously installed, it is a good idea to reboot since the above procedure installed new drivers (here, the new ones are 450 and the old 440).

### Test the compiler

Finally, it is a good idea to test that the compiler works properly. For that, download the samples and compile them and run some basic tests (there are more samples in the directory):
```
cuda-install-samples-11.0.sh ~/Downloads/CUDA
cd ~/Downloads/CUDA/NVIDIA_CUDA-11.0_Samples
make 
./bin/x86_64/linux/release/deviceQuery
./bin/x86_64/linux/release/bandwidthTest
```
Both tests should pass.

### Optional (but a good idea): Third party libraries

Some of these may already be present, but let's be sure:
```
sudo apt install g++ freeglut3-dev build-essential libx11-dev libxmu-dev libxi-dev libglu1-mesa libglu1-mesa-dev
```

### Optional: Install the Nsight - the NVIDIA Visual Studio Edition

- See: [Nsight Eclipse Plugins Installation Guide](https://docs.nvidia.com/cuda/nsightee-plugins-install-guide/index.html)


## TensorFlow 2 with GPU support and Docker
- For more info, see: [TensorFlow Docker image with GPU support](https://www.tensorflow.org/install/docker). The instructions below originate from this link.
- TensorFlow Docker image with GPU support REQUIRES that NVIDIA GPU drivers have been installed succesfully.

TensorFlow 2 requires pip > 19.0. Check which version of pip (pip3) you have:
```
pip3 --version
```
If it is not installed, install it using
```
sudo apt install python3-pip
```
If you have a version that is not >19.0, upgrade pip
```
pip3 install --upgrade pip3
```

Install TensorFlow stable release with GPU support (the switch `--upgrade` takes care of dependencies).
```
pip3  install --upgrade tensorflow
```




1. [Install Docker](https://docs.docker.com/engine/install/)
  - If you have an older version of Docker installed, see: [Uninstall old version](https://docs.docker.com/engine/install/ubuntu/)

   - Let's get the packages, add the GPG kets and verify the fingerprint (at this time should be: `9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88` but check the  [Docker install page](https://docs.docker.com/engine/install/ubuntu/))

  ```
    sudo apt update
    sudo apt install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    sudo apt-key fingerprint 0EBFCD88
  ```
    
   - If the fingerprint matches, add the repository, install and verify:
     ```
      sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
      sudo apt update
      sudo apt install docker-ce docker-ce-cli containerd.io
      sudo docker run hello-world
      ```
      
   [Post-installation actions](https://docs.docker.com/engine/install/linux-postinstall/):
    - It is good to be able to run Docker as a non-root. For that, a new group called `docker` is created and users are added to it. Then the groups is activated and tested:
  ```
     sudo groupadd docker
     sudo usermod -aG docker $USER
     newgrp docker 
     docker run hello-world
  ```
  - If you want to start `docker` at boot time:
    ```
    sudo systemctl enable docker
    ```
    Disable:
    ```
    sudo systemctl disable docker
    ```
   - More options are listed on the [Docker postinstall page](https://docs.docker.com/engine/install/linux-postinstall/)
    
2. Install [NVIDIA Docker Container Toolkit](https://github.com/NVIDIA/nvidia-docker)
   - Here is a copy from the link. This should work if the CUDA was installed with the instructions above, otherwise & for more info see the link:
   ```
   distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
   curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
   curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
   sudo apt update && sudo apt install -y nvidia-container-toolkit
   sudo systemctl restart docker
   ```
  
2. Pull one of the images for TensorFlow. For more see, [https://www.tensorflow.org/install/docker](https://www.tensorflow.org/install/docker):
  ```
  docker pull tensorflow/tensorflow:latest-gpu-jupyter  # latest release w/ GPU support and Jupyter
  ```

3. Test:
```
docker run -it --rm tensorflow/tensorflow python -c "import tensorflow as tf; print(tf.reduce_sum(tf.random.normal([1000, 1000])))"

```

4. Check that the GPI version works:
  ```
  docker run --gpus all --rm nvidia/cuda nvidia-smi
  ```

## cuDNN
cuDNN is not required for the latest TensorFlow but may be required for other tasks. One must register at NVIDIA to be able to download. From downloads, select the cuDNN version matching the CUDA version installed. At this time, there is no version for Ubuntu 20.04






### CUDA installation guide from NVIDIA


```
lspci | grep -i nvidia
```
```
uname -m && cat /etc/*release
```
```
gcc --version
```
```
uname -r
```
```
sudo apt-get install linux-headers-$(uname -r)
```
