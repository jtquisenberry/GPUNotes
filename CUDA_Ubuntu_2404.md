# CUDA in Ubuntu 24.04 LTS

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
       configuration: depth=32 driver=vmwgfx latency=64 resolution=1280,800
       resources: irq:16 ioport:2040(size=16) memory:e8000000-efffffff memory:fb800000-fbffffff memory:c0000-dffff
  *-display
       description: VGA compatible controller
       product: GP104GL [Tesla P6]
       vendor: NVIDIA Corporation
       physical id: 1
       bus info: pci@0000:02:01.0
       version: a1
       width: 64 bits
       clock: 66MHz
       capabilities: msi vga_controller bus_master cap_list
       configuration: driver=nvidia latency=0
       resources: irq:-22 memory:fa000000-faffffff memory:d0000000-dfffffff memory:f8000000-f9ffffff

```

# Check Communication with Nvidia Driver

```
$ nvidia-smi
```

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

The solution to both errors is to install the correct NVIDIA driver.

# Install NVIDIA Drivers

## Remove Nvidia Packages

```
sudo apt autoremove nvidia* --purge
```

## List Available Nvidia Drivers

```
$ sudo ubuntu-drivers devices
== /sys/devices/pci0000:00/0000:00:0f.0 ==
modalias : pci:v000015ADd00000405sv000015ADsd00000405bc03sc00i00
vendor   : VMware
model    : SVGA II Adapter
manual_install: True
driver   : open-vm-tools-desktop - distro free

== /sys/devices/pci0000:00/0000:00:11.0/0000:02:01.0 ==
modalias : pci:v000010DEd00001BB4sv000010DEsd000011FDbc03sc00i00
vendor   : NVIDIA Corporation
model    : GP104GL [Tesla P6]
manual_install: True
driver   : nvidia-driver-535-server - distro non-free
driver   : nvidia-driver-555 - third-party non-free
driver   : nvidia-driver-560 - third-party non-free recommended
driver   : nvidia-driver-470-server - distro non-free
driver   : nvidia-driver-535 - distro non-free
driver   : nvidia-driver-550 - third-party non-free
driver   : nvidia-driver-390 - third-party non-free
driver   : nvidia-driver-545 - third-party non-free
driver   : nvidia-driver-470 - distro non-free
driver   : xserver-xorg-video-nouveau - distro free builtin
```

## Another Way to List Drivers

```
~$ apt list nvidia-driver*
Listing... Done
nvidia-driver-390/noble 390.157-0ubuntu7 amd64
nvidia-driver-460-server/noble-updates,noble-security 470.256.02-0ubuntu0.24.04.1 amd64
nvidia-driver-460/noble-updates,noble-security 470.256.02-0ubuntu0.24.04.1 amd64
nvidia-driver-465/noble-updates,noble-security 470.256.02-0ubuntu0.24.04.1 amd64
nvidia-driver-470-server/noble-updates,noble-security 470.256.02-0ubuntu0.24.04.1 amd64
nvidia-driver-470/noble-updates,noble-security 470.256.02-0ubuntu0.24.04.1 amd64
nvidia-driver-510/noble 525.147.05-0ubuntu2 amd64
nvidia-driver-515-open/noble 525.147.05-0ubuntu2 amd64
nvidia-driver-515-server/noble 525.147.05-0ubuntu2 amd64
nvidia-driver-515/noble 525.147.05-0ubuntu2 amd64
nvidia-driver-520-open/noble 525.147.05-0ubuntu2 amd64
nvidia-driver-520/noble 525.147.05-0ubuntu2 amd64
nvidia-driver-525-open/noble 525.147.05-0ubuntu2 amd64
nvidia-driver-525-server/noble 525.147.05-0ubuntu2 amd64
nvidia-driver-525/noble 525.147.05-0ubuntu2 amd64
nvidia-driver-530-open/noble-updates,noble-security 535.183.01-0ubuntu0.24.04.1 amd64
nvidia-driver-530/noble-updates,noble-security 535.183.01-0ubuntu0.24.04.1 amd64
nvidia-driver-535-open/noble-updates,noble-security 535.183.01-0ubuntu0.24.04.1 amd64
nvidia-driver-535-server-open/noble-updates,noble-security 535.216.01-0ubuntu0.24.04.1 amd64
nvidia-driver-535-server/noble-updates,noble-security 535.216.01-0ubuntu0.24.04.1 amd64
nvidia-driver-535/noble-updates,noble-security 535.183.01-0ubuntu0.24.04.1 amd64
nvidia-driver-545-open/noble 545.29.06-0ubuntu0~gpu24.04.1 amd64
nvidia-driver-545/noble 545.29.06-0ubuntu0~gpu24.04.1 amd64
nvidia-driver-550-open/noble 550.127.05-0ubuntu0~gpu24.04.1 amd64
nvidia-driver-550-server-open/noble-updates,noble-security 550.127.05-0ubuntu0.24.04.1 amd64
nvidia-driver-550-server/noble-updates,noble-security 550.127.05-0ubuntu0.24.04.1 amd64
nvidia-driver-550/noble 550.127.05-0ubuntu0~gpu24.04.1 amd64
nvidia-driver-555-open/noble 555.58.02-0ubuntu0~gpu24.04.1 amd64
nvidia-driver-555/noble 555.58.02-0ubuntu0~gpu24.04.1 amd64
nvidia-driver-560-open/noble 560.35.03-0ubuntu0~gpu24.04.4 amd64
nvidia-driver-560/noble 560.35.03-0ubuntu0~gpu24.04.4 amd64
```

## Install a Driver

The highest available version of the CUDA Toolkit depends on the version of the NVIDIA driver. In tests, `nvidia-driver-535` was not compatible with CUDA Toolkit. I tried the next highest version `nvidia-driver-525`

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

### Install "Recommended Driver"
This command installs the driver marked as "recommended". It may not be the latest compatible version.

```
$ sudo ubuntu-drivers autoinstall
```

## Reboot
Reboot the machine after installing the NVIDIA drivers and before installing CUDA Toolkit.

```
$sudo reboot
```

# Check Communication with the NVIDIA Driver

This utility reports these metrics, among others: 
* Driver version: 535.* 
* CUDA version: 12.2.
* GPU Model:  GRID P6-16Q
* GPU Memory: 16 GB

```
$ nvidia-smi
Tue Nov 26 17:47:30 2024
+---------------------------------------------------------------------------------------+
| NVIDIA-SMI 535.183.06             Driver Version: 535.183.06   CUDA Version: 12.2     |
|-----------------------------------------+----------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |         Memory-Usage | GPU-Util  Compute M. |
|                                         |                      |               MIG M. |
|=========================================+======================+======================|
|   0  GRID P6-16Q                    On  | 00000000:02:01.0 Off |                    0 |
| N/A   N/A    P8              N/A /  N/A |      0MiB / 16384MiB |      0%      Default |
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
  adwaita-icon-theme alsa-topology-conf alsa-ucm-conf at-spi2-common at-spi2-core ca-certificates-java cpp-12 dconf-gsettings-backend dconf-service fontconfig fonts-dejavu-extra g++-12 gcc-12 gcc-12-base gsettings-desktop-schemas
  gtk-update-icon-cache hicolor-icon-theme humanity-icon-theme java-common javascript-common libaccinj64-12.0 libamd-comgr2 libamdhip64-5 libasound2-data libasound2t64 libasyncns0 libatk-bridge2.0-0t64 libatk-wrapper-java
  libatk-wrapper-java-jni libatk1.0-0t64 libatspi2.0-0t64 libbabeltrace1 libcairo-gobject2 libcairo2 libcu++-dev libcub-dev libcublas12 libcublaslt12 libcudart12 libcufft11 libcufftw11 libcuinj64-12.0 libcupti-dev libcupti-doc
  libcupti12 libcurand10 libcusolver11 libcusolvermg11 libcusparse12 libdatrie1 libdconf1 libdebuginfod-common libdebuginfod1t64 libflac12t64 libgail-common libgail18t64 libgcc-12-dev libgdk-pixbuf-2.0-0 libgdk-pixbuf2.0-bin
  libgdk-pixbuf2.0-common libgif7 libgraphite2-3 libgtk2.0-0t64 libgtk2.0-bin libgtk2.0-common libharfbuzz0b libhsa-runtime64-1 libhsakmt1 libhwloc-plugins libhwloc15 libibumad3 libice6 libipt2 libjpeg62 libjs-jquery liblcms2-2
  libmp3lame0 libmpg123-0t64 libnppc12 libnppial12 libnppicc12 libnppidei12 libnppif12 libnppig12 libnppim12 libnppist12 libnppisu12 libnppitc12 libnpps12 libnvblas12 libnvidia-compute-535 libnvidia-ml-dev libnvjitlink12 libnvjpeg12
  libnvrtc-builtins12.0 libnvrtc12 libnvtoolsext1 libnvvm4 libogg0 libopus0 libpango-1.0-0 libpangocairo-1.0-0 libpangoft2-1.0-0 libpcsclite1 libpfm4 libpixman-1-0 libpulse0 librdmacm1t64 librsvg2-2 librsvg2-common libsm6 libsndfile1
  libsource-highlight-common libsource-highlight4t64 libstdc++-12-dev libtbb-dev libtbb12 libtbbbind-2-5 libtbbmalloc2 libthai-data libthai0 libthrust-dev libucx0 libvdpau-dev libvdpau1 libvorbis0a libvorbisenc2 libwayland-cursor0
  libwayland-egl1 libxaw7 libxcb-icccm4 libxcb-image0 libxcb-keysyms1 libxcb-render-util0 libxcb-render0 libxcb-shape0 libxcb-util1 libxcb-xkb1 libxcomposite1 libxcursor1 libxdamage1 libxft2 libxi6 libxinerama1 libxkbcommon-x11-0
  libxkbfile1 libxmu6 libxnvctrl0 libxrandr2 libxrender1 libxt6t64 libxtst6 libxv1 libxxf86dga1 mesa-vdpau-drivers node-html5shiv nsight-compute nsight-compute-target nsight-systems nsight-systems-target nvidia-cuda-dev nvidia-cuda-gdb
  nvidia-cuda-toolkit-doc nvidia-opencl-dev nvidia-profiler nvidia-visual-profiler ocl-icd-libopencl1 ocl-icd-opencl-dev opencl-c-headers opencl-clhpp-headers openjdk-8-jre openjdk-8-jre-headless session-migration ubuntu-mono
  vdpau-driver-all x11-common x11-utils
Suggested packages:
  gcc-12-locales cpp-12-doc g++-12-multilib gcc-12-doc gcc-12-multilib default-jre apache2 | lighttpd | httpd alsa-utils libasound2-plugins gvfs libhwloc-contrib-plugins liblcms2-utils opus-tools pcscd pulseaudio librsvg2-bin
  libstdc++-12-doc libtbb-doc libvdpau-doc nodejs nvidia-cuda-samples opencl-clhpp-headers-doc libnss-mdns fonts-nanum fonts-ipafont-gothic fonts-ipafont-mincho fonts-wqy-microhei fonts-wqy-zenhei fonts-indic libvdpau-va-gl1 mesa-utils
Recommended packages:
  libnvcuvid1 luit
The following packages will be REMOVED:
  nvidia-linux-grid-535
The following NEW packages will be installed:
  adwaita-icon-theme alsa-topology-conf alsa-ucm-conf at-spi2-common at-spi2-core ca-certificates-java cpp-12 dconf-gsettings-backend dconf-service fontconfig fonts-dejavu-extra g++-12 gcc-12 gcc-12-base gsettings-desktop-schemas
  gtk-update-icon-cache hicolor-icon-theme humanity-icon-theme java-common javascript-common libaccinj64-12.0 libamd-comgr2 libamdhip64-5 libasound2-data libasound2t64 libasyncns0 libatk-bridge2.0-0t64 libatk-wrapper-java
  libatk-wrapper-java-jni libatk1.0-0t64 libatspi2.0-0t64 libbabeltrace1 libcairo-gobject2 libcairo2 libcu++-dev libcub-dev libcublas12 libcublaslt12 libcudart12 libcufft11 libcufftw11 libcuinj64-12.0 libcupti-dev libcupti-doc
  libcupti12 libcurand10 libcusolver11 libcusolvermg11 libcusparse12 libdatrie1 libdconf1 libdebuginfod-common libdebuginfod1t64 libflac12t64 libgail-common libgail18t64 libgcc-12-dev libgdk-pixbuf-2.0-0 libgdk-pixbuf2.0-bin
  libgdk-pixbuf2.0-common libgif7 libgraphite2-3 libgtk2.0-0t64 libgtk2.0-bin libgtk2.0-common libharfbuzz0b libhsa-runtime64-1 libhsakmt1 libhwloc-plugins libhwloc15 libibumad3 libice6 libipt2 libjpeg62 libjs-jquery liblcms2-2
  libmp3lame0 libmpg123-0t64 libnppc12 libnppial12 libnppicc12 libnppidei12 libnppif12 libnppig12 libnppim12 libnppist12 libnppisu12 libnppitc12 libnpps12 libnvblas12 libnvidia-compute-535 libnvidia-ml-dev libnvjitlink12 libnvjpeg12
  libnvrtc-builtins12.0 libnvrtc12 libnvtoolsext1 libnvvm4 libogg0 libopus0 libpango-1.0-0 libpangocairo-1.0-0 libpangoft2-1.0-0 libpcsclite1 libpfm4 libpixman-1-0 libpulse0 librdmacm1t64 librsvg2-2 librsvg2-common libsm6 libsndfile1
  libsource-highlight-common libsource-highlight4t64 libstdc++-12-dev libtbb-dev libtbb12 libtbbbind-2-5 libtbbmalloc2 libthai-data libthai0 libthrust-dev libucx0 libvdpau-dev libvdpau1 libvorbis0a libvorbisenc2 libwayland-cursor0
  libwayland-egl1 libxaw7 libxcb-icccm4 libxcb-image0 libxcb-keysyms1 libxcb-render-util0 libxcb-render0 libxcb-shape0 libxcb-util1 libxcb-xkb1 libxcomposite1 libxcursor1 libxdamage1 libxft2 libxi6 libxinerama1 libxkbcommon-x11-0
  libxkbfile1 libxmu6 libxnvctrl0 libxrandr2 libxrender1 libxt6t64 libxtst6 libxv1 libxxf86dga1 mesa-vdpau-drivers node-html5shiv nsight-compute nsight-compute-target nsight-systems nsight-systems-target nvidia-cuda-dev nvidia-cuda-gdb
  nvidia-cuda-toolkit nvidia-cuda-toolkit-doc nvidia-opencl-dev nvidia-profiler nvidia-visual-profiler ocl-icd-libopencl1 ocl-icd-opencl-dev opencl-c-headers opencl-clhpp-headers openjdk-8-jre openjdk-8-jre-headless session-migration
  ubuntu-mono vdpau-driver-all x11-common x11-utils
0 upgraded, 178 newly installed, 1 to remove and 3 not upgraded.
Need to get 2,317 MB of archives.
After this operation, 7,149 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
```

# Report CUDA Toolkit Version

```
$ which nvcc
/usr/bin/nvcc
```

```
$ nvcc --version
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2023 NVIDIA Corporation
Built on Fri_Jan__6_16:45:21_PST_2023
Cuda compilation tools, release 12.0, V12.0.140
Build cuda_12.0.r12.0/compiler.32267302_0
```

# Links

* https://varhowto.com/check-cuda-version/
* https://gist.github.com/denguir/b21aa66ae7fb1089655dd9de8351a202



