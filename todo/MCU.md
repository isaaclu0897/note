
### 什麽是MCU？

MCU, Micro Controller Unit 也被叫做 MC, UC, μC 是一種小型集成電路裝置，常用來控制各種電子產品或裝置的運行。

通常會集成一個或多個運算單元(PU)、輸出入單元(GPIO)、輔助控制單元(Timer, UART, I2C, SPI, ADC等)及記憶體(Flash, SRAM, EEPROM)在同一顆晶片上，使其能夠在嵌入式系統(Embedded Systems)中執行複雜的計算和控制任務。簡單的來説 MCU 相當於是把一台電腦主機板塞進一個晶片中。

由於物聯網的發展，目前有許多廠商也會把無線通訊部份（如WiFi, BlueTooth, Zeebee, 4G, 5G等）加入其中。

### 爲什麽要使用MCU？

MCU的優點是體積小、價格便宜、低功耗，可使用電池供電，容易開發，有非常完整的工具。但缺點是系統架構種類及供應商太多，沒有統一的開發工具。

優點：
1. 體積小
2. 低功耗，可以使用電池供電
3. 容易開發，由於設計簡單以及完整的工具鏈(Tool Chain)及生態體系(Ecosystem)
4. 價格便宜
缺點：
1. 工作時脈不高（MHz等級）
2. 程式及記憶體區域都很小（KByte等級，少數能到MByte）
3. 專為特定情境設計，程式難以跨平臺運用
4. 系統架構種類及供應商太多，沒有統一的開發工具

### MCU可以做什麽？

MCU常常被用於控制家用電子設備，如：微波爐、洗衣機、智能手機、汽車電子系統、工業自動化設備、醫療設備、無人機等等。它們可以根據預定的程式或指令來執行不同的任務，例如監控感測器數據、處理通信、控制馬達、執行演算法等。

### MCU有哪些分類

![](../../attachments/MCU.png)

MCU依不同屬性有不同的分類方式

依「**工作用途**」可分為使用者可完全使用全部資源的「通用型MCU」，和有特定用途，僅需少量程式碼或完全不需使用者程式的「專用型MCU」，當然也有兩者混合的類型，端看面對的市場而定。

依「**處理器結構**」可分為馮紐曼結構(von Neumann architecture, 或譯為馮．諾依曼）和哈佛結構(Harvard architecture)，前者中央處理器和儲存裝置分開且程式和資料儲存在同一個記憶體中，指令和資料不能同時存取，而後者的程式和資料則分開存放在不同的記憶體中，存取時各自有匯流排(Bus)，可於同一週期中運行，處理速度較快。

依「**指令集家族**」又可分為複雜指令集(Complex Instruction Set Computer, CISC)和精簡指令集(Reduced Instruction Set Computer, RISC)，前者主要代表有Intel 8051系列，而後者常見代表則有Arm Cortex-M, RISC-V, Atmel AVR, Microchip PIC, TI MSP430等系列，後者有指令工作週期短及省電優勢，因此目前在MCU領域RISC已逐漸取CISC。

依「**指令寬度**」可分為4/8/16/32 bit，部份廠商亦有依不同需求而採混合指令寬度，如Arm Cortex-M就有採用Thumb-1(16bit)和Thumb-2(32bit)的作法。

依「**程式記憶體**」可分為不帶（外掛）程式記憶體，由半導體廠直接光罩(MASK)製作(俗稱Read-Only Memory, ROM)，使用者可一次燒錄的(One Time Programmable ROM, OTPROM)，可重覆燒錄的紫外線抹除式可複寫唯讀記憶體(Erasable Programmable ROM, EPROM)或電子抹除式可複寫唯讀記憶體(Electrically-Erasable Programmable ROM, EEPROM)或NOR型快閃記憶體(Flash ROM)。而常用於記憶卡的NAND Flash雖然儲存容量很大，但由於存放資料不連續，難以直接用來儲存程式碼，如一定要用（如導入作業系統），則通常需要搭配大量的隨機記憶體（如SRAM, DRAM, DDR等）來使程式能連續存放於記憶體中。

### MCU有哪些型號？

### Reference

> [推薦閲讀 - 30天學會MCU](https://ithelp.ithome.com.tw/articles/10314190)
> [MCU的分類方式](https://ithelp.ithome.com.tw/articles/10267487)
> [什麽是MCU與產業現況](https://omnixri.blogspot.com/2021/09/aiottinymlmcu.html)
> 
> [Wiki - MCU - en](https://en.wikipedia.org/wiki/Microcontroller)
> [Wiki - MCU - zh](https://zh.wikipedia.org/wiki/%E5%8D%95%E7%89%87%E6%9C%BA)
> 
> [處理器的分類，CPU、GPU、MCU、DSP、MPU](https://www.stockfeel.com.tw/%E8%99%95%E7%90%86%E5%99%A8-cpu-gpu-mcu-dsp-mpu/)
> [微型處理器和微型控制器的差別](https://aws.amazon.com/tw/compare/the-difference-between-microprocessors-microcontrollers/)


---

與[[SoC]]不同


什麽是CPU、什麽是MPU
什麽是MCU、什麽是SOC
和微處理器不同要注意！應該吧

> ## 微型處理器和微型控制器有何區別？
> 微型處理器和微型控制器是電子裝置的內部元件。微型處理器是 CPU 內部非常小的處理單元。它是電腦晶片上的單一積體電路，可對數位訊號執行各種算術和邏輯功能。數十個微型處理器在高效能伺服器內共同運作，以進行資料處理和分析。
> 另一方面，微型控制器是洗衣機和恆溫器等智慧型電子裝置中的基本運算單元。它是一部非常小型的電腦，擁有自己的 RAM、ROM 和 I/O 系統，全部內嵌於單一晶片上。它可處理數位訊號並回應使用者輸入，但其運算能力受到限制。