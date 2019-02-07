# 磁盘分区
## 主分区

## 扩展分区

## 逻辑分区
> 逻辑分区必须建立在扩展分区中

# 先装win后装linux好
linux的引导加载程序grub既能识别linux的核心启动文件，也能识别windows的核心启动文件。而windows的引导加载程序却不能识别linux的核心启动文件，如果先装linux的，后装windows的话，由于windows默认把引导加载程序安装在MBR与超级块中，这样的话就覆盖掉原来的linux的grub了，导致磁盘的MBR只能识别windows的而不能进入linux了，所以每次加载BIOS信息后，你只能毫无选择的进入windows了

# Legacy BIOS 和 UEFI BIOS 的区别
## BIOS
> Basic Input/Output System
