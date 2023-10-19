# CUDA in Windows 11

# Check for Installed CUDA

Check whether CUDA Toolkit is already installed. In this example, CUDA Toolkit is not already installed.

```
>where nvcc
INFO: Could not find files for the given pattern(s).

C:\Users\jquisenberry>nvcc --version
'nvcc' is not recognized as an internal or external command,
operable program or batch file.

```

# Install Visual Studio

The CUDA Toolkit installer checks whether Visual Studio is installed. Visual Studio is required to enable full functionality. 

Download and install Visual Studio 2022 Community from https://visualstudio.microsoft.com/. 

I installed multi-platform .NET and C++ packages.

# Install CUDA Toolkit

Main Site: https://developer.nvidia.com/cuda-downloads

Direct Download: https://developer.download.nvidia.com/compute/cuda/12.2.2/local_installers/cuda_12.2.2_537.13_windows.exe


# Detect CUDA Version

```
nvcc --version

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



