# ASRock-Z390-Phantom-ITX-OpenCore-Hackintosh

### [English](README.md) | [中文](README-zh.md)

## Configuration

Motherboard：ASRockz390 phantom gaming-itx/ac

cpu：i7 9700k

Graphics：AMD Sapphire rx480

Wireless network card：BCM943602CS

## Drive situation

* System stability：No system crashes，System has been update10.15.1 Beta2(19B77a)

* Graphics：rx480 driver is normal，UHD630 working frequency 1.2Ghz
* Sound card：Normal drive
* wifi、Bluetooth、Handoff、Sidecar Normal use
* Sleep &wake：Manual click sleep

![QQ20191013-105901](http://github.fangf.cc/mweb/QQ20191013-105901.png)
* location：work well
* nvram：The nvram.plst file can be generated normally.
    
    But the boot did not read, wait for the official fix.
    
    The necessity of nvram：
    
    Because the official description can achieve 
    
    the default boot of the startup disk like real-imac, 
    
    and ensure other functions are heavy.
    
    Don't lose after starting, for example find for my device    
![QQ20191013-112532](http://github.fangf.cc/mweb/QQ20191013-112532.png)
* usb：No abnormality

![QQ20191013-112335](http://github.fangf.cc/mweb/QQ20191013-112335.png)

* type-c：Plug in the device before booting, hotplug





# Update log

### 2019-10-17

* Re-impersonating the EC, the previous method has an error

* Synchronize updates to official Opencore

* Remove apfs.efi (only for fusiondrive)

* Add usb custom full port version, you need to manually switch

* ![](http://github.fangf.cc/mweb/15712818344299.jpg)


### 2019-10-13

* Synchronously update the official OpenCore v0.5.2 10.13 content

* Sleep is very well

   Output the last sleep time     `sysctl -a |grep sleeptime`
    
   Output the last wake up time  `sysctl -a |grep waketime`

![A78F9F5414D437EC1FF6FD74E1CF0E64](http://github.fangf.cc/mweb/A78F9F5414D437EC1FF6FD74E1CF0E64.jpg)


### 2019-10-09

* Change the scanning policy and boot Macintosh HD directly into the macOOS system by default

* Add win boot, you need to modify the boot path for your own（Misc-Entries-Path）

### 2019-10-04
* Startup file config optimization settings [reference](https://insanelymacdiscord.github.io/Getting-Started-With-OpenCore/)

* **Add IOElectrify.kext to repair device hot plug**，
* 移除不必要启动文件

### 2019-10-03
~~* 增加一个1.6版本的bios 已更改为苹果启动logo 可直接刷入 参考[修改教程](https://www.bilibili.com/read/cv2788822/)~~

# Optimization tutorial

### Emulated NVRAM
So this section is for those who don’t have native NVRAM, Hardware to have incompatible native NVRAM with macOS are the Z390-300 series chipsets:
* B360
* B365
* H310
* H370
* Q370
* Z390


#### Making the nvram.plist

Outlay’s to making a NVRAM.plist file, Requires the following:

Change these settings within the config.plist:

##### Booter Section

* `DisableVariableWrite`: set to `YES` NVRAM Section
* `LegacyEnable`: set to `YES`
* `LegacySchema`: NVRAM variables set and injected into OpenCore and compares these variables present in nvram.plist **Security Section**
* `ExposeSensitiveData`: set to `0x3` (Which allows all data exposure)

##### And within your EFI:

* FwRuntimeServices.efi (Needed for sleep, wake and shutdown and other services to work correctly (Goes in the EFI/OC/Drivers Folder)

##### Now grab the ‘LogoutHook.command’ and place it somewhere safe like within your user directory:

`/Users/(your username)/LogoutHook/LogoutHook.command`

##### Open up terminal and run the following:

`sudo defaults write com.apple.loginwindow LogoutHook /Users/(your username)/LogoutHook/LogoutHook.command`

##### Now you have emulated NVRAM, Just to note that for macOS to support the -x flag and work correctly which is unavailable on 10.12 and below. nvram.mojave fixes this by injecting it instead of the system based one.

## BIOS Setting

Advanced \ Chipset Configuration → Vt-d : Disabled

Advanced \ Super IO Configuration → Serial Port: Disabled

Advanced \ USB Configuration → XHCI Hand-off : Enabled

Advanced \ Chipset Configuration → Share Memory : 128MB

Advanced \ Chipset Configuration → IGPU Multi-Monitor : Enabled


# Reference
[精解OpenCore](https://blog.daliansky.net/OpenCore-BootLoader.html)

[macOS Catalina 10.15安装中常见的问题及解决方法](https://blog.daliansky.net/Common-problems-and-solutions-in-macOS-Catalina-10.15-installation.html)

[使用HIDPI解决睡眠唤醒黑屏、花屏及连接外部显示器的正确姿势](https://blog.daliansky.net/Use-HIDPI-to-solve-sleep-wake-up-black-screen,-Huaping-and-connect-the-external-monitor-the-correct-posture.html)

[OpenCore部件补丁](https://github.com/daliansky/OC-little)


# Thank
**[daliansky](https://github.com/daliansky)（黑果小兵）**

**[RehabMan](https://bitbucket.org/RehabMan/)**

**[ZeRo° Xu](https://github.com/xzhih)(冰水加劲Q)**

**[acidanthera](https://github.com/acidanthera/OpenCorePkg)**

**[Bat.bat](https://github.com/williambj1)**
