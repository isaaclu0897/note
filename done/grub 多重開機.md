#ubuntu , #grub, #bios, #gpt, #uefi, #多重開機

[TOC]

一直以來都想要使用UEFI+GPT格式開機，

優點：
* GPT格式可以突破4個主要磁區的限制
* UEFI開機好像比較快

### 最終系統配置
![|500](../../attachments/grub%20多重開機.png)

### 系統配置說明

![|500](../../attachments/grub%20多重開機-1.png)

主要分成三個作業系統
* Ubuntu - 1 ： 平常作業使用
* Windows 10 ： 爲了辦公作業使用
* Ubuntu - 2 ： 電腦救援使用(常常會改系統配置導致整臺電腦被我搞掛，所以多加這個救援系統)

其實個人完全沒有使用到Windows，不過因爲辦公環境需要，加減還是裝一下。有時候也真的會需要用到Windows的，像是開發PLC、HMI這種工控產品。



![|500](../../attachments/grub%20多重開機-2.png)

這裡有個安裝上的重點要注意，因爲是先裝了兩個Ubuntu，才裝的Windows，所以在安裝Windows的時候，他會報這個錯誤`windows 無法安裝到選取的位置 0x80300024`。一開始其實挺懵的...完全搞不清楚爲啥不能安裝。

後來從本質上去想，因爲Windows的架構關係，在安裝的時候他只認得自己的作業系統，只要有其他EFI分區，便會導致安裝無法辨識...還真是挺霸道的設計呢...Linux就不會這樣。

OKey，反正在安裝Windows前，用Gparted把EFI分區調整掉就可以了，最後安裝完畢，系統只會進入Windows，再透過Ubuntu的LiveCD，將grub安裝進去即可
![|500](../../attachments/grub%20多重開機-3.png)



開機啓動程序筆記

主要分成兩種機制MBR、UEFI

MBR(Master Boot Record, 主引導記錄)
有一个441字节大小的区域,BIOS在开机自检(Power-On Self-Test,以下简称POST)之后加载其中的内容。然而因为空间太小,无法容纳引导装载程序,所以需要额外的空间,从而就引入了多场景引导装载程序(multi-stage boot loader)。一开始MBR加载引导装载程序的其余部分,通常是在MBR和第一个分区之间。当然,这样做并不安全,因为里面的代码任何人都可以修改

UEFI(Unified Extensible Firmware Interface, 統一可延伸韌體介面)

GPT通常和UEFI一起使用,而不是BIOS

### GRUB工作原理

GRUB是一個獨立的系统。它能够读取文件系统，加载配置文件(grub.cfg)以及其他需要的模块。

GRUB自带一个叫作 grub-install 的工具(注意不要和Ubuntu的 install-grub 混
淆),它负责大部分的GRUB文件安装和配置工作。

GRUB安装不正确可能会让系统的启动顺序失效,所以请小心操作。最好是了解一下如
何使用 dd 来备份MBR,并且备份其他已经安装了的GRUB目录,最后确保你有一个应急
启动计划。

1. BIOS或者固件初始化硬件,在启动存储设备上寻找启动代码。
2. BIOS和固件运行找到的启动代码,开始GRUB。
3. 加载GRUB核心。
4. 初始化GRUB核心,此时GRUB可以读取磁盘和文件系统。
5. GRUB识别启动分区,在那里加载配置信息。
6. GRUB为用户提供一个更改配置的机会。
7. 超时或者用户完成操作以后,GRUB执行配置(执行顺序在5.5.2节有介绍)。
8. 执行过程当中,GRUB可能会在启动分区中加载额外的代码(模块)。
9. GRUB执行 boot 命令,以加载和执行配置信息中 linux 命令指定的内核。

實驗在usb或是存儲裝置上搭建grub系統
