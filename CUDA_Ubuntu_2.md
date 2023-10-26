# CUDA on Ubuntu 22.04 LTS Option 2

# Link

* https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=22.04&target_type=deb_local
* https://docs.nvidia.com/cuda/cuda-quick-start-guide/index.html

# CUDA Toolkit

```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/12.3.0/local_installers/cuda-repo-ubuntu2204-12-3-local_12.3.0-545.23.06-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2204-12-3-local_12.3.0-545.23.06-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2204-12-3-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda-toolkit-12-3
```

# NVIDIA Drivers

```
sudo apt-get install -y nvidia-kernel-open-545
sudo apt-get install -y cuda-drivers-545
```

# Set Paths
## Current Session

```
$ export PATH=/usr/local/cuda-12.3/bin${PATH:+:${PATH}}
$ export LD_LIBRARY_PATH=/usr/local/cuda-12.3/lib64\
                         ${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```

## Current User Permanently

```
$ nano ~/.bashrc
```

Paste these lines at the bottom of the file:
```
export PATH=/usr/local/cuda-12.3/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-12.3/lib64${LD_LIBRARY_PATH:+:${LD_LIBRA>
```
Save

Reboot
```
sudo reboot
```
Check Paths
```
$ echo $PATH
/usr/local/cuda-12.3/bin:...
$ echo $LD_LIBRARY_PATH
/usr/local/cuda-12.3/lib64
```

## All Users Permanently

See https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux-unix

```
$ sudo nano /etc/environment
```
Edit the environment variables to include these lines:

```
PATH="<original value>:/usr/local/cuda-12.3/bin"
LD_LIBRARY_PATH="/usr/local/cuda-12.3/lib64"


```
Example:

```
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/usr/local/cuda-12.3/bin"
LD_LIBRARY_PATH="/usr/local/cuda-12.3/lib64"
```

Save

Source
```
# source /etc/environment
```

Reboot
```
sudo reboot
```
Check Paths
```
$ echo $PATH
/usr/local/cuda-12.3/bin:...
$ echo $LD_LIBRARY_PATH
/usr/local/cuda-12.3/lib64
```


# Check CUDA Toolkit

```
$ nvcc --version
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2023 NVIDIA Corporation
Built on Fri_Sep__8_19:17:24_PDT_2023
Cuda compilation tools, release 12.3, V12.3.52
Build cuda_12.3.r12.3/compiler.33281558_0
```

# Check NVIDIA Driver Version

$ nvidia-smi
Tue Oct 24 23:11:53 2023       
+---------------------------------------------------------------------------------------+
| NVIDIA-SMI 545.23.06              Driver Version: 545.23.06    CUDA Version: 12.3     |
|-----------------------------------------+----------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |         Memory-Usage | GPU-Util  Compute M. |
|                                         |                      |               MIG M. |
|=========================================+======================+======================|
|   0  NVIDIA A100-PCIE-40GB          On  | 00000000:13:00.0 Off |                  Off |
| N/A   34C    P0              34W / 250W |      4MiB / 40960MiB |      0%      Default |
|                                         |                      |             Disabled |
+-----------------------------------------+----------------------+----------------------+
                                                                                         
+---------------------------------------------------------------------------------------+
| Processes:                                                                            |
|  GPU   GI   CI        PID   Type   Process name                            GPU Memory |
|        ID   ID                                                             Usage      |
|=======================================================================================|
|  No running processes found                                                           |
+---------------------------------------------------------------------------------------+

```



