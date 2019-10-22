# ASRock-Z390-Phantom-ITX-OpenCore-Hackintosh
`交流群942593633`
### [English](README.md) | [中文](README-zh.md)

## 配置

主板：华擎z390 phantom gaming-itx/ac

cpu：i7 9700k

显卡：AMD 蓝宝石 rx480

网卡：BCM943602CS

## 驱动情况
* 系统稳定性：未出现系统崩溃情况，系统已升级10.15.1 Beta2(19B77a)

* 显卡：独立显卡驱动正常，核显可满载1.2Ghz

* 声卡：驱动正常，本人使用情况不多

* wifi、蓝牙、隔空投送、ipad随航等功能正常

* 睡眠唤醒：经一个月测试，需关闭电能电能小憩进行手动睡眠，开启可自动进入睡眠，

    但会半小时自动唤醒后无法再次自动进入睡眠
    
![QQ20191013-105901](http://github.fangf.cc/mweb/QQ20191013-105901.png)


* nvram：可以正常生成nvram.plst文件，但启动没有进行读取，等OpenCore官方修复。

    为什么纠结nvram。因为官方描述可实现如同白果一样的指定磁盘进行默认启动，
    
    以及保证其他功能重启后不丢失，例如查找我的设备
    
![QQ20191013-112532](http://github.fangf.cc/mweb/QQ20191013-112532.png)

* usb：主板及机箱面板全端口驱动、唤醒无磁盘推出情况

* type-c：需开机前插入设备、可实现热插拔

![QQ20191013-112335](http://github.fangf.cc/mweb/QQ20191013-112335.png)






# 更新日志

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


# 优化教程

### 开启模拟nvram教程
这个部分是给那些没有原生nvram的用户，最常见的与macos不兼容的本机nvram硬件是非z370 300系列芯片组：
* B360
* B365
* H310
* H370
* Q370
* Z390


#### 制作nvram.plist

要制作一个nvram.plist，您需要如下设置：

在你的config.plist里
* `DisableVariableWrite`: 设置成 YES

* `LegacyEnable`: 设置成  YES

* `LegacySchema`: nvram变量集（opencore将这些变量与nvram.plist中的变量进行比较）

* `ExposeSensitiveData`: 设置成3


把“logouthook.command”放到正确的位置：

`/Users/(your username)/LogoutHook/LogoutHook.command`

打开终端并运行一下命令

`sudo defaults write com.apple.loginwindow LogoutHook /Users/(your username)/LogoutHook/LogoutHook.command`

重启两次电脑，你就可以看到在EFI分区根目录生成的nvram.plist文件


## OC-引导扫描策略

- 设置位置：`Misc\Security\ScanPolicy`

- **定义：**

  （01）0x00000001 — 限定为文件系统，由以下`允许扫描文件系统子项`开启

  （02）0x00000002 — 限定为设备类型，由以下`允许扫描设备类型子项`开启

  ​	`允许扫描文件系统子项`：

  （03）0x00000100 — 允许扫描APFS文件系统

  （04）0x00000200 — 允许扫描HFS文件系统

  （05）0x00000400 — 允许扫描EFI系统分区文件系统

  ​	`允许扫描设备类型子项`：

  （06）0x00010000 — 允许扫描SATA设备

  （07）0x00020000 — 允许扫描SAS和Mac NVMe设备

  （08）0x00040000 — 允许扫描SCSI设备

  （09）0x00080000 — 允许扫描NVMe设备

  （10）0x00100000 — 允许扫描CD / DVD设备

  （11）0x00200000 — 允许扫描USB设备

  （12）0x00400000 — 允许扫描FireWire设备

  （13）0x00800000 — 允许扫描读卡器设备

  `扫描策略数值`=（01）+（02）+1个或数个`允许扫描文件系统子项`+1个或数个`允许扫描设备类型子项`

  例如：希望扫描对象是APFS文件系统的USB设备，`扫描策略数值`=（01）+（02）+（03）+（11），经16进制加法计算得出，`扫描策略数值`=`0x200103`。

  `注意`，使用时需将16进制转换为10进制。示例最终`扫描策略数值`=`2097411`

- 几种扫描策略

  - `F0103` —官方推荐值：（01）+（02）+（03）+（06）+（07）+（08）+（09）
  
    最终`扫描策略数值` = `983299`
  
  - `0`—允许扫描所有已知文件系统+允许扫描所有已知设备类型。
  
  - `2F0303` —官方推荐值+允许扫描HFS文件系统+允许扫描USB设备
  
    最终`扫描策略数值` = `3080963`
    
## OC-引导多系统

- 设置位置：`Misc\Entries`

- 定义启动项

  - `Comment`：一个有意义的名称。
  - `Enabled`：允许开关。
  - `Name`：引导时显示的名称。
  - `Path`：被引导系统的绝对路径。

- 示例：

  按照`定义启动项`的格式要求填写所有内容。其中`path`格式像这样：

  示例1：

  ```
  PciRoot(0x0)/Pci(0x14,0x0)/USB(0xE,0x0)/HD(1,GPT,FBAB0AB8-698F-11E9-8DC7-93AD5ED2C040,0x800,0x1A716B)/\EFI\BOOT\BOOTX64.EFI
  
  PciRoot(0x0)/Pci(0x17,0x0)/Sata(0x1,0xFFFF,0x0)/HD(1,GPT,B3DC0CC3-5F77-4E95-A41C-5E6EE4687BC3,0x28,0x64000)/\EFI\BOOT\BOOTX64.EFI
  PciRoot(0x0)/Pci(0x17,0x0)/Sata(0x0,0xFFFF,0x0)/HD(1,GPT,987AF4BE-FCB5-4CA3-A719-B3D798E95FF0,0x28,0x64000)/\EFI\BOOT\BOOTX64.EFI
  
  ```

  示例2：

  ```
  PciRoot(0x0)/Pci(0x1D,0x0)/Pci(0x0,0x0)/NVMe(0x1,00-00-00-00-00-00-00-00)/HD(1,GPT,8763DD59-B7D6-4734-9B01-D7BCD42ECDDA,0x800,0x96000)/\EFI\Microsoft\Boot\bootmgfw.efi
  ```

  示例1为移动硬盘的Windows系统的绝对路径（自带EFI，可引导）。

  示例2为驱动器不同分区的Windows系统的绝对路径。`Microsoft`是可引导windows的文件夹。

- 获取`path`的方法

  - 终端确认启动分区的UUID

    终端输入`diskutil list`，确认启动分区硬盘标识符，如：`disk2s1`。

    终端输入`diskutil info disk2s1`进一步确认`启动分区的UUID`，如：

    ```
    ......
    Disk / Partition UUID:     FBAB0AB8-698F-11E9-8DC7-93AD5ED2C040
    ......
    ```

  - 获得完整的`path`

    - 安装`NOOPT`或者`DEBUG`版本的`OpenCore`（BOOTx64.ef`和OpenCore.efi）。
    - [下载地址](https://github.com/acidanthera/OpenCorePkg/releases)
    - 设置Debug选项，提取日志文件：EFI根目录\opencore-YYYY-MM-DD-HHMMSS.txt。
      - `Misc\Debug\DisableWatchDog`=`true`
      - `Misc\Debug\Target`=`65`
    - 打开opencore-YYYY-MM-DD-HHMMSS.txt文件，搜索前文已经确认的`启动分区的UUID`。
    - 参考示例获得完整的`path`。

- 注：Clover , Grub 等其他系统可以参照上述示例添加引导项目，达成以OC为主的多系统引导管理器。


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
