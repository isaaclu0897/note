#what-is , #ipmi , #ipmitool , #bmc

開發中

### 什麼是 ipmitool？

ipmitool 是一個廣泛用於管理和配置支持的設備的實用程序智能平台管理界面。 IPMI 是一個開放標準用於硬件的監視、記錄、恢復、庫存和控制它的實現獨立於主 CPU、BIOS 和操作系統。服務處理器（或基板管理控制器，[[../../todo/BMC]]）是內部平台管理的主要引擎。目的是處理自主傳感器監控和事件記錄功能。

ipmitool 程序為 BMC 提供了一個簡單的命令行界面。它能夠讀取傳感器數據存儲庫 (SDR) 並打印傳感器值、顯示系統事件日誌 (SEL) 的內容、打印現場可更換單元 (FRU) 庫存信息、讀取和設置 LAN 配置參數以及執行遠程操作機櫃電源控制。

### ipmitool 能做什麼？

**Ipmitool 提供了一系列功能**，讓管理員能夠有效地管理和監控伺服器。一些關鍵的功能包括：

- 遠程電源控制：透過 IPMI 介面，您可以遠程進行開機、關機和重啟伺服器。
- 感測器監測：您可以監測硬體感測器，如溫度、風扇速度和電壓，以確保伺服器健康。
- 系統資訊：Ipmitool 可以幫助您檢索系統信息，如序列號和硬體清單。
- 事件日誌訪問：您可以查看系統事件日誌，用於疑難排解和診斷。
- 遠程控制台訪問：Ipmitool 允許進行遠程控制台重定向，這對疑難排解和恢復任務很有價值。
- 使用者管理：Ipmitool 讓您可以管理 IPMI 使用者及其權限，以增強安全性。

### 如何使用 ipmitool？

#### 安裝

要使用 ipmitool，請確保在您的系統上安裝了它：

```bash
# 安裝指令
sudo apt-get install ipmitool  # 在 Debian/Ubuntu 上
sudo yum install ipmitool      # 在 CentOS/RHEL 上
```

#### 指令

以下是使用 ipmitool 執行一些常見任務的方法：

```bash
# 開啟伺服器電源
ipmitool -H <IP地址> -U <使用者名稱> -P <密碼> power on

# 監測感測器
ipmitool -H <IP地址> -U <使用者名稱> -P <密碼> sensor list

# 查看系統信息
ipmitool -H <IP地址> -U <使用者名稱> -P <密碼> fru print

# 訪問事件日誌
ipmitool -H <IP地址> -U <使用者名稱> -P <密碼> sel list

# 遠程控制台重定向
ipmitool -H <IP地址> -U <使用者名稱> -P <密碼> sol activate
```

### 總結

Ipmitool 是一個強大的工具，用於管理和監控支援 IPMI 的伺服器。其命令行界面為管理員提供了必要的功能，以確保伺服器的健康和可用性。