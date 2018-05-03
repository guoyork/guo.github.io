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

![avatar](/blog_2_2.png)

下载runfile文件

之后按ctrl+alt+F1进入控制台，登录后在控制台输入

	sudo service lightdm stop
	
关闭图形界面

在控制台输入

	sudo sh cuda_9.0.176_384.81_linux.run
	
运行CUDA工具安装包

所有的问题如果有默认就选默认，否则就选yes。

因为安装包中带有NVIDIA显卡驱动，所以如果已经安装过显卡驱动可以在询问是否安装显卡驱动时选择no。

安装好后启动图形界面

	sudo service lightdm start
	
之后设置环境变量

	sudo gedit /etc/profile
	
在文件末尾输入(64位系统)

	export PATH=/usr/local/cuda/bin:$PATH
	export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
	
保存并重启，之后检查是否安装成功

1. 检查显卡驱动是否安装成功

		cat /proc/driver/nvidia/version
	
2. 验证CUDA Toolkit
	
		nvcc -V
	
3. 编译sample，这一步需要大概10~20分钟，如果出错会立刻停止

		cd /home/user_name/NVIDIA_CUDA-9.0_Samples
	
		sudo make
	
4. 运行编译完的sample

		cd bin/x86_64/linux/release
	
		./deviceQuery
	
5. 如果输出Result = PASS则成功，否则会输出Result = FAIL

6. 最后检查CUDA-Capable deviced的连接情况

		./bandwidthTest
	
### 安装cuDNN

[back](./)
