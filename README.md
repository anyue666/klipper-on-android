XServer-XSDL-1.20.51.apk（必装） 下载链接：https://sourceforge.net/projects/libsdl-android/files/apk/XServer-XSDL/
    
linuxdeploy-2.6.0-259.apk（必装） 下载链接：https://github.com/meefik/linuxdeploy/releases/download/2.6.0/linuxdeploy-2.6.0-259.apk

kerneladiutor_248.apk（开启所有CPU核心，推荐安装） 下载链接：https://f-droid.org/en/packages/com.nhellfire.kerneladiutor/

termux_118.apk（选装，需要时再安装）下载链接：https://github.com/termux/termux-app/releases/tag/v0.118.0
		
电脑端：

Xshell（必装）官网地址：https://www.netsarang.com/en/xshell/

Xftp（选装，建议安装）：https://www.netsarang.com/en/xftp/






	屏幕常亮  （勾选）
	
	锁定Wi-Fi （勾选）

	CPU唤醒   （勾选）

	开机自启动 （勾选）

	语言      （简体中文）

	启动延迟   （5）  （以秒为单位，根据需要设置，想迟一点启动就将数字调大）

	联网更新   （勾选）


	发行版 （Debian）

	架构（armhf）（自行查询自己手机处理器型号，如果支持64位就选arm64）

	发行版本 （stable）

	源地址 （ http://ftp.cn.debian.org/debian/ ）（国内源安装更快）

	安装类型 （目录）

	安装路径 （/data/debian11）

	用户名 （print3D）（因为涉及到klipper配置文件的路径，所以建议就用这个用户名）

	密码：（123456）（随便设置，能记住就行）

	本地化 （zh-CN.UTF-8）（系统汉化，便于使用）

	初始化 （启用）

	初始化系统 （sysV）

	挂载点 （可选，此应用场景下一般用不到）

	挂载点列表 （/sdcard/-/mnt/sdcard/）（可选，此应用场景下一般用不到）

	SSH （启用）（必须开启，否则连不上linux系统）

	图形界面 （启用）

	图形子系统 （X11）

	图形界面设置 （取消勾选自动打开XServer-XSDL）（一键配置脚本里已经配置自动开启XServer-XSDL客户端，此处不需要勾选）

	桌面环境 （XTerm）

## 4.klipper安装环境配置 ##

ssh登录进入debian系统后执行以下命令：
只要很简单的命令：
	
	groupadd print3D
	useradd -m print3D -g print3D -s /bin/bash -d /home/print3D
	passwd print3D
	usermod -G 3003 root
	usermod -G 3003 print3D

	su -
	chmod u+w /etc/sudoers
	apt update && apt install vim -y
	vim /etc/sudoers
	root ALL=(ALL:ALL) ALL语句，在下面添加一行：
	print3D ALL=(ALL:ALL) ALL
	:wq!

	sudo usermod -a -G aid_inet,aid_net_raw root

###由于安卓系统上chroot容器权限问题，除初始登录用户外，默认其他用户没有网络权限，包括root用户。此命令可以解决使用sudo命令时root用户无法联网的问题。

	sudo apt update

###更新系统软件包

	sudo apt install -y git vim wget

###安装必要的工具软件

## 5.使用kiauh安装klipper ##

	cd ~

###进入登录用户家目录

	git clone https://github.com/th33xitus/kiauh.git

###官方kiauh脚本地址

	git clone https://gitee.com/miroky/kiauh.git

###国内kiauh脚本地址（与上面官方地址二选一即可）

	./kiauh/kiauh.sh

## 6.klipper全家桶配置 ##

使用Xftp或命令行进入以下路径：

	/home/print3D/printer_data/config/

将里面的 fluidd.cfg,moonraker.conf,printer.cfg 进行备份之后把原文件删除。

	cd ~

###进入登录用户家目录

将本仓库里的fluidd.cfg,homing_override.cfg,moonraker.conf,printer.cfg 这4个文件下载后放到 /home/print3D/printer_data/config/ 路径下。

或者想省事，直接执行以下命令：

	sudo wget -P /home/print3D/printer_data/config/  https://raw.githubusercontent.com/gaifeng8864/klipper-on-android/main/fluidd.cfg

	sudo wget -P /home/print3D/printer_data/config/  https://raw.githubusercontent.com/gaifeng8864/klipper-on-android/main/homing_override.cfg

	sudo wget -P /home/print3D/printer_data/config/  https://raw.githubusercontent.com/gaifeng8864/klipper-on-android/main/moonraker.conf

	sudo wget -P /home/print3D/printer_data/config/  https://raw.githubusercontent.com/gaifeng8864/klipper-on-android/main/printer.cfg


     cd ~

     sudo wget https://raw.githubusercontent.com/anyue666/klipper-on-android/main/configuration_klipper_family.sh

     bash configuration_klipper_family.sh


     源: /data/data/com.octo4a/files
     
     目标: /home/android/octo4a
     
     /home/android/octo4a/serialpipe
     
     is the serial port you need to use in your printer.cfg
     
     Make the serial device accessible to Klipper:

     sudo chmod 777 /dev/ttyACM0
# or 
     sudo chmod 777 /dev/ttyUSB0
# or 
     sudo chmod 777 /home/android/octo4a/serialpipe

     ls -al /dev/

使用识别的设备名称替换 configuration_klipper_family.sh 内的 ttyACM0


然后重新执行： 

	bash configuration_klipper_family.sh







