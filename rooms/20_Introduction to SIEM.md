# Introduction to SIEM

**🟦 SIEM 簡介**

THM路徑：https://tryhackme.com/room/introtosiem

---

>> #### Task 1：介紹

🧠 什麼是 SIEM？

 **Security Information and Event Management（安全資訊與事件管理）**

是一種資安工具，具備以下功能：

- 收集：從網路中各種終端設備、伺服器、網路設備等收集日誌資料
- 集中：將這些資料統一儲存於一個中央平台
- 關聯分析：透過規則比對與模式關聯，找出潛在異常或資安事件

簡單來說，**SIEM 是企業監控、分析、偵測資安事件的「核心大腦」**。

>> #### Task 2：通過 SIEM 實現網路可見性

🌐 為何需要 SIEM？先從<b>「網路可視性」</b>說起

一個基本網路架構會包含：
- 多個 **Linux / Windows 終端節點**
- 一台 **資料伺服器**
- 一個 **網站**
- 一個 **路由器（網關） 管理內外連線**

在這樣的環境中，各裝置都會產生不同的 **日誌（Logs）**，若不集中處理，發生事件時要一台一台分析，幾乎不可能。

<p align="left">
  <img src="/rooms/images/20_01.png" width="600">
</p>

---

📂 日誌來源分類（Log Source Types）

| 類型                 | 說明與常見來源                                           | 範例事件                                                       |
|----------------------|----------------------------------------------------------|----------------------------------------------------------------|
| 🖥️ Host-Centric Logs  | 針對單一主機發生的行為記錄，如系統事件、行為異常         | 使用者登入、檔案存取、程式執行、註冊表變更、PowerShell 執行   |
| 🌐 Network-Centric Logs | 主機之間或與網際網路通訊產生的日誌                     | SSH 連線、FTP 檔案下載、VPN 使用、網站瀏覽、網路檔案共享       |

工具例子：
- Host-Centric：<br>Windows Event Logs、Sysmon、Osquery
- Network-Centric：<br>Router/Firewall 日誌、VPN Server、Web Proxy、IDS/IPS

---

🛡️ SIEM 的重要性（Why SIEM Matters）

- **單靠人工逐一檢查每台裝置的 log 是不切實際的**
- **SIEM 解決的就是「整合 + 搜索 + 關聯 + 偵測」的問題**

<p align="left">
  <img src="/rooms/images/20_02.png" width="600">
</p>

---

✅ SIEM 提供的核心功能：

| 功能名稱               | 說明                                                            |
|------------------------|-----------------------------------------------------------------|
| 即時日誌收集（Log Ingestion）   | 可從各系統即時接收 log 並集中存儲                              |
| 行為異常警示（Alerting）       | 偵測可疑活動，自動發出警示                                    |
| 24/7 監控與可視化              | 提供 SOC 全天候監控與事件視覺呈現                              |
| 威脅早期偵測（Threat Detection） | 偵測已知與未知攻擊技巧，降低潛在風險                          |
| 資料洞察與分析（Insight & Viz） | 可視化圖表、統計趨勢、事件儀表板等                           |
| 事件調查與追溯（Investigation） | 支援事件調查與歷史資料查詢，協助事後分析與應變                  |

##### 🔐 答題：
1. Is Registry-related activity host-centric or network-centric?
   
   Registry 相關活動是以主機為中心還是以網路為中心？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Host-Centric`

2. Is VPN related activity host-centric or network-centric?
   
   VPN 相關活動是以主機為中心還是以網路為中心？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Network-Centric`

>> #### Task 3：日誌源和日誌引入

🧾 常見設備的日誌來源（Log Sources by Device）

| 裝置類型           | 日誌來源與描述                                                                                               |
|--------------------|-------------------------------------------------------------------------------------------------------|
| Windows 裝置        | 透過內建的 **Event Viewer** 管理所有事件記錄（含唯一事件 ID）並將其轉送至 SIEM                                                  |
| Linux 工作站        | 儲存於 `/var/log` 目錄下：<br>• `auth.log` / `secure`（登入）<br>• `cron`（排程任務）<br>• `kern`（核心）等 |
| Web Server（Apache）| 存於 `/var/log/apache` 或 `/var/log/httpd`，記錄所有 HTTP 請求與錯誤                                               |

🔍 **這些日誌將會送至 SIEM 平台做集中監控與異常偵測。**

---

Windows 裝置：**Event Viewer**
<p align="left">
  <img src="/rooms/images/20_03.gif" width="600">
</p>



Linux 工作站：`cron` log
<p align="left">
  <img src="/rooms/images/20_04.png" width="600">
</p>


Web Server：Apache Logs
<p align="left">
  <img src="/rooms/images/20_05.png" width="600">
</p>

---

📡 **常見日誌收集方式（Log Ingestion Methods）**

| 方法               | 說明                                                                                     |
|--------------------|------------------------------------------------------------------------------------------|
| 1. Agent / Forwarder | 安裝代理程式於終端設備（如 Splunk Forwarder），收集並轉送關鍵日誌至 SIEM                 |
| 2. Syslog           | 使用標準 Syslog 協定，將來自 Web Server / DB 等設備的資料即時送至 SIEM                   |
| 3. Manual Upload    | 允許使用者手動上傳離線日誌進行分析（如 Splunk、ELK）                                     |
| 4. Port Forwarding  | 設定 SIEM 監聽特定 Port，裝置將資料主動傳送至該端口（可搭配 rsyslog 等實作）             |

<p align="left">
  <img src="/rooms/images/20_06.png" width="600">
</p>

---

🧠 延伸說明：
- **Agent 適用於主機日誌（Host-Centric）**
- **Syslog 通常用於網路與伺服器日誌（Network/Web Services）**
- **Manual Upload 常用於事件事後鑑識（Forensics）**
- **Port Forwarding 適合與輕量裝置或 IoT 整合**

---

**Splunk** 日誌收集方法：

<p align="left">
  <img src="/rooms/images/20_07.png" width="600">
</p>

##### 🔐 答題：
1. In which location within a Linux environment are HTTP logs stored?
   
   HTTP 日誌存儲在 Linux 環境中的哪個位置？
   
&nbsp;&nbsp;&nbsp;&nbsp; `/var/log/httpd`

>> #### Task 4：為什麼選擇 SIEM

🛡️ SIEM 的核心功能與作用：

- **SIEM（安全資訊與事件管理系統）** 是 SOC（資安營運中心）中不可或缺的關鍵元件，能協助企業即時偵測並回應資安威脅。

---

🎯 SIEM 的主要功能（SIEM Capabilities）：

| 功能項目                             | 說明                                                                 |
|--------------------------------------|----------------------------------------------------------------------|
| 事件關聯分析（Event Correlation）      | 整合來自不同裝置的日誌資料，建立跨來源的異常偵測能力                     |
| 可視化主機與網路行為（Visibility）     | 同時觀察 Host-Centric 與 Network-Centric 活動                         |
| 威脅調查與即時應變                    | 協助分析師深入追蹤事件細節並快速回應                                |
| 規則外的威脅狩獵（Threat Hunting）     | 補足規則偵測盲點，主動發掘尚未被偵測的攻擊行為                         |

📌 一旦發現異常行為或達到警示門檻，SIEM 會自動產生警示（Alert），引導分析師進行調查與回應。

---

👨‍💻 SOC 分析師的工作職責（SOC Analyst Responsibilities）：

&nbsp;&nbsp;&nbsp;&nbsp;_SOC 分析師是第一線資安守門人，依賴 SIEM 系統掌握網路環境中一切活動。_ <br>

---

**🔍 SOC 分析師的主要職責：**


| 職責項目                     | 說明                                                                 |
|------------------------------|----------------------------------------------------------------------|
| 監控與調查（Monitoring & Investigating） | 持續追蹤警示與事件，展開調查                                         |
| 排除誤報（False Positives）       | 協助辨識並排除非惡意行為的誤報警示                                   |
| 規則調整（Rule Tuning）         | 優化 SIEM 規則以減少噪音與誤判                                       |
| 報告與法遵（Reporting & Compliance） | 編寫事件報告、支援稽核與資安合規需求                                 |
| 發現可視性盲點（Blind Spot Detection） | 發掘未納入監控的裝置或行為，擴展日誌涵蓋範圍                           |

<p align="left">
  <img src="/rooms/images/20_08.png" width="600">
</p>

>> #### Task 5：分析日誌和警報
🧠 SIEM 運作機制簡介：
1. 日誌收集（Log Ingestion）
   - 使用 Agent、Port Forwarding 等方式收集安全相關日誌
   - 日誌經過標準化（Normalization）後進入 SIEM

2. 規則比對與警示（Rule Matching & Alerting）：
   - SIEM 根據分析師設定的 **Correlation Rule（關聯規則）** 判斷是否觸發警示
   - 若條件達成，則生成警示（Alert），進入事件調查階段

---

**📊 Dashboard 儀表板：**

&nbsp;&nbsp;&nbsp;&nbsp;_儀表板是 SIEM 的核心視覺化元件，協助分析師快速掌握網路狀況與安全異常。_ <br>

<p align="left">
  <img src="/rooms/images/20_09.png" width="600">
</p>

**儀表板常見資訊：**

| 類別                 | 說明                                                  |
|----------------------|-------------------------------------------------------|
| Alert Highlights      | 最新 / 高嚴重度警示總覽                                |
| System Notification   | 系統訊息、模組狀態、錯誤提醒                            |
| Health Alert          | SIEM 平台自身健康狀態                                   |
| Failed Logins         | 登入失敗次數 / 排名清單                                 |
| Event Count           | 日誌收集數量統計                                        |
| Rules Triggered       | 被觸發的規則列表                                        |
| Top Domains Visited   | 最常被存取的網域，協助檢視可疑連線                      |

---

**📐 關聯規則（Correlation Rules）：**

&nbsp;&nbsp;&nbsp;&nbsp;_SIEM 的核心偵測邏輯，通常是「條件判斷式」，符合條件即產生警示。_ <br>

**規則範例：**

| 規則條件                             | 警示說明                       |
|--------------------------------------|--------------------------------|
| 使用者在 10 秒內失敗登入 5 次        | 多次失敗登入警示              |
| 多次失敗登入後成功登入              | 可疑成功登入                  |
| 使用者插入 USB（若公司政策禁止）    | 未授權設備存取警示            |
| 出站流量大於 25MB（視企業政策）      | 潛在資料外洩警示              |

---

🎯 Use Case 實例：
- Use Case 1：清除事件記錄
  - 事件 ID：104（事件日誌被清除）
  - 規則：若 Log Source 為 `WinEventLog` 且 `EventID=104` ➝ 產生「清除事件記錄」警示


- Use Case 2：使用 `whoami` 命令
  - 事件 ID：4688（Process Creation）
  - 條件欄位：`NewProcessName` 包含 `whoami`
  - 規則：若 `EventCode=4688` 且 `NewProcessName` 包含 `whoami` ➝ 警示「偵測到 `whoami` 命令」

---
🔎  **警示調查流程（Alert Investigation）：**<br>
分析師主要工作集中在 Dashboard 上，觸發警示流程 :

1️⃣ 檢查警示關聯事件（Event/Flow）  
2️⃣ 驗證規則觸發條件是否合理  
3️⃣ 判斷是否為誤報（False Positive）或真實警報（True Positive）  
4️⃣ 採取下列行動之一：

- 是誤報 ➝ 微調規則，降低未來誤報機率  


- 是真警報 ➝ 深入調查  
   - 聯繫資產擁有者確認行為  
   - 當可疑行為成立：  
     - 隔離主機  
     - 封鎖可疑 IP / 網域

##### 🔐 答題：
1. Which Event ID is generated when event logs are removed?
   
   刪除事件日誌時，會生成哪個事件 ID？
   
&nbsp;&nbsp;&nbsp;&nbsp; `104`

2. What type of alert may require tuning?
   
   什麼類型的警報可能需要調整？
   
&nbsp;&nbsp;&nbsp;&nbsp; `False Alarm`

>> #### Task 6：實驗室工作

Question 1：進入 SIEM 介面，點擊 Start Suspicious Activity，發現可疑活動

<p align="left">
  <img src="/rooms/images/20_10.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/20_11.png" width="600">
</p>

Question 2、3：查看可疑事件，發現其可疑活動執行者及主機名稱

<p align="left">
  <img src="/rooms/images/20_12.png" width="600">
</p>

Question 4：查看規則，發現該可疑活動觸發條件 

<p align="left">
  <img src="/rooms/images/20_13.png" width="600">
</p>

Question 5：判斷該可疑活動，是否為誤報

<p align="left">
  <img src="/rooms/images/20_14.png" width="600">
</p>

Question 6：判斷後獲得 Flag 🎉🎉

<p align="left">
  <img src="/rooms/images/20_15.png" width="600">
</p>

##### 🔐 答題：
1. Click on Start Suspicious Activity, which process caused the alert?
   
   單擊 Start Suspicious Activity（開始可疑活動），哪個進程導致了警報？
   
&nbsp;&nbsp;&nbsp;&nbsp; `cudominer.exe`

2. Find the event that caused the alert, which user was responsible for the process execution?
   
   查找導致警報的事件，哪個使用者負責流程執行？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Chris.fort`

3. What is the hostname of the suspect user?
   
   可疑使用者的主機名是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `HR_02`

4. Examine the rule and the suspicious process; which term matched the rule that caused the alert?
   
   檢查規則和可疑過程;哪個術語與導致警報的規則匹配？
   
&nbsp;&nbsp;&nbsp;&nbsp; `miner`

5. What is the best option that represents the event? Choose from the following:
   
   代表事件的最佳選擇是什麼？從以下選項中選擇：
   
&nbsp;&nbsp;&nbsp;&nbsp; `True-Positive`

6. Selecting the right ACTION will display the FLAG. What is the FLAG?
   
   選擇正確的 ACTION 將顯示 FLAG。什麼是 FLAG？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{000_SIEM_INTRO}`