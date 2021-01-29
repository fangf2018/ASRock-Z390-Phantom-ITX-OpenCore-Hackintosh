# ASRock-Z390-Phantom-ITX-OpenCore-Hackintosh

### [English](README.md) | [中文](README-zh.md)

## Configuration

Motherboard：ASRockz390 phantom gaming-itx/ac

cpu：i7 9700k

Graphics： AMD RX5500 itx

Wireless network card：BCM943602CS

![](http://github.fangf.cc/mweb/15934410276957.jpg)


## Drive situation

* System stability：No system crashes，System has been update10.15.1 Beta2(19B77a)

* Graphics：RX5500 driver is normal，UHD630 working frequency 1.2Ghz
* Sound card：Normal drive
* wifi、Bluetooth、Handoff、Sidecar Normal use
* Sleep &wake：work well
* location：work well
* nvram：work well

      
![QQ20191013-112532](http://github.fangf.cc/mweb/QQ20191013-112532.png)
* usb：No abnormality

![QQ20191013-112335](http://github.fangf.cc/mweb/QQ20191013-112335.png)

* ~~type-c：Plug in the device before booting, hotplug~~
* TB3 ：hot-plug





# Update log


### 2020-05-18

* TB3 hotplug [Help](https://fangf.cc/2020/05/19/TB3/)

![](http://github.fangf.cc/mweb/15898151330755.jpg)

### 2020-01-20

* Turn on native NVRAM
* Update

### 2019-11-07

* update OpenCore、Kext
* delete ssdt-PM、usbport

### 2019-10-18

* Update OpenCore and kext

* Add BRCM network card driver

![](http://github.fangf.cc/mweb/15717383021286.png)

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
* Remove unnecessary startup files




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
