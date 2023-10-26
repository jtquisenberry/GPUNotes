# CUDA on Ubuntu 22.04 LTS Option 2

# Links

* https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=22.04&target_type=deb_local
* https://docs.nvidia.com/cuda/cuda-quick-start-guide/index.html
* https://docs.nvidia.com/cuda/demo-suite/index.html

# Install CUDA Toolkit

```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/12.3.0/local_installers/cuda-repo-ubuntu2204-12-3-local_12.3.0-545.23.06-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2204-12-3-local_12.3.0-545.23.06-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2204-12-3-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda-toolkit-12-3
```

# Install NVIDIA Drivers

```
sudo apt-get install -y nvidia-kernel-open-545
sudo apt-get install -y cuda-drivers-545
```

# Set Paths
## Current Session

```
$ export PATH=/usr/local/cuda-12.3/bin${PATH:+:${PATH}}
$ export LD_LIBRARY_PATH=/usr/local/cuda-12.3/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```

## Current User Permanently

```
$ nano ~/.bashrc
```

Paste these lines at the bottom of the file:
```
export PATH=/usr/local/cuda-12.3/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-12.3/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```
__Save__

__Reboot__
```
$ sudo reboot
```
__Check Paths__
```
$ echo $PATH
/usr/local/cuda-12.3/bin:...
$ echo $LD_LIBRARY_PATH
/usr/local/cuda-12.3/lib64
```

## All Users Permanently

Update `PATH` and `LD_LIBRARY_PATH` for all users permanently.

```
$ sudo nano /etc/environment
```
Edit the environment variables to include these lines:

```
PATH="<original value>:/usr/local/cuda-12.3/bin"
LD_LIBRARY_PATH="/usr/local/cuda-12.3/lib64"
```

__Example:__

```
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/usr/local/cuda-12.3/bin"
LD_LIBRARY_PATH="/usr/local/cuda-12.3/lib64"
```

__Save__

__Root__
```
$ sudo su
```

__Source__
```
# source /etc/environment
```

__Reboot__
```
# sudo reboot
```
__Check Paths__
```
$ echo $PATH
/usr/local/cuda-12.3/bin:...
$ echo $LD_LIBRARY_PATH
/usr/local/cuda-12.3/lib64
```

## With `sudo byobu`

Running `byobu` as root typically resets environment variables, including `$PATH`. Add the directory to what the path is reset to.

```
$ sudo visudo
```

Edit the file by updating this:
```
Defaults        secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"
```
to this
```
Defaults        secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin:/usr/local/cuda-12.3/bin"
```

__Save__

__Reboot__



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

```
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

# Check CUDA Functionality with NVIDIA Demos

As of CUDA 11.6, CUDA demos are available on GitHub only. https://docs.nvidia.com/cuda/cuda-samples/index.html

Repository: https://github.com/NVIDIA/cuda-samples/

## Download and Unzip Code

```
$ cd ~/Downloads
$ unzip cuda-samples-master.zip -d ../git
Archive:  cuda-samples-master.zip
b5c84e699635946cfd4cf53fae2933f98ca2a077
   creating: ../git/cuda-samples-master/
 extracting: ../git/cuda-samples-master/.gitignore  
  inflating: ../git/cuda-samples-master/CHANGELOG.md  
   creating: ../git/cuda-samples-master/Common/
...
```

## Build Demos from Source

```
$ cd ~/git/cuda-samples-master
$ make
make[1]: Entering directory '/home/jacobqadmin@consilio.com/git/cuda-samples-master/Samples/0_Introduction/UnifiedMemoryStreams'
/usr/local/cuda/bin/nvcc -ccbin g++ -I../../../Common -m64 -Xcompiler -fopenmp --threads 0 --std=c++11 -gencode
...
```

## Demo Directory

Enter the directory containing built demos.

```
$ ~/git/cuda-samples-master/bin/x86_64/linux/release
```

## Run Demos

```
$ ./eigenvalues 
Starting eigenvalues
GPU Device 0: "Ampere" with compute capability 8.0

Matrix size: 2048 x 2048
Precision: 0.000010
Iterations to be timed: 100
Result filename: 'eigenvalues.dat'
Gerschgorin interval: -2.894310 / 2.923303
Average time step 1: 1.275601 ms
Average time step 2, one intervals: 1.513480 ms
Average time step 2, mult intervals: 3.318349 ms
Average time TOTAL: 6.119980 ms
Test Succeeded!
```

```
$ ./bandwidthTest 
[CUDA Bandwidth Test] - Starting...
Running on...

 Device 0: NVIDIA A100-PCIE-40GB
 Quick Mode

 Host to Device Bandwidth, 1 Device(s)
 PINNED Memory Transfers
   Transfer Size (Bytes)	Bandwidth(GB/s)
   32000000			8.8

 Device to Host Bandwidth, 1 Device(s)
 PINNED Memory Transfers
   Transfer Size (Bytes)	Bandwidth(GB/s)
   32000000			8.7

 Device to Device Bandwidth, 1 Device(s)
 PINNED Memory Transfers
   Transfer Size (Bytes)	Bandwidth(GB/s)
   32000000			1162.6

Result = PASS

NOTE: The CUDA Samples are not meant for performance measurements. Results may vary when GPU Boost is enabled.
```

```
$ ./deviceQuery
./deviceQuery Starting...

 CUDA Device Query (Runtime API) version (CUDART static linking)

Detected 1 CUDA Capable device(s)

Device 0: "NVIDIA A100-PCIE-40GB"
  CUDA Driver Version / Runtime Version          12.3 / 12.3
  CUDA Capability Major/Minor version number:    8.0
  Total amount of global memory:                 40338 MBytes (42297786368 bytes)
  (108) Multiprocessors, (064) CUDA Cores/MP:    6912 CUDA Cores
  GPU Max Clock rate:                            1410 MHz (1.41 GHz)
  Memory Clock rate:                             1215 Mhz
  Memory Bus Width:                              5120-bit
  L2 Cache Size:                                 41943040 bytes
  Maximum Texture Dimension Size (x,y,z)         1D=(131072), 2D=(131072, 65536), 3D=(16384, 16384, 16384)
  Maximum Layered 1D Texture Size, (num) layers  1D=(32768), 2048 layers
  Maximum Layered 2D Texture Size, (num) layers  2D=(32768, 32768), 2048 layers
  Total amount of constant memory:               65536 bytes
  Total amount of shared memory per block:       49152 bytes
  Total shared memory per multiprocessor:        167936 bytes
  Total number of registers available per block: 65536
  Warp size:                                     32
  Maximum number of threads per multiprocessor:  2048
  Maximum number of threads per block:           1024
  Max dimension size of a thread block (x,y,z): (1024, 1024, 64)
  Max dimension size of a grid size    (x,y,z): (2147483647, 65535, 65535)
  Maximum memory pitch:                          2147483647 bytes
  Texture alignment:                             512 bytes
  Concurrent copy and kernel execution:          Yes with 3 copy engine(s)
  Run time limit on kernels:                     No
  Integrated GPU sharing Host Memory:            No
  Support host page-locked memory mapping:       Yes
  Alignment requirement for Surfaces:            Yes
  Device has ECC support:                        Disabled
  Device supports Unified Addressing (UVA):      Yes
  Device supports Managed Memory:                Yes
  Device supports Compute Preemption:            Yes
  Supports Cooperative Kernel Launch:            Yes
  Supports MultiDevice Co-op Kernel Launch:      Yes
  Device PCI Domain ID / Bus ID / location ID:   0 / 19 / 0
  Compute Mode:
     < Default (multiple host threads can use ::cudaSetDevice() with device simultaneously) >

deviceQuery, CUDA Driver = CUDART, CUDA Driver Version = 12.3, CUDA Runtime Version = 12.3, NumDevs = 1
Result = PASS
```

