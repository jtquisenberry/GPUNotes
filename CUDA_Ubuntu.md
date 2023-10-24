# CUDA in Ubuntu 22.04 LTS

# Check GPU

```
$ sudo lshw -class display
  *-display                 
       description: VGA compatible controller
       product: SVGA II Adapter
       vendor: VMware
       physical id: f
       bus info: pci@0000:00:0f.0
       logical name: /dev/fb0
       version: 00
       width: 32 bits
       clock: 33MHz
       capabilities: vga_controller bus_master cap_list rom fb
       configuration: depth=32 driver=vmwgfx latency=64 resolution=1176,885
       resources: irq:16 ioport:2040(size=16) memory:e8000000-efffffff memory:f9000000-f97fffff memory:c0000-dffff
  *-display UNCLAIMED
       description: 3D controller
       product: GA100 [A100 PCIe 40GB]
       vendor: NVIDIA Corporation
       physical id: 0
       bus info: pci@0000:13:00.0
       version: a1
       width: 64 bits
       clock: 33MHz
       capabilities: pm cap_list
       configuration: latency=64
       resources: iomemory:1fe00-1fdff iomemory:1ff00-1feff memory:fb000000-fbffffff memory:1fe000000000-1fefffffffff memory:1ff000000000-1ff001ffffff
```

# Check Communication with Nvidia Driver

## Error: Driver Mismatch

This error may indicate that components of two different versions are installed.
```
$ nvidia-smi
Failed to initialize NVML: Driver/library version mismatch
```

## Error: Driver Not Installed

```
$ nvidia-smi
NVIDIA-SMI has failed because it couldn't communicate with the NVIDIA driver. Make sure that the latest NVIDIA driver is installed and running.
```

## Solution

The solution to both issues is to install the correct Nvidia driver.

# Remove Nvidia Packages



# List Available Nvidia Drivers

```
$ sudo ubuntu-drivers devices
ERROR:root:aplay command not found
== /sys/devices/pci0000:00/0000:00:17.0/0000:13:00.0 ==
modalias : pci:v000010DEd000020F1sv000010DEsd0000145Fbc03sc02i00
vendor   : NVIDIA Corporation
model    : GA100 [A100 PCIe 40GB]
driver   : nvidia-driver-535-server - distro non-free
driver   : nvidia-driver-450-server - distro non-free
driver   : nvidia-driver-470 - distro non-free recommended
driver   : nvidia-driver-525-open - distro non-free
driver   : nvidia-driver-525-server - distro non-free
driver   : nvidia-driver-535-server-open - distro non-free
driver   : nvidia-driver-535-open - distro non-free
driver   : nvidia-driver-470-server - distro non-free
driver   : xserver-xorg-video-nouveau - distro free builtin

== /sys/devices/pci0000:00/0000:00:0f.0 ==
modalias : pci:v000015ADd00000405sv000015ADsd00000405bc03sc00i00
vendor   : VMware
model    : SVGA II Adapter
driver   : open-vm-tools-desktop - distro free

```

# Install a Driver

To use the latest version of CUDA, it may be necessary to install the latest Nvidia driver. The highest-version driver in the above list is `nvidia-driver-535`.


```
$ sudo apt install nvidia-driver-525
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  dctrl-tools dkms libnvidia-cfg1-525 libnvidia-common-525 libnvidia-compute-525 libnvidia-decode-525 libnvidia-encode-525 libnvidia-extra-525 libnvidia-fbc1-525 libnvidia-gl-525 libvdpau1 libxnvctrl0
  mesa-vdpau-drivers nvidia-compute-utils-525 nvidia-dkms-525 nvidia-kernel-common-525 nvidia-kernel-source-525 nvidia-prime nvidia-settings nvidia-utils-525 pkg-config screen-resolution-extra vdpau-driver-all
  xserver-xorg-video-nvidia-525
Suggested packages:
  debtags menu libvdpau-va-gl1
Recommended packages:
  libnvidia-compute-525:i386 libnvidia-decode-525:i386 libnvidia-encode-525:i386 libnvidia-fbc1-525:i386 libnvidia-gl-525:i386
The following packages will be REMOVED:
  libnvidia-compute-535
The following NEW packages will be installed:
  dctrl-tools dkms libnvidia-cfg1-525 libnvidia-common-525 libnvidia-compute-525 libnvidia-decode-525 libnvidia-encode-525 libnvidia-extra-525 libnvidia-fbc1-525 libnvidia-gl-525 libvdpau1 libxnvctrl0
  mesa-vdpau-drivers nvidia-compute-utils-525 nvidia-dkms-525 nvidia-driver-525 nvidia-kernel-common-525 nvidia-kernel-source-525 nvidia-prime nvidia-settings nvidia-utils-525 pkg-config
  screen-resolution-extra vdpau-driver-all xserver-xorg-video-nvidia-525
0 upgraded, 25 newly installed, 1 to remove and 0 not upgraded.
Need to get 329 MB/330 MB of archives.
After this operation, 677 MB of additional disk space will be used.
Do you want to continue? [Y/n] y



```







## To Install a Specific Driver

```
$ sudo apt install nvidia-driver-535
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following NEW packages will be installed:
  libnvidia-cfg1-535 libnvidia-common-535 libnvidia-compute-535 libnvidia-decode-535 libnvidia-encode-535 libnvidia-extra-535 libnvidia-fbc1-535 libnvidia-gl-535 nvidia-compute-utils-535 nvidia-dkms-535
  nvidia-driver-535 nvidia-kernel-common-535 nvidia-kernel-source-535 nvidia-utils-535 xserver-xorg-video-nvidia-535
0 upgraded, 15 newly installed, 17 to remove and 0 not upgraded.
Need to get 307 MB of archives.
After this operation, 203 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
```

```
$sudo reboot
```

## To Install the Recommended Driver

Installing the recommended driver may preclude the use of the latest version of CUDA.

```
$ sudo ubuntu-drivers autoinstall
```

```
$sudo reboot
```

# Check Communication with Nvidia Driver

This utility reports driver version 525.* and CUDA version 12.0. It reports the correct GPU model and that 40 GB of GPU memory are found.

```
$ nvidia-smi
Tue Oct 24 22:36:59 2023       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 525.125.06   Driver Version: 525.125.06   CUDA Version: 12.0     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA A100-PCI...  On   | 00000000:13:00.0 Off |                  Off |
| N/A   34C    P0    34W / 250W |      0MiB / 40960MiB |      0%      Default |
|                               |                      |             Disabled |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+


```

# Check for Installed CUDA Toolkit

Check whether CUDA Toolkit is already installed. In this example, CUDA Toolkit is not already installed.

```
$ which nvcc

$ nvcc --version
Command 'nvcc' not found, but can be installed with:
apt install nvidia-cuda-toolkit
Please ask your administrator.

```

# Install CUDA Toolkit

```
sudo apt update && sudo apt upgrade
```

```
$ sudo apt install nvidia-cuda-toolkit
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  ca-certificates-java fonts-dejavu-extra java-common javascript-common libaccinj64-11.5 libatk-wrapper-java libatk-wrapper-java-jni libbabeltrace1 libboost-regex1.74.0 libcub-dev libcublas11 libcublaslt11
  libcudart11.0 libcufft10 libcufftw10 libcuinj64-11.5 libcupti-dev libcupti-doc libcupti11.5 libcurand10 libcusolver11 libcusolvermg11 libcusparse11 libdebuginfod-common libdebuginfod1 libegl-dev
  libgail-common libgail18 libgif7 libgl-dev libgl1-mesa-dev libgles-dev libgles1 libglvnd-core-dev libglvnd-dev libglx-dev libgtk2.0-0 libgtk2.0-bin libgtk2.0-common libipt2 libjs-jquery libnppc11 libnppial11
  libnppicc11 libnppidei11 libnppif11 libnppig11 libnppim11 libnppist11 libnppisu11 libnppitc11 libnpps11 libnvblas11 libnvidia-compute-495 libnvidia-compute-510 libnvidia-ml-dev libnvjpeg11
  libnvrtc-builtins11.5 libnvrtc11.2 libnvtoolsext1 libnvvm4 libopengl-dev libpcsclite1 libpthread-stubs0-dev libsource-highlight-common libsource-highlight4v5 libtbb-dev libtbb12 libtbbmalloc2 libthrust-dev
  libvdpau-dev libx11-dev libxau-dev libxcb1-dev libxdmcp-dev node-html5shiv nvidia-cuda-dev nvidia-cuda-gdb nvidia-cuda-toolkit-doc nvidia-opencl-dev nvidia-profiler nvidia-visual-profiler ocl-icd-libopencl1
  ocl-icd-opencl-dev opencl-c-headers opencl-clhpp-headers openjdk-8-jre openjdk-8-jre-headless x11proto-dev xorg-sgml-doctools xtrans-dev
Suggested packages:
  default-jre apache2 | lighttpd | httpd pcscd libtbb-doc libvdpau-doc libx11-doc libxcb-doc nodejs opencl-clhpp-headers-doc fonts-nanum fonts-ipafont-gothic fonts-ipafont-mincho fonts-wqy-microhei
  fonts-wqy-zenhei fonts-indic
Recommended packages:
  libnvcuvid1 nsight-compute nsight-systems
The following NEW packages will be installed:
  ca-certificates-java fonts-dejavu-extra java-common javascript-common libaccinj64-11.5 libatk-wrapper-java libatk-wrapper-java-jni libbabeltrace1 libboost-regex1.74.0 libcub-dev libcublas11 libcublaslt11
  libcudart11.0 libcufft10 libcufftw10 libcuinj64-11.5 libcupti-dev libcupti-doc libcupti11.5 libcurand10 libcusolver11 libcusolvermg11 libcusparse11 libdebuginfod-common libdebuginfod1 libegl-dev
  libgail-common libgail18 libgif7 libgl-dev libgl1-mesa-dev libgles-dev libgles1 libglvnd-core-dev libglvnd-dev libglx-dev libgtk2.0-0 libgtk2.0-bin libgtk2.0-common libipt2 libjs-jquery libnppc11 libnppial11
  libnppicc11 libnppidei11 libnppif11 libnppig11 libnppim11 libnppist11 libnppisu11 libnppitc11 libnpps11 libnvblas11 libnvidia-compute-495 libnvidia-compute-510 libnvidia-ml-dev libnvjpeg11
  libnvrtc-builtins11.5 libnvrtc11.2 libnvtoolsext1 libnvvm4 libopengl-dev libpcsclite1 libpthread-stubs0-dev libsource-highlight-common libsource-highlight4v5 libtbb-dev libtbb12 libtbbmalloc2 libthrust-dev
  libvdpau-dev libx11-dev libxau-dev libxcb1-dev libxdmcp-dev node-html5shiv nvidia-cuda-dev nvidia-cuda-gdb nvidia-cuda-toolkit nvidia-cuda-toolkit-doc nvidia-opencl-dev nvidia-profiler nvidia-visual-profiler
  ocl-icd-libopencl1 ocl-icd-opencl-dev opencl-c-headers opencl-clhpp-headers openjdk-8-jre openjdk-8-jre-headless x11proto-dev xorg-sgml-doctools xtrans-dev
0 upgraded, 92 newly installed, 0 to remove and 0 not upgraded.
Need to get 1,505 MB of archives.
After this operation, 4,066 MB of additional disk space will be used.
Do you want to continue? [Y/n] y


```

# Detect CUDA Version

```
$ nvcc --version
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2021 NVIDIA Corporation
Built on Thu_Nov_18_09:45:30_PST_2021
Cuda compilation tools, release 11.5, V11.5.119
Build cuda_11.5.r11.5/compiler.30672275_0
```

```
$ which nvcc
/usr/bin/nvcc
```



# Links

https://varhowto.com/check-cuda-version/



