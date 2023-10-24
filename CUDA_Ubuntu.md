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

# Install Correct CUDA Driver

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

## To Install a Specific Driver

```
$ sudo apt install nvidia-driver-535
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following packages were automatically installed and are no longer required:
  ca-certificates-java cuda-cccl-12-2 cuda-command-line-tools-12-2 cuda-compiler-12-2 cuda-crt-12-2 cuda-cudart-12-2 cuda-cudart-dev-12-2 cuda-cuobjdump-12-2 cuda-cupti-12-2 cuda-cupti-dev-12-2
  cuda-cuxxfilt-12-2 cuda-documentation-12-2 cuda-driver-dev-12-2 cuda-gdb-12-2 cuda-libraries-12-2 cuda-libraries-dev-12-2 cuda-nsight-12-2 cuda-nsight-compute-12-2 cuda-nsight-systems-12-2 cuda-nvcc-12-2
  cuda-nvdisasm-12-2 cuda-nvml-dev-12-2 cuda-nvprof-12-2 cuda-nvprune-12-2 cuda-nvrtc-12-2 cuda-nvrtc-dev-12-2 cuda-nvtx-12-2 cuda-nvvm-12-2 cuda-nvvp-12-2 cuda-opencl-12-2 cuda-opencl-dev-12-2
  cuda-profiler-api-12-2 cuda-sanitizer-12-2 cuda-toolkit-12-2 cuda-toolkit-12-2-config-common cuda-toolkit-12-config-common cuda-toolkit-config-common cuda-tools-12-2 cuda-visual-tools-12-2 default-jre
  default-jre-headless fonts-dejavu-extra gds-tools-12-2 java-common javascript-common libaccinj64-11.5 libatk-wrapper-java libatk-wrapper-java-jni libbabeltrace1 libboost-regex1.74.0 libcub-dev libcublas-12-2
  libcublas-dev-12-2 libcublas11 libcublaslt11 libcudart11.0 libcufft-12-2 libcufft-dev-12-2 libcufft10 libcufftw10 libcufile-12-2 libcufile-dev-12-2 libcupti-dev libcupti-doc libcupti11.5 libcurand-12-2
  libcurand-dev-12-2 libcurand10 libcusolver-12-2 libcusolver-dev-12-2 libcusolver11 libcusolvermg11 libcusparse-12-2 libcusparse-dev-12-2 libcusparse11 libdebuginfod-common libdebuginfod1 libegl-dev libgif7
  libgl-dev libgl1-mesa-dev libgles-dev libgles1 libglvnd-core-dev libglvnd-dev libglx-dev libipt2 libjs-jquery libnpp-12-2 libnpp-dev-12-2 libnppc11 libnppial11 libnppicc11 libnppidei11 libnppif11 libnppig11
  libnppim11 libnppist11 libnppisu11 libnppitc11 libnpps11 libnvblas11 libnvidia-egl-wayland1 libnvjitlink-12-2 libnvjitlink-dev-12-2 libnvjpeg-12-2 libnvjpeg-dev-12-2 libnvjpeg11 libnvrtc-builtins11.5
  libnvrtc11.2 libnvtoolsext1 libnvvm4 libopengl-dev libpcsclite1 libpthread-stubs0-dev libsource-highlight-common libsource-highlight4v5 libtbb-dev libtbb12 libtbbmalloc2 libthrust-dev libtinfo5 libvdpau-dev
  libx11-dev libxau-dev libxcb-icccm4 libxcb-image0 libxcb-keysyms1 libxcb-render-util0 libxcb-xinerama0 libxcb-xinput0 libxcb-xkb1 libxcb1-dev libxdmcp-dev libxkbcommon-x11-0 node-html5shiv
  nsight-compute-2023.2.2 nsight-systems-2023.2.3 nvidia-cuda-gdb nvidia-cuda-toolkit-doc nvidia-firmware-535-535.113.01 nvidia-modprobe nvidia-opencl-dev ocl-icd-libopencl1 ocl-icd-opencl-dev opencl-c-headers
  opencl-clhpp-headers openjdk-11-jre openjdk-11-jre-headless openjdk-8-jre openjdk-8-jre-headless x11proto-dev xorg-sgml-doctools xtrans-dev
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  libnvidia-cfg1-535 libnvidia-common-535 libnvidia-compute-535 libnvidia-decode-535 libnvidia-encode-535 libnvidia-extra-535 libnvidia-fbc1-535 libnvidia-gl-535 nvidia-compute-utils-535 nvidia-dkms-535
  nvidia-kernel-common-535 nvidia-kernel-source-535 nvidia-utils-535 xserver-xorg-video-nvidia-535
Recommended packages:
  libnvidia-compute-535:i386 libnvidia-decode-535:i386 libnvidia-encode-535:i386 libnvidia-fbc1-535:i386 libnvidia-gl-535:i386
The following packages will be REMOVED:
  libnvidia-cfg1-470 libnvidia-common-470 libnvidia-compute-470 libnvidia-decode-470 libnvidia-encode-470 libnvidia-extra-470 libnvidia-fbc1-470 libnvidia-gl-470 libnvidia-ifr1-470
  linux-modules-nvidia-470-5.15.0-87-generic linux-modules-nvidia-470-generic nvidia-compute-utils-470 nvidia-driver-470 nvidia-kernel-common-470 nvidia-kernel-source-470 nvidia-utils-470
  xserver-xorg-video-nvidia-470
The following NEW packages will be installed:
  libnvidia-cfg1-535 libnvidia-common-535 libnvidia-compute-535 libnvidia-decode-535 libnvidia-encode-535 libnvidia-extra-535 libnvidia-fbc1-535 libnvidia-gl-535 nvidia-compute-utils-535 nvidia-dkms-535
  nvidia-driver-535 nvidia-kernel-common-535 nvidia-kernel-source-535 nvidia-utils-535 xserver-xorg-video-nvidia-535
0 upgraded, 15 newly installed, 17 to remove and 0 not upgraded.
Need to get 307 MB of archives.
After this operation, 203 MB of additional disk space will be used.
Do you want to continue? [Y/n] y

```

## To Install the Recommended Driver

```
$ sudo ubuntu-drivers autoinstall
```




# Check for Installed CUDA

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
The following packages were automatically installed and are no longer required:
  cuda-cccl-12-2 cuda-command-line-tools-12-2 cuda-compiler-12-2 cuda-crt-12-2
  cuda-cudart-12-2 cuda-cudart-dev-12-2 cuda-cuobjdump-12-2 cuda-cupti-12-2
  cuda-cupti-dev-12-2 cuda-cuxxfilt-12-2 cuda-documentation-12-2
  cuda-driver-dev-12-2 cuda-gdb-12-2 cuda-libraries-12-2
  cuda-libraries-dev-12-2 cuda-nsight-12-2 cuda-nsight-compute-12-2
  cuda-nsight-systems-12-2 cuda-nvcc-12-2 cuda-nvdisasm-12-2
  cuda-nvml-dev-12-2 cuda-nvprof-12-2 cuda-nvprune-12-2 cuda-nvrtc-12-2
  cuda-nvrtc-dev-12-2 cuda-nvtx-12-2 cuda-nvvm-12-2 cuda-nvvp-12-2
  cuda-opencl-12-2 cuda-opencl-dev-12-2 cuda-profiler-api-12-2
  cuda-sanitizer-12-2 cuda-toolkit-12-2 cuda-toolkit-12-2-config-common
  cuda-toolkit-12-config-common cuda-toolkit-config-common cuda-tools-12-2
  cuda-visual-tools-12-2 dctrl-tools dkms gds-tools-12-2 libcublas-12-2
  libcublas-dev-12-2 libcufft-12-2 libcufft-dev-12-2 libcufile-12-2
  libcufile-dev-12-2 libcurand-12-2 libcurand-dev-12-2 libcusolver-12-2
  libcusolver-dev-12-2 libcusparse-12-2 libcusparse-dev-12-2 libnpp-12-2
  libnpp-dev-12-2 libnvidia-cfg1-535 libnvidia-common-535 libnvidia-decode-535
  libnvidia-encode-535 libnvidia-extra-535 libnvidia-fbc1-535 libnvidia-gl-535
  libnvjitlink-12-2 libnvjitlink-dev-12-2 libnvjpeg-12-2 libnvjpeg-dev-12-2
  libtinfo5 libxcb-icccm4 libxcb-image0 libxcb-keysyms1 libxcb-render-util0
  libxcb-xinerama0 libxcb-xinput0 libxcb-xkb1 libxkbcommon-x11-0 libxnvctrl0
  nsight-compute-2023.2.2 nsight-systems-2023.2.3 nvidia-compute-utils-535
  nvidia-firmware-535-535.113.01 nvidia-kernel-common-535
  nvidia-kernel-source-535 nvidia-modprobe nvidia-prime nvidia-settings
  nvidia-utils-535 pkg-config screen-resolution-extra
  xserver-xorg-video-nvidia-535
Use 'sudo apt autoremove' to remove them.
$ sudo apt install nvidia-cuda-toolkit
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following packages were automatically installed and are no longer required:
  cuda-cccl-12-2 cuda-command-line-tools-12-2 cuda-compiler-12-2 cuda-crt-12-2
  cuda-cudart-12-2 cuda-cudart-dev-12-2 cuda-cuobjdump-12-2 cuda-cupti-12-2
  cuda-cupti-dev-12-2 cuda-cuxxfilt-12-2 cuda-documentation-12-2
  cuda-driver-dev-12-2 cuda-gdb-12-2 cuda-libraries-12-2
  cuda-libraries-dev-12-2 cuda-nsight-12-2 cuda-nsight-compute-12-2
  cuda-nsight-systems-12-2 cuda-nvcc-12-2 cuda-nvdisasm-12-2
  cuda-nvml-dev-12-2 cuda-nvprof-12-2 cuda-nvprune-12-2 cuda-nvrtc-12-2
  cuda-nvrtc-dev-12-2 cuda-nvtx-12-2 cuda-nvvm-12-2 cuda-nvvp-12-2
  cuda-opencl-12-2 cuda-opencl-dev-12-2 cuda-profiler-api-12-2
  cuda-sanitizer-12-2 cuda-toolkit-12-2 cuda-toolkit-12-2-config-common
  cuda-toolkit-12-config-common cuda-toolkit-config-common cuda-tools-12-2
  cuda-visual-tools-12-2 dctrl-tools dkms gds-tools-12-2 libcublas-12-2
  libcublas-dev-12-2 libcufft-12-2 libcufft-dev-12-2 libcufile-12-2
  libcufile-dev-12-2 libcurand-12-2 libcurand-dev-12-2 libcusolver-12-2
  libcusolver-dev-12-2 libcusparse-12-2 libcusparse-dev-12-2 libnpp-12-2
  libnpp-dev-12-2 libnvidia-cfg1-535 libnvidia-common-535 libnvidia-decode-535
  libnvidia-encode-535 libnvidia-extra-535 libnvidia-fbc1-535 libnvidia-gl-535
  libnvjitlink-12-2 libnvjitlink-dev-12-2 libnvjpeg-12-2 libnvjpeg-dev-12-2
  libtinfo5 libxcb-icccm4 libxcb-image0 libxcb-keysyms1 libxcb-render-util0
  libxcb-xinerama0 libxcb-xinput0 libxcb-xkb1 libxkbcommon-x11-0 libxnvctrl0
  nsight-compute-2023.2.2 nsight-systems-2023.2.3 nvidia-compute-utils-535
  nvidia-firmware-535-535.113.01 nvidia-kernel-common-535
  nvidia-kernel-source-535 nvidia-modprobe nvidia-prime nvidia-settings
  nvidia-utils-535 pkg-config screen-resolution-extra
  xserver-xorg-video-nvidia-535
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  javascript-common libaccinj64-11.5 libbabeltrace1 libboost-regex1.74.0
  libcub-dev libcublas11 libcublaslt11 libcudart11.0 libcufft10 libcufftw10
  libcuinj64-11.5 libcupti-dev libcupti-doc libcupti11.5 libcurand10
  libcusolver11 libcusolvermg11 libcusparse11 libdebuginfod-common
  libdebuginfod1 libegl-dev libgail-common libgail18 libgl-dev libgl1-mesa-dev
  libgles-dev libgles1 libglvnd-core-dev libglvnd-dev libglx-dev libgtk2.0-0
  libgtk2.0-bin libgtk2.0-common libipt2 libjs-jquery libnppc11 libnppial11
  libnppicc11 libnppidei11 libnppif11 libnppig11 libnppim11 libnppist11
  libnppisu11 libnppitc11 libnpps11 libnvblas11 libnvidia-ml-dev libnvjpeg11
  libnvrtc-builtins11.5 libnvrtc11.2 libnvtoolsext1 libnvvm4 libopengl-dev
  libpthread-stubs0-dev libsource-highlight-common libsource-highlight4v5
  libtbb-dev libtbb12 libtbbmalloc2 libthrust-dev libvdpau-dev libx11-dev
  libxau-dev libxcb1-dev libxdmcp-dev node-html5shiv nvidia-cuda-dev
  nvidia-cuda-gdb nvidia-cuda-toolkit-doc nvidia-opencl-dev nvidia-profiler
  nvidia-visual-profiler ocl-icd-libopencl1 ocl-icd-opencl-dev
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

```
$ nvidia-smi
NVIDIA-SMI has failed because it couldn't communicate with the NVIDIA driver. Make sure that the latest NVIDIA driver is installed and running.

```

# Links

https://varhowto.com/check-cuda-version/



