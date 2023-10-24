# CUDA in Ubuntu 22.04 LTS

# Check for Installed CUDA

Check whether CUDA Toolkit is already installed. In this example, CUDA Toolkit is not already installed.

```
$which nvcc

$nvcc --version
Command 'nvcc' not found, but can be installed with:
apt install nvidia-cuda-toolkit
Please ask your administrator.

```

# Install CUDA Toolkit

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
>where nvcc
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v12.2\bin\nvcc.exe

>nvcc --version
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2023 NVIDIA Corporation
Built on Tue_Aug_15_22:09:35_Pacific_Daylight_Time_2023
Cuda compilation tools, release 12.2, V12.2.140
Build cuda_12.2.r12.2/compiler.33191640_0
```

```
>nvidia-smi
Wed Oct 18 21:28:37 2023
+---------------------------------------------------------------------------------------+
| NVIDIA-SMI 537.13                 Driver Version: 537.13       CUDA Version: 12.2     |
|-----------------------------------------+----------------------+----------------------+
| GPU  Name                     TCC/WDDM  | Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |         Memory-Usage | GPU-Util  Compute M. |
|                                         |                      |               MIG M. |
|=========================================+======================+======================|
|   0  NVIDIA GeForce RTX 3060      WDDM  | 00000000:01:00.0 Off |                  N/A |
| 36%   32C    P8               5W / 170W |    399MiB / 12288MiB |      4%      Default |
|                                         |                      |                  N/A |
+-----------------------------------------+----------------------+----------------------+

+---------------------------------------------------------------------------------------+
| Processes:                                                                            |
|  GPU   GI   CI        PID   Type   Process name                            GPU Memory |
|        ID   ID                                                             Usage      |
|=======================================================================================|
|    0   N/A  N/A      7564    C+G   ...oogle\Chrome\Application\chrome.exe    N/A      |
|    0   N/A  N/A      9760    C+G   ...e Stream\82.0.1.0\GoogleDriveFS.exe    N/A      |
|    0   N/A  N/A     12636    C+G   C:\Windows\explorer.exe                   N/A      |
|    0   N/A  N/A     24280    C+G   ...GeForce Experience\NVIDIA Share.exe    N/A      |
|    0   N/A  N/A     27972    C+G   ...1.0_x64__8wekyb3d8bbwe\Video.UI.exe    N/A      |
+---------------------------------------------------------------------------------------+
```

# Links

https://varhowto.com/check-cuda-version/



