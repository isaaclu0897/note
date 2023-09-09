Top keyword in BMC - Continually updated⭐
===

###### tags: `keyword` `BMC`

[TOC]

### BMC 是xxx

第一次玩這麽底層

突然就卯起來玩

爲了避免英文詞不達意，這裏會使用中文，也是爲了快速學習。


### What can tao do? What problem does it resolve?
管理主板、電源...


### Keywords

#### BMC Keywords

* [[SoC]]
* arm
* bmc
* 硬體
* 韌體
* 軟體
* [[MCU]]，單晶片、單片機
    * STM32
    * Arduino
* yocto
* bitbake
* qume
* aspeed
* ami
* ast2400
* flash memory spi
* 嵌入式Linux
* uboot
* kernel
* roofs
* spi，貌似是一種通訊界面，可能會將晶片的spi脚位來出來，讓焊接好的板子可以直接燒錄
* openbmc
* 

### 情景

1. 新的晶片進來怎麼確認是好的
2. 每次重新寫程式都要重燒嗎
3. 編譯過程要很久可以怎麼解決
4. source code那麼大，編譯後為什麼變那麼小
5. 不同的架構編譯的執行檔可以互相執行嗎
6. ast的晶片沒有外接的觸點是怎麽燒錄的使用轉接板嗎
7. 貌似可以將晶片的spi接口拉出來，然後用夾頭燒入，需要被確認
8. 其他的單晶片是怎麽燒入的？

這個arduino的英文教學不錯
https://www.adeept.com/learn/tutorial-46.html
https://www.adeept.com/learn/tutorial-45.html

https://zhuanlan.zhihu.com/p/352944001

https://www.zhihu.com/question/405534552/answer/1801068074 閲讀中

https://zhuanlan.zhihu.com/p/647290967
> 这里顺便再提一句，学硬件的技巧：先看结果，再倒推理论！
> 以前我们学习，都是先学理论，再用理论去实践，最后发现，卧槽，怎么跟书上教的不一样？
> 硬件有时候是玄学，我一般喜欢用结果去倒推理论，直到能理论和结果匹配为止。
作者說，搞嵌入式不用全懂硬件，看懂就可以了！
先有結果在推導，TMD軟體也是一樣啊！

https://mp.weixin.qq.com/s/FjSZFePafq7BgVB5D_Vhag
按鈕還有要消除抖動的！很酷。反正總結來説就是消除雜訊就對了，文章有提供硬體消除的方式

來自chatgpt的回答：
> 1. BMC（Baseboard Management Controller）：
> * BMC是一种独立的微控制器或芯片，嵌入在服务器、网络设备等硬件中，用于管理和监控系统的各种硬件和管理任务。
> * BMC内部包含一个微处理器（Microprocessor），用于执行硬件管理和监控任务。
> * 微处理器與處理器相似，一個是大型的，一個是小型的。

> 4. Raspberry Pi和BMC的区别：
> * Raspberry Pi是一系列低成本、高性能的单板计算机，通常运行基于Linux的操作系统。
> * BMC是专用的微控制器，用于管理和监控服务器和硬件设备，通常运行特定的嵌入式操作系统。


由於單晶片沒有OS，他們的編程會比較多事件驱动或循环执行。

到這裏fireware開發有了新的認識，應該説要與這些晶片打交道的行爲都可以叫做fireware開發。

https://hkgoldenmra.blogspot.com/2020/02/bootloader-atmega328p.html

乾！看半天嵌入式Linux又跟stm32這些東西不一樣，只能說還有其他系統在處理，stm32都是嵌入式裏面的其中一個東西而已。

經典 嵌入式Linux和stm32区别? 之间有什么关系吗？

https://zhuanlan.zhihu.com/p/502470016
https://www.zhihu.com/question/53880054

入門：可以將openBMC編譯好，燒錄到晶片中，並修改或添加代碼
進階：知道晶片脚位，根據脚位除錯、設計、或是與其他系統對接
重新開始：嘗試與其他系統對接例如bios、感測器等

https://www.servethehome.com/explaining-the-baseboard-management-controller-or-bmc-in-servers/

BMC 工具介紹
https://nosleep.pixnet.net/blog/post/224531871-%E7%A8%8B%E5%BC%8F%E9%96%8B%E7%99%BC-%7C-%5Bfirmware%5D%5Bbmc%5D-server-bmc%E9%96%8B%E7%99%BC-%7C-%E9%9F%8C%E9%AB%94%E5%B7%A5

CH340好像是一種晶片，這個網友推薦他，之前好像有看過這個晶片不需要驅動
USB 轉TTL(CH340)
USB 轉DB9(CH340)

https://developer.aliyun.com/article/244170

嵌入式的几种固件烧录方式
https://zhuanlan.zhihu.com/p/57519145
> 固件其实就是放在存储介质上的数据，当嵌入式板子启动时，能够从特定的位置找到这些文件，使得板子能够跑起来，这些文件就是固件。那么在嵌入式linux系统中，经常用到的文件如下：

uboot：如uboot.bin
kernel：如uImage
rootfs：如system.yaffs2文件
1.2 什么是烧录？
烧录的意思是将一些嵌入式启动所必须的硬件下载到嵌入式的储存设备中，这可能是norflash， 有可能是nandflash，也有可能是SD卡。

板子启动后，可以利用mount命令，将某一目录挂载到PC机上。 -> 這個感覺很實用，要瞭解一下

给X470D4U安装OpenBMC
https://zhuanlan.zhihu.com/p/444180167

qemu仿真
https://www.cnblogs.com/zl-yang/p/16324367.html

openbmc开发--＞aspeed--＞slave-i2c[ast2400]
https://blog.csdn.net/qq_41571052/article/details/113313133

Build A Raspberry Pi BMC
https://www.boniface.me/a-raspberry-pi-bmc/

openbmc开发5
https://masterhu.blog.csdn.net/
https://blog.csdn.net/qq_34160841/article/details/115430387

OpenBMC
https://blog.csdn.net/datapad/category_11536494.html
https://blog.csdn.net/Datapad/article/details/121859922

添加新系统到 OpenBMC 实践
https://www.cnblogs.com/arvin-blog/p/15664537.html

添加新系统到 OpenBMC
https://www.cnblogs.com/arvin-blog/p/15663921.html

start-qemu-session
https://github.com/openbmc/docs/blob/master/development/dev-environment.md#download-and-start-qemu-session

qemu-system-arm安装和基本使用
https://zhuanlan.zhihu.com/p/622572068

OpenBMC开发4：启动编译的镜像
https://blog.csdn.net/qq_34160841/article/details/104951547

qemu arm aspeed
https://www.qemu.org/docs/master/system/arm/aspeed.html

openbmc palmetto
https://jenkins.openbmc.org/view/latest/job/latest-master/label=docker-builder,target=palmetto/lastSuccessfulBuild/artifact/openbmc/build/tmp/deploy/images/palmetto/

一步步教你：如何用Qemu来模拟ARM系统
https://zhuanlan.zhihu.com/p/340362172

https://blog.csdn.net/qq_34160841/article/details/119977726

https://ithelp.ithome.com.tw/m/articles/10235889

https://ithelp.ithome.com.tw/m/articles/10264112


