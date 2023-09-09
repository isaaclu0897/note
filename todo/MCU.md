
### 什麽是MCU？

MCU, Micro Controller Unit 也被叫做 MC, UC, μC。MCU 將運算單元(PU)、輸出入單元(GPIO)、輔助控制單元(Timer, UART, I2C, SPI, ADC等)及記憶體(Flash, SRAM, EEPROM)整合在同一顆晶片上。相當於把一台電腦塞進一個晶片中，故早期亦將MCU稱為「微電腦晶片」。更有許多廠商把無線通訊部份（如WiFi, BlueTooth, Zeebee, 4G, 5G等）加入其中。

和微處理器不同要注意！應該吧

> ## 微型處理器和微型控制器有何區別？
> 微型處理器和微型控制器是電子裝置的內部元件。微型處理器是 CPU 內部非常小的處理單元。它是電腦晶片上的單一積體電路，可對數位訊號執行各種算術和邏輯功能。數十個微型處理器在高效能伺服器內共同運作，以進行資料處理和分析。
> 另一方面，微型控制器是洗衣機和恆溫器等智慧型電子裝置中的基本運算單元。它是一部非常小型的電腦，擁有自己的 RAM、ROM 和 I/O 系統，全部內嵌於單一晶片上。它可處理數位訊號並回應使用者輸入，但其運算能力受到限制。

### 爲什麽要MCU？

MCU的優點是體積小、價格便宜（視功能配置，約US$ 0.5 ~ 20）、功耗極低(mW等級)可使用電池供電、功能強大，從4bit到32bit都有，容易開發，有非常完整的工具鏈(Tool Chain)及生態體系(Ecosystem)，連中小學生在玩的Micro:bit, Arduino開發板都屬於MCU的範圍。但缺點是系統架構種類及供應商太多，沒有統一的開發工具。

另外受限價格因素，通常工作時脈不高（MHz等級），程式及記憶體區域都很小（KByte等級，少數能到MByte），不利大量運算，通常也沒有作業系統，僅有少數像Arm Mbed, RTOS能運行在較高階的MCU上。所以開發出來的程式就很難像手機上的APP一樣可以任意運行在不同硬體的手機上。

### MCU有哪些分類

而MCU依不同屬性有不同的分類方式，如Fig. 6-1所示。以下就根據不同屬性作一簡單說明。

依「**工作用途**」可分為使用者可完全使用全部資源的「通用型MCU」，和有特定用途，僅需少量程式碼或完全不需使用者程式的「專用型MCU」，當然也有兩者混合的類型，端看面對的市場而定。

依「**處理器結構**」可分為馮紐曼結構(von Neumann architecture, 或譯為馮．諾依曼）和哈佛結構(Harvard architecture)，前者中央處理器和儲存裝置分開且程式和資料儲存在同一個記憶體中，指令和資料不能同時存取，而後者的程式和資料則分開存放在不同的記憶體中，存取時各自有匯流排(Bus)，可於同一週期中運行，處理速度較快。

依「**指令集家族**」又可分為複雜指令集(Complex Instruction Set Computer, CISC)和精簡指令集(Reduced Instruction Set Computer, RISC)，前者主要代表有Intel 8051系列，而後者常見代表則有Arm Cortex-M, RISC-V, Atmel AVR, Microchip PIC, TI MSP430等系列，後者有指令工作週期短及省電優勢，因此目前在MCU領域RISC已逐漸取CISC。

依「**指令寬度**」可分為4/8/16/32 bit，部份廠商亦有依不同需求而採混合指令寬度，如Arm Cortex-M就有採用Thumb-1(16bit)和Thumb-2(32bit)的作法。

依「**程式記憶體**」可分為不帶（外掛）程式記憶體，由半導體廠直接光罩(MASK)製作(俗稱Read-Only Memory, ROM)，使用者可一次燒錄的(One Time Programmable ROM, OTPROM)，可重覆燒錄的紫外線抹除式可複寫唯讀記憶體(Erasable Programmable ROM, EPROM)或電子抹除式可複寫唯讀記憶體(Electrically-Erasable Programmable ROM, EEPROM)或NOR型快閃記憶體(Flash ROM)。而常用於記憶卡的NAND Flash雖然儲存容量很大，但由於存放資料不連續，難以直接用來儲存程式碼，如一定要用（如導入作業系統），則通常需要搭配大量的隨機記憶體（如SRAM, DRAM, DDR等）來使程式能連續存放於記憶體中。

### MCU有哪些型號？

### Reference

https://omnixri.blogspot.com/2021/09/aiottinymlmcu.html
https://ithelp.ithome.com.tw/articles/10267487
https://en.wikipedia.org/wiki/Microcontroller
https://zh.wikipedia.org/wiki/%E5%8D%95%E7%89%87%E6%9C%BA
https://aws.amazon.com/tw/compare/the-difference-between-microprocessors-microcontrollers/