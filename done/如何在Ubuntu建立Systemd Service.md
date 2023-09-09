#how-to , #ubuntu , #systemctl, #systemd


https://blog.gtwang.org/linux/linux-create-systemd-service-unit-for-python-echo-server-tutorial-examples/

https://blog.gtwang.org/linux/linux-basic-systemctl-systemd-service-unit-tutorial-examples/

[TOC]

## 如何創建

```
# juptyer.sevice in /etc/systemd/system
[Unit]                                                                                                                 
# 服務名稱
Description=My Jupyter Server

[Service]
# 行程類型
Type=simple

# 啟動服務指令
ExecStart=jupyter-notebook

# 服務終止時自動重新啟動
Restart=always

[Install]
WantedBy=multi-user.target

```

## 如何使用

```
# 重新載入 Systemd 設定檔
sudo systemctl daemon-reload
```



```
sudo systemctl edit --full jupyter.service
```

### 如何更換編輯器
```
sudo update-alternatives --config editor
```
>替代項目 editor（提供 /usr/bin/editor）有 4 個選擇。
>
>  選項       路徑              優先權  狀態
>------------------------------------------------------------
>  0            /bin/nano            40        自動模式
>  1            /bin/ed             -100       手動模式
>  2            /bin/nano            40        手動模式
>* 3            /usr/bin/vim.basic   30        手動模式
>  4            /usr/bin/vim.tiny    15        手動模式
>
>Press <enter> to keep the current choice[*], or type selection number: 3



```
sudo chmod 644 /etc/systemd/system/echo_server.service
```

## 範例檔案

```bash
[Unit]
# 服務名稱
Description=Your Server

# 服務相關文件
# Documentation=https://example.com
# Documentation=man:nginx(8)

# 設定服務啟動的先後相依姓，例如在網路啟動之後：
# After=network.target

[Service]
# 行程類型
Type=simple

# 啟動服務指令
ExecStart=/opt/your_command

# 服務行程 PID（通常配合 forking 的服務使用）
# PIDFile=/run/your_server.pid

# 啟動服務前，執行的指令
# ExecStartPre=/opt/your_command

# 啟動服務後，執行的指令
# ExecStartPost=/opt/your_command

# 停止服務指令
# ExecStop=/opt/your_command

# 停止服務後，執行的指令
# ExecStopPost=/opt/your_command

# 重新載入服務指令
# ExecReload=/opt/your_command

# 服務終止時自動重新啟動
Restart=always

# 重新啟動時間格時間（預設為 100ms）
# RestartSec=3s

# 啟動服務逾時秒數
# TimeoutStartSec=3s

# 停止服務逾時秒數
# TimeoutStopSec=3s

# 執行時的工作目錄
# WorkingDirectory=/opt/your_folder

# 執行服務的使用者（名稱或 ID 皆可）
# User=myuser

# 執行服務的群組（名稱或 ID 皆可）
# User=mygroup

# 環境變數設定
# Environment="VAR1=word1 word2" VAR2=word3 "VAR3=$word 5 6"

# 服務輸出訊息導向設定
# StandardOutput=syslog

# 服務錯誤訊息導向設定
# StandardError=syslog

# 設定服務在 Syslog 中的名稱
# SyslogIdentifier=your-server

[Install]
WantedBy=multi-user.target
```