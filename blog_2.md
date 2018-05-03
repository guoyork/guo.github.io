---
layout: default
---

# tensorflow-gpu的配置和安装
### 系统配置

![avatar](/blog_2_1.png)

### 更新源

打开终端，运行

	sudo apt-get update
	
	sudo apt-get upgrade

这个步骤需要花比较多的时间

### 禁用nouveau驱动

在终端中输入

	lsmod | grep nouveau

如果有输出，说明nouveau驱动正在运行，需要我们手动禁用。

在终端中输入

	sudo gedit /etc/modprobe.d/blacklist-nouveau.conf
	
在文件中输入
	
	blacklist nouveau 
	
	options nouveau modeset=0
	
之后关闭并保存文件

再在终端中输入

	sudo update-initramfs -u

之后重启即可

### 安装CUDA9.0

打开[CUDA9.0官网](https://developer.nvidia.com/cuda-90-download-archive)



[back](./)
