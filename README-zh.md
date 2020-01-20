# ASRock-Z390-Phantom-ITX-OpenCore-Hackintosh
`交流群942593633`
### [English](README.md) | [中文](README-zh.md)

## 配置

主板：华擎z390 phantom gaming-itx/ac

cpu：i7 9700k

显卡：~~AMD 蓝宝石 rx480~~ RX5500 itx

网卡：BCM943602CS

## 驱动情况
* 系统稳定性：未出现系统崩溃情况，系统已升级10.15.1 Beta2(19B77a)

* 显卡：独立显卡驱动正常，核显可满载1.2Ghz

* 声卡：驱动正常，本人使用情况不多

* wifi、蓝牙、隔空投送、ipad随航等功能正常

* 睡眠唤醒：完美

* 原生nvram


    
![QQ20191013-112532](http://github.fangf.cc/mweb/QQ20191013-112532.png)

* usb：主板及机箱面板全端口驱动、唤醒无磁盘推出情况

* type-c：需开机前插入设备、可实现热插拔

![QQ20191013-112335](http://github.fangf.cc/mweb/QQ20191013-112335.png)






# 更新日志

### 2019-01-20

* 开启原生nvram支持
* 驱动日常更新

### 2019-12-25

* OpenCore&kext等文件更新到最新版本
* 重新加入usbport 修复usb充电电流及type-c接口
* 重新加入ssdt-APMC、节能中显示断电后自动重启（无实际意义）
* 修改扫描策略，默认不扫描win

### 2019-12-25

* 显卡更换成amd rx5500 itx


### 2019-11-07

* 同步更新OpenCore、Kext驱动更新
* 删除PM、USB定制

### 2019-10-18

* 同步更新OpenCore以及kext

* 添加博通网卡驱动，需要手动开启
![](http://github.fangf.cc/mweb/15717383021286.png)


### 2019-10-17

* 重新仿冒EC，之前的方式出现错误

* 同步更新官方Opencore

* 移除apfs.efi(仅fusiondrive需要)

* 添加usb定制全端口版本需手动切换

* ![](http://github.fangf.cc/mweb/15712818344299.jpg)


### 2019-10-13

* 同步更新官方OpenCore v0.5.2 10.13内容

* 睡眠非常稳了

    输出最近一次睡眠时间`sysctl -a |grep sleeptime`
    
    输出最近一次唤醒时间`sysctl -a |grep waketime`

![A78F9F5414D437EC1FF6FD74E1CF0E64](http://github.fangf.cc/mweb/A78F9F5414D437EC1FF6FD74E1CF0E64.jpg)


### 2019-10-09

* 更改扫描策略，默认引导 Macintosh HD 直接进入 MacOS 系统

* 手动添加win引导，需修改引导路径为自己的（Misc-Entries-Path）

### 2019-10-04

* 启动文件config优化设置 [参考](https://insanelymacdiscord.github.io/Getting-Started-With-OpenCore/)

* **加入IOElectrify.kext修复雷电热插拔**，占用HS1 HS3端口，实际不影响该端口设备使用

* 移除不必要启动文件




## BIOS设置

Advanced \ Chipset Configuration → Vt-d : Disabled

Advanced \ Super IO Configuration → Serial Port: Disabled

Advanced \ USB Configuration → XHCI Hand-off : Enabled

Advanced \ Chipset Configuration → Share Memory : 128MB

Advanced \ Chipset Configuration → IGPU Multi-Monitor : Enabled


# 参考
[精解OpenCore](https://blog.daliansky.net/OpenCore-BootLoader.html)

[macOS Catalina 10.15安装中常见的问题及解决方法](https://blog.daliansky.net/Common-problems-and-solutions-in-macOS-Catalina-10.15-installation.html)

[使用HIDPI解决睡眠唤醒黑屏、花屏及连接外部显示器的正确姿势](https://blog.daliansky.net/Use-HIDPI-to-solve-sleep-wake-up-black-screen,-Huaping-and-connect-the-external-monitor-the-correct-posture.html)

[OpenCore部件补丁](https://github.com/daliansky/OC-little)


# 感谢
**[daliansky](https://github.com/daliansky)（黑果小兵）**

**[RehabMan](https://bitbucket.org/RehabMan/)**

**[ZeRo° Xu](https://github.com/xzhih)(冰水加劲Q)**

**[acidanthera](https://github.com/acidanthera/OpenCorePkg)**

**[Bat.bat](https://github.com/williambj1)**
