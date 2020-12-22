# Ausu-ROG-Strix-B360i-UHD630-OPENCORE-EFI

## EFI 介绍
此 EFI 使用`MacMini8,1`机型，华硕 B360i 的绝大部分核显用户可通过修改使用(没有独显），默认启用全部 USB 端口，[OpenCore](https://github.com/acidanthera/OpenCorePkg) 版本：0.6.4 [Mac版本](https://www.apple.com.cn/macos/big-sur/): Big Sur 11.1<br>
<br>
![关于本机](https://github.com/NEEPUCS/Ausu-ROG-Strix-B360i-HACKINTOSH-OPENCORE-EFI/blob/master/images/about.png)

### 我的配置

|         硬件       |                   型号                     | 
|-------------------:|:------------------------------------------|
|               主板 | 华硕 ROG Strix B360i Gaming                   |
|             处理器 | 英特尔酷睿 i5-8400K                            |
|               显卡 | Intel UHD Graphics 630                       |
|               硬盘 | 西部数据 Black 3D NVMe WDS250G2X0C 256GB                          |
|               内存 | 十铨（Team Group） 8GB DDR4 2666MHz x 2       |
|        无线 + 蓝牙 |  Broadcom 94360CS2拆机卡 + 转接带（替换板载网卡时，发现此款网卡长，所以使用转接带，将网卡放在机甲壳内，巧妙的是，我将WIFI天线放至于机箱背侧）|
|  机箱 + 电源 + 散热 | 迎广肖邦 + 自带150W电源（多次替换电源风扇，只为噪音较小的电源散热风扇）+ 猫头鹰（NOCTUA）NH-L9i CPU散热器 |
|             显示器 | DELL U2417H 23.5英寸(1920 × 1080)                |
|               键盘 | Ikbc（有线红轴）                 |
|               鼠标 | 罗技 Logitech Go Pro Wireless |

### 兼容的配置

|         硬件       |                              型号                           | 
|-------------------:|:------------------------------------------------------------|
|               主板 | 华硕 B360                                 |
|             处理器 | 英特尔第 8 代、第 9 代酷睿处理器（推荐拥有核显的版本）                |
|               显卡 | 
|               硬盘 | 除了几个特例（如三星 PM981, 970EvoPlus），基本都可以                            |
|               内存 | 除了非常差的，基本都可以                                        |
|        无线 + 蓝牙 | 黑苹果免驱版无线 + 蓝牙 PCI-E 网卡都可以                          |
|     摄像头 + 麦克风 | 免驱版都可以                                             |
|  机箱 + 电源 + 风扇 | 根据个人喜好和 CPU、显卡的功率来决定                               |
|             显示器 | 根据个人喜好选择（推荐 4K 分辨率）                                |
|  键盘 + 鼠标 + 音箱 | 根据个人喜好选择                                                |
|           其它外设 | 根据个人喜好选配                                              |

## 更新记录
- 2020.12.22 更新了HDMI显示输出问题(使用Hackintool应用预设补丁，同时修复了热插拔问题(boot-args 添加 igfxonln=1)）
----
- 2020.12.21 经过测试和两天时间的使用，上传第一版
## 硬件杂谈
关于主板如何更换板载网卡可自行搜索B站，将网线内置于机箱后面本该放置HDD 2.5的位置，并用胶带固定，走线可以通过CPU供电上方的走线口。


## BIOS 设置
CFGLock - Disabled

VT-d - Disabled

大于4G地址空间解码 - Enabled

Systemtime and Alarm Source - Legacy RTC

SATA模式选择 - AHCI （必须设置）

legacyUSB支持 - Enabled

XHCIHand-off - Enabled

快速启动 - Disabled

开启CSM - Disabled

安全启动状态 - Disabled

操作系统类型 - 其他操作系统

Intel 虚拟化技术 - Enabled


## ACPI
- PLUG-XCPM(代替SSDT-PLUG用于电源管理 参见http://vlambda.com/wz_7iqf7rYdpoC.html)
- SSDT-AWAC 
- SSDT-EC-USBX
- SSDT-no-EC
- SSDT-PM
- SSDT-PMC
- SSDT-UIAC

## Drivers
- HfsPlus.efi(必须)
- OpenCanopy.efi
- OpenRuntime.efi(必须)
## Kexts
**Lilu.kext** 插件 必装

| 设备      |              | kext                                                         |
| --------- | ------------ | ------------------------------------------------------------ |
| 显卡      | UHD630       | WhateverGreen.kext                                           |
| 有线网卡  | Intel® I219V | IntelMausi.kext                                              |
| 声卡      | S1220a       | AppleALC.kext                                                |
| USB       | 按需定制     | XHCI-unsupported.kext USBInjectAll.kext |
| Wi-Fi     | Broadcom 94360CS2      | AirportBrcmFixup.kext                                        |
| 蓝牙      |       |  |
| SMBus设备 |              | VirtualSMC.kext SMCProcessor.kext SMCSuperIO.kext            |
|固态硬盘|SN720 256G |NVMeFix.kext(不加没问题，官网建议)


## 其他设置

HideAuxiliay - Enabled

boot-args String brcmfx-country=CN(修改网卡的国家地区代码为CN) igfxfw=2(核显用户) -v(啰嗦模式)

AirPortBrcm4360_Injector.kext - MaxKernal -> 19.9.9

禁止Apple固件更新 - Enabled

## 基本使用(从[GeQ1an](https://github.com/GeQ1an/MSI-B360M-MORTAR-HACKINTOSH-OPENCORE-EFI)复制，本EFI的PCI参数是我使用的，如果不行，请删掉并重新配置)
准备 [ProperTree](https://github.com/corpnewt/ProperTree) 编辑配置文件，尽量避免使用其他编辑器。
OpenCore 拥有高度的可定制化，建议先参考下面的说明使用配置好的基础版本，之后再通过 [daliansky](https://github.com/daliansky) ([黑果小兵的博客](https://blog.daliansky.net/)) 和 [xjn](https://blog.xjn819.com/) 学习更多内容进行修改。

0.依照上面的BIOS设置，对电脑BIOS设置完成

1.填入Macmini8,1机型的三码 + ROM 信息到/EFI/OC/config.plist文件 PlatformInfo > Generic 处，并将机型修改为Macmini8,1。

2.修改/EFI/OC/config.plist文件 DeviceProperties > Add > PciRoot(0x0)/Pci(0x2,0x0) 下 AAPL,ig-platform-id 参数为07009b3e，并新增 framebuffer-unifiedmem 参数为00000080。
## 正常工作
***12.21更新  当前置USB口被U盘等占用时，无线网络就会连不上或者没流量，暂时没有解决方法***
- [x] 声卡（板载）/ 网卡（板载）
- [x] 显卡（核显）/ 硬解 4K（H.264）
- [x] WiFi（PCI-E 设备） / 蓝牙（PEI-E 载 USB 设备）
- [x] 隔空投送 / 接力 / 随航
- [x] FaceTime(没摄像头) / iMessage
- [x] Apple Music
- [x] 睿频 / 原生电源管理
- [x] 睡眠 / 键盘、鼠标唤醒

[截图] (https://github.com/NEEPUCS/Ausu-ROG-Strix-B360i-HACKINTOSH-OPENCORE-EFI/tree/master/images)

## 进阶使用
1. 参考 [xjn 博客](https://blog.xjn819.com/?p=543) 的进阶部分「4.1 CPU 的变频优化」或 xjn 大佬发表于 PCbeta 的帖子 [FCPX 核显独显全程满速指南](http://bbs.pcbeta.com/viewthread-1836920-1-1.html) 中「HWP 变频」部分
2. 参考 [黑果小兵博客](https://blog.daliansky.net/Intel-FB-Patcher-USB-Custom-Video.html)


## 鸣谢
[daliansky](https://github.com/daliansky) ([黑果小兵](https://blog.daliansky.net/))<br>
[xjn](https://blog.xjn819.com/)<br>
[GeQ1an](https://github.com/GeQ1an/MSI-B360M-MORTAR-HACKINTOSH-OPENCORE-EFI)<br>

## 链接
OpenCorePkg [官方版本](https://github.com/acidanthera/OpenCorePkg/releases) [自动编译](https://github.com/williambj1/OpenCore-Factory/releases) / AppleSupportPkg [官方版本](https://github.com/acidanthera/AppleSupportPkg/releases) [自动编译](https://github.com/athlonreg/AppleSupportPkg-Factory/releases) / [MacInfoPkg](https://github.com/acidanthera/MacInfoPkg/releases) / [Lilu](https://github.com/acidanthera/Lilu/releases) / [AppleALC](https://github.com/acidanthera/AppleALC/releases) / [WhateverGreen](https://github.com/acidanthera/WhateverGreen/releases) / [IntelMausi](https://github.com/acidanthera/IntelMausi/releases) / [VirtualSMC](https://github.com/acidanthera/VirtualSMC/releases)  / [OcBinaryData](https://github.com/acidanthera/OcBinaryData) / [MaciASL](https://github.com/acidanthera/MaciASL/releases) / [ProperTree](https://github.com/corpnewt/ProperTree) / [Hackintool](https://www.tonymacx86.com/threads/release-hackintool-v2-8-6.254559/) 
## 关于这个项目
可以无限制的下载、使用、修改、分发、上传，不可用作商业用途。
## 关于我
本人Hack技术不精通，略懂OpenCore皮毛，最近装机时能感觉到黑苹果配置的难度，一方面，希望能够帮助大家解决难题，另一方面，希望各位大佬能优化我的EFI，使其更完善；同时，如果仓库文件有错误烦请各位大佬指正。