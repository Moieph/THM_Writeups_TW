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

>> #### Task 3：端點日誌記錄和監控

>> #### Task 4：端點日誌分析

>> #### Task 5：結論
