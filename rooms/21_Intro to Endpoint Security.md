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
   
&nbsp;&nbsp;&nbsp;&nbsp; `wininit.exe`

>> #### Task 3：端點日誌記錄和監控

>> #### Task 4：端點日誌分析

>> #### Task 5：結論
