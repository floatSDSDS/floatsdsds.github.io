---
layout: post
title: "cuda安装ubuntu16.04"
excerpt: "按照官方文档安装NVIDIA CUDA及过程记录"
tags:
  - translate
  - experience
  - ZH
---

- 依照[1] [官方文档](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html)安装cuda，不完全（随缘）翻译√，全过程纪录。
- 过程中如有错漏邮件至float.hellowmr@gmail.com
- `floatsd@floatsd:~$`后为需要运行的指令，否则为返回输出的结果

## 1. CUDA
- CUDA是NVIDIA开发的一款利用GPU进行并行计算架构，支持应用协同使用CPU（串行）和GPU（并行），CPU和GPU将被视为独立不相关的设备并使用独立的内存。这意味着CPU和GPU在运行时将不会竞争资源。而对于如GPU多核来说，所有核心将共享内存空间，则数据传输将不会受限于总线带宽。

### 1.1. 系统要求
- 配置的检查见[1]Table 1.
  - 一块支持CUDA的英伟达显卡
  - 合适的gcc编译版本及工具链
  - NVIDIA CUDA Toolkit

## 2. 依赖项检查，安装CUDA
### 2.0. 卸载冲突项
- 本机是第一次安装CUDA，在此之前940MX也没有安装驱动，所以不存在冲突的可能性。在安装之前需要卸载会造成冲突的软件，详见[1]2.7节

### 2.1. 检查GPU是否支持CUDA
```
floatsd@floatsd:~$ lspci | grep -i nvidia
02:00.0 3D controller: NVIDIA Corporation GM108M [GeForce 940MX] (rev a2)
```
- 返回为电脑英伟达显卡型号，在[这里](https://developer.nvidia.com/cuda-gpus)检查该型号是否支持CUDA。如果没有任何返回结果（且确定自己电脑显卡为英伟达支持CUDA型号），输入`update-pciids`更新PCI硬件数据库。

### 2.2. 检查Linux版本是否支持

```
floatsd@floatsd:~$  uname -m && cat /etc/*release
x86_64
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=16.04
DISTRIB_CODENAME=xenial
DISTRIB_DESCRIPTION="Ubuntu 16.04.3 LTS"
NAME="Ubuntu"
VERSION="16.04.3 LTS (Xenial Xerus)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 16.04.3 LTS"
VERSION_ID="16.04"
HOME_URL="http://www.ubuntu.com/"
SUPPORT_URL="http://help.ubuntu.com/"
BUG_REPORT_URL="http://bugs.launchpad.net/ubuntu/"
VERSION_CODENAME=xenial
UBUNTU_CODENAME=xenial
```
- 返回如上，可以看到本机ubuntu桌面版为16.04，x86_64代表系统为64位系统

### 2.3. 检查系统gcc版本
```
floatsd@floatsd:~$ gcc --version
gcc (Ubuntu 5.4.0-6ubuntu1~16.04.5) 5.4.0 20160609
Copyright (C) 2015 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```
- 显示gcc版本为5.4.0，对照[1]Table 1.中对应系统版本的gcc要求，需为表格中版本及以上
- 如果返回错误需要安装对应版本gcc编译环境

### 2.4. 检查系统内核版本及头文件
- 在安装CUDA驱动前需要确保系统内核版本受支持（见Table 1.)且头文件和内核版本对应。
- 检查内核版本
```
floatsd@floatsd:~$ uname -r
4.10.0-40-generic
```
- 如版本需要更新，对ubuntu来说，运行如下指令：
```
floatsd@floatsd:~$ sudo apt-get install linux-headers-$(uname -r)
[sudo] password for floatsd:
Reading package lists... Done
Building dependency tree       
Reading state information... Done
linux-headers-4.10.0-40-generic is already the newest version (4.10.0-40.44~16.04.1).
linux-headers-4.10.0-40-generic set to manually installed.
0 upgraded, 0 newly installed, 0 to remove and 70 not upgraded.
```

### 2.5. 选择安装方式
- CUDA有两种安装方式
  - distribution-independent(.runfile)：优势在于可以支持更广的Linux发型系统，但不会随着包管理系统更新
  - distribution-specific(.RPM, .Deb)：会随着包管理系统更新，所以如果系统版本支持distribution-specific，安装这个版本是比较方便的（sudo apt-get update自动更新什么的：））

### 2.6. 下载NVIDIA CUDA Toolkit
- [下载地址](http://developer.nvidia.com/cuda-downloads.)
- 选择对应版本如图，该toolkit包含了安装所需的头文件，源代码和其他依赖资源（文中使用的是network安装方式，local会把所有的资源首先下载下来）
<figure class="one">
    <a href="/images/cudaToolkitDownload.png"><img src="/images/cudaToolkitDownload.png"></a>
</figure>

- deb安装包下载好后，按照下载地址中指示代码，进入安装包所在路径进行安装

```
loatsd@floatsd:~$ cd nvidia
floatsd@floatsd:~/nvidia$ sudo dpkg -i cuda-repo-ubuntu1604_9.0.176-1_amd64.deb
(Reading database ... 243002 files and directories currently installed.)
Preparing to unpack cuda-repo-ubuntu1604_9.0.176-1_amd64.deb ...
Unpacking cuda-repo-ubuntu1604 (9.0.176-1) over (9.0.176-1) ...
Setting up cuda-repo-ubuntu1604 (9.0.176-1) ...

The public CUDA GPG key does not appear to be installed.
To install the key, run this command:
sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub

floatsd@floatsd:~/nvidia$ sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub
Executing: /tmp/tmp.TwJq9NMavo/gpg.1.sh --fetch-keys
http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub
gpg: key 7FA2AF80: public key "cudatools <cudatools@nvidia.com>" imported
gpg: Total number processed: 1
gpg:               imported: 1  (RSA: 1)


floatsd@floatsd:~/nvidia$ sudo apt-get update
floatsd@floatsd:~/nvidia$ sudo apt-get install cuda
//此处是一段漫长的下载安装
```

- 安装完毕显示需要关闭UEFI

<figure class="one">
    <a href="/images/CudaInterface1.png"><img src="/images/CudaInterface1.png"></a>
</figure>
- 关机，进入bios disable secure boot

## 3. 配置环境及安装检查
 安装完毕后，推荐手动配置环境1. 添加路径变量（如使用distribution-independent方法安装参见[1]7.1节）
```
floatsd@floatsd:~/nvidia$ export PATH=/usr/local/cuda-9.0/bin${PATH:+:${PATH}}
```

### 3.1 检查安装状态
- 检查gcc及内核等依赖版本

```
floatsd@floatsd:~/nvidia$ cat /proc/driver/nvidia/version
NVRM version: NVIDIA UNIX x86_64 Kernel Module  384.98  Thu Oct 26 15:16:01 PDT 2017
GCC version:  gcc version 5.4.0 20160609 (Ubuntu 5.4.0-6ubuntu1~16.04.5)
```

- 检查CUDA是否安装成功

```
floatsd@floatsd:~/nvidia$ nvcc -V
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2017 NVIDIA Corporation
Built on Fri_Sep__1_21:08:03_CDT_2017
Cuda compilation tools, release 9.0, V9.0.176
```

- 检查驱动版本显卡配置

```
floatsd@floatsd:~/nvidia$ nvidia-smi
Mon Dec  4 16:45:53 2017       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 384.98                 Driver Version: 384.98                    |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce 940MX       Off  | 00000000:02:00.0 Off |                  N/A |
| N/A   38C    P0    N/A /  N/A |    486MiB /  2002MiB |      6%      Default |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0      1177      G   /usr/lib/xorg/Xorg                           314MiB |
|    0      1843      G   compiz                                        77MiB |
|    0      2356      G   ...passed-by-fd --v8-snapshot-passed-by-fd    43MiB |
|    0      2607      G   /proc/self/exe                                49MiB |
+-----------------------------------------------------------------------------+

```
