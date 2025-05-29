# Intro to Endpoint Security

**🟦 Endpoint Security 簡介**

THM路徑：https://tryhackme.com/room/introtoendpointsecurity

---

>> #### Task 1：介紹

Endpoint Security ➜ **端點安全監控**

>> #### Task 2：端點安全基礎知識

📌 為什麼要認識 Core Windows Processes？
- 在分析端點日誌前，理解哪些是「正常行為」的程序 是必要的
- 否則你無法從大量事件中識別出「異常活動」

**Task Manager**：內置的基於 GUI 的 Windows 實用程式，允許使用者查看 Windows 系統上運行的內容。

<p align="left">
  <img src="/rooms/images/21_01.png" width="600">
</p>

---

🧠 常見的 Windows 核心程序（正常行為）

| 程序層級結構（Parent > Child）         | 說明                                           |
|----------------------------------------|------------------------------------------------|
| System                                 | 最底層核心程序，其父程序為 System Idle (PID 0) |
| System > smss.exe                      | Session 管理器                                 |
| csrss.exe                              | Client/Server Runtime 子系統                   |
| wininit.exe                            | Windows 初始化                                 |
| wininit.exe > services.exe             | 系統服務管理器                                 |
| services.exe > svchost.exe             | 多數服務會由 svchost.exe 執行                  |
| lsass.exe                              | 本地安全授權子系統                             |
| winlogon.exe                           | 登入管理程序                                   |
| explorer.exe                           | 使用者桌面與檔案總管界面                       |

📌 除了 System 以外，**若有程序「無父程序」或異常繼承鏈，需特別留意。**

---
🛠️ **Sysinternals** 工具套件簡介：

Sysinternals 是一套微軟官方提供的 70+ 種 Windows 深度分析工具，涵蓋以下分類：

- 📁 檔案 / 磁碟工具
- 🌐 網路工具
- 🔧 程序工具
- 🔐 安全工具
- 📊 系統資訊工具
- 🧩 其他小工具

---
📡 **TCPView** - 網路連線監控工具：

✅ 功能說明：
- 列出所有 TCP / UDP 連線
- 顯示本地 / 遠端位址與連線狀態
- 標示該連線由哪個程序啟動
- 支援 GUI 與 CLI 版本（tcpview / tcpvcon）

🎯 用途：
- 分析某程序是否與可疑 IP 建立連線
- 輔助事件關聯分析

<p align="left">
  <img src="/rooms/images/21_02.png" width="600">
</p>

---
🔍 **Process Explorer** - 高階程序分析工具：

✅ 功能說明：
- 顯示所有執行中程序（含帳號與繼承關係）
- 檢視程序開啟的 Handle（檔案、資料夾）
- 檢視載入的 DLL 與映射記憶體
- 檢查所關聯的服務與網路行為

🎯 用途：
- 比 Task Manager 更強的「可疑程序追查工具」
- 用來追查後門 / 木馬或惡意持久化行為

<p align="left">
  <img src="/rooms/images/21_03.png" width="600">
</p>

---
🧭 建議使用路線：
1. 用 **Process Explorer** 看「執行中的異常程序」與關聯服務、DLL、Handle
2. 用 **TCPView** 比對該程序是否有連外異常行為
3. 結合 SIEM 日誌與 Sysmon 事件進行交叉分析

##### 🔐 答題：

1. What is the normal parent process of services.exe?

   services.exe 的正常父流程是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `wininit.exe`

2. What is the name of the network utility tool introduced in this task?

   此任務中引入的網路實用程式工具的名稱是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `TCPView`

>> #### Task 3：端點日誌記錄和監控

🧠為什麼要**端點日誌記錄**（Endpoint Logging）？

即使能用工具查看當下系統狀態（如 Process Explorer），但：

⚠️ 若無「日誌歷史記錄」，就無法：

- **回溯攻擊時間點與路徑**
- **跨機器比對活動**
- **自動化建立偵測規則**

因此，**端點日誌記錄是威脅偵測與數位鑑識的基礎**。

---

🧾 常見端點日誌來源與分析工具

| 工具               | 說明與用途                                                                 | 特點 / 優勢                                                         |
|--------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------|
| Windows Event Logs | Windows 內建日誌系統，儲存於 `.evtx` 格式，可用 **Event Viewer**、**PowerShell** 或 **Wevtutil** 存取 | 基礎事件來源，含登入、程序建立、系統錯誤等                          |
| Sysmon             | 微軟 Sysinternals 套件之一，提供高解析度事件記錄，可客製化追蹤項目（如進程、網路、註冊表等） | 提供 27 類事件 ID，可與 SIEM 整合，自訂規則強大                     |
| Osquery            | Facebook 開源工具，使用 SQL 語法查詢端點資訊，支援跨平台（Win / Linux / Mac / BSD）     | 用戶端查詢為主，支援 Kolide Fleet 遠端集中查詢                     |
| Wazuh              | 開源 EDR 解決方案，採用 Agent/Manager 架構，可大規模部署於企業環境               | 提供威脅監控、視覺化圖表、異常行為比對、CVE 掃描等多元功能         |

---
🗂️ 使用場景簡述：

- 🔹 Windows Event Log：<br>
   - 基本系統活動：登入、系統異常、程式執行
   - 可作為 SIEM 或 Forensics 的基礎來源
   - 儲存的 `.evtx`，通常位於  `C:\Windows\System32\winevt\Logs`

使用 Event Viewer 查看 **Windows Event Log**日誌：
<p align="left">
  <img src="/rooms/images/21_04.png" width="600">
</p>

---

- 🔹 Sysmon：<br>
   - 建議安裝於伺服器與重要端點
   - 與 SIEM 結合效果極佳（可直接觸發規則）
  
使用 Event Viewer 查看 **Sysmon** 日誌：
<p align="left">
  <img src="/rooms/images/21_05.png" width="600">
</p>

---

- 🔹 Osquery：<br>
   - 偵測特定程序是否執行
   - 透過 SQL 查詢，即時分析系統資訊 
   - 搭配 Kolide Fleet 可進行集中式查詢

請打開 CMD（或 PowerShell）並執行 `osqueryi`，

<p align="left">
  <img src="/rooms/images/21_06.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/21_07.png" width="600">
</p>

藉助 Kolide Fleet，您可以從 Kolide Fleet UI 查詢多個終端節點，而不是在本地使用 `osquery` 查詢機器內部的事件

<p align="left">
  <img src="/rooms/images/21_08.png" width="600">
</p>

---

- 🔹 Wazuh
  - 作為完整 EDR 解決方案（Endpoint detection and response）
  - 支援漏洞掃描、持續監控、視覺化威脅地圖
  - 適用企業部署、大規模端點監控

<p align="left">
  <img src="/rooms/images/21_09.gif" width="600">
</p>

##### 🔐 答題：

1. Where do the Windows Event logs (.evtx files) typically reside?

   Windows 事件日誌（.evtx 檔）通常位於何處？
   
&nbsp;&nbsp;&nbsp;&nbsp; `C:\Windows\System32\winevt\Logs`

2. Provide the command used to enter OSQuery CLI.

   提供用於進入 OSQuery CLI 的命令。
   
&nbsp;&nbsp;&nbsp;&nbsp; `osqueryi`

3. What does EDR mean? Provide the answer in lowercase.

   EDR 是什麼意思？以小寫形式提供答案。
   
&nbsp;&nbsp;&nbsp;&nbsp; `Endpoint detection and response`

>> #### Task 4：端點日誌分析
🔗 **事件關聯分析（Event Correlation）**：

&nbsp;&nbsp;&nbsp;&nbsp;_<b>事件關聯</b>是指從多個不同來源的日誌中，找出彼此之間有意義的關聯關係。_ <br>

🎯 目的：
- 將來自 **應用程式 / 端點 / 網路** 的日誌碎片拼成完整事件流程
- 將一連串看似無關的事件，**「連點成線」**，形成可追查的攻擊路徑

🔍 舉例：網路連線事件可能出現在以下來源

| 資料來源              | 提供資訊                             |
|-----------------------|--------------------------------------|
| Sysmon (Event ID 3)   | 程序名稱、使用者、啟動連線的行為     |
| Firewall Logs         | IP、Port、協定、動作（Allow / Block） |

✅ 可關聯欄位包括：
- Source / Destination IP
- Source / Destination Port
- Protocol
- Process Name
- User Account
- Action Taken
- Hostname / Machine Name

📌 「事件關聯」就像把拼圖拼起來，還原真實攻擊情境，是進階分析的關鍵技巧。

---

📈 **行為基準建立（Baselining）**：

&nbsp;&nbsp;&nbsp;&nbsp;_<b>Baselining</b> 是定義「什麼是正常行為」的過程，有了基準才能識別異常。_ <br>

✅ 為什麼需要建立 Baseline？
- 沒有基準，就無法定義什麼是 異常
- 所有事件都像乾草堆中的針，難以辨識威脅

📋 範例對照表：

| 正常行為（Baseline）                                      | 異常行為（Unusual Activity）                       |
|-----------------------------------------------------------|----------------------------------------------------|
| 公司員工皆位於倫敦，正常上下班時間為 9:00–18:00           | 有人在凌晨 3 點從新加坡透過 VPN 登入              |
| 每人分配一台工作機                                        | 同一帳號嘗試登入多台工作機                        |
| 僅允許 O365 網站（如 OneDrive、SharePoint）              | 有使用者上傳 3GB 資料到 Google Drive               |
| 僅安裝 Microsoft 相關應用（Word, Excel, Teams, Chrome 等） | 多台電腦出現 firefox.exe 程序                     |

---

🧪 **調查實作活動（Investigation Activity）**：

現在是時候換上 Blue Team 帽子，根據前面所學的概念：

- 檢視端點事件
- 建立關聯
- 對比基準
- 判斷是否異常並深入調查

Question 2：進入 Baseline Document 確認正常行為

<p align="left">
  <img src="/rooms/images/21_10.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/21_11.png" width="600">
</p>

發現可疑程序為 beacon.exe

<p align="left">
  <img src="/rooms/images/21_12.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/21_13.png" width="600">
</p>

輸入惡意 IP 地址，並清除威脅，獲得 Flag 🎉🎉

<p align="left">
  <img src="/rooms/images/21_14.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/21_15.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/21_16.png" width="600">
</p>

##### 🔐 答題：
2. Provide the flag for the simulated investigation activity.
   
   為類比調查活動提供旗幟。
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{3ndp01nt_s3cur1ty!}`

