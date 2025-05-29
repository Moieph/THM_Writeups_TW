# Intro to Cyber Threat Intel

**🟦 網路威脅情報簡介**

THM路徑：https://tryhackme.com/room/cyberthreatintel

---

>> #### Task 1：介紹

Cyber Threat Intelligence（CTI）➜ **網路威脅情資** 

>> #### Task 2：網路威脅情報

🧠 CTI（網路威脅情資）簡介

- CTI 是以證據為基礎的知識，描述敵手的：
    - 指標（Indicators）
    - 戰術（Tactics） 
    - 動機（Motivations）
    - 對應建議（Actionable Advice）

➡️ 目的為保護關鍵資產、輔助決策、強化資安團隊與管理層判斷

---
🔍 「Data / Information / Intelligence」區別

| 類型                   | 說明                   | 範例                     |
| -------------------- | -------------------- | ---------------------- |
| **Data（資料）**         | 零散指標                 | IP、URL、Hash            |
| **Information（資訊）**  | 多筆資料匯整後的回答           | 員工一個月內連線 TryHackMe 的次數 |
| **Intelligence（情資）** | 結合資訊與背景脈絡，形成可採取行動的見解 | 分析敵手行為模式與潛在攻擊時間點       |

---

🎯 CTI 主要目標

透過建立「攻防關係脈絡」，回答下列問題：
- 誰在攻擊我？（Who）
- 為什麼攻擊我？（Why）
- 對方有多厲害？（Capabilities）
- 有哪些可供偵測的指標？（IOCs）

---

📚 CTI 資料來源分類

| 類型                | 說明                                 |
| ----------------- | ---------------------------------- |
| **Internal（內部）**  | 事件報告、漏洞掃描、系統日誌、訓練成效                |
| **Community（社群）** | 公開論壇、暗網社群、攻擊者討論區                   |
| **External（外部）**  | 威脅情資訂閱源（商業 / 開源）、政府報告、OSINT、市場評估資料 |

---

🧩 CTI 四大分類（情資類型）

| 分類                        | 說明                               | 使用對象                 |
|---------------------------|----------------------------------| -------------------- |
| **Strategic Intel（戰略情資）** | 高層次、趨勢導向，協助制定政策與業務決策             | 管理層                  |
| **Technical Intel（技術情資）** | 攻擊用指標（IP、URL、惡意檔等），建構基準面及防禦機制。   | Incident Response 團隊 |
| **Tactical Intel（戰術情資）**  | TTPs（戰術、技術、程序），即 MITRE ATT&CK 對應行為 | 藍隊工程師、SOC            |
| **Operational Intel（作戰情資）**    | 分析敵方具體行動意圖與目標資產                  | 情資分析師、攻防研究員          |



##### 🔐 答題：
1. What does CTI stand for?
   
   CTI 代表什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{PACKET_MASTER}`

2. IP addresses, Hashes and other threat artefacts would be found under which Threat Intelligence classification?
   
   IP 位址、哈希和其他威脅工件將在哪個威脅情報分類下找到？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{PACKET_MASTER}`

>> #### Task 3：CTI 生命週期

CTI **情資生命週期**（六步驟）

| 階段                          | 中文說明          | 重點內容                                                    |
| --------------------------- | ------------- | ------------------------------------------------------- |
| 1️⃣ **Direction（方向規劃）**     | 確立目標與資安需求     | 🎯 決定保護哪些資產<br>💥 評估損失風險<br>🔍 情資來源與工具                  |
| 2️⃣ **Collection（資料收集）**    | 根據目標蒐集威脅資料    | 📚 商用 / 開源 / 私有來源<br>⚙️ 建議自動化處理                         |
| 3️⃣ **Processing（資料處理）**    | 將原始資料轉換成可分析格式 | 🧩 整合日誌、漏洞、流量<br>🏷️ 資料分類、標籤、可視化<br>🔧 SIEM 為常見工具       |
| 4️⃣ **Analysis（情資分析）**      | 從整合資料中提取洞察    | 🕵️‍♂️ 發現指標與攻擊模式<br>🛡️ 制定防禦計畫<br>💰 證明資源需求合理性          |
| 5️⃣ **Dissemination（情資傳遞）** | 對不同對象傳遞不同內容   | 👨‍💼 C-Level：趨勢、財務風險、策略建議<br>👨‍💻 技術團隊：IOCs、TTPs、行動指南 |
| 6️⃣ **Feedback（回饋機制）**      | 根據回應優化流程與防禦措施 | 🔁 持續互動、調整政策<br>📈 增進整體威脅回應效率                           |

<p align="left">
  <img src="/rooms/images/24_01.png" width="600">
</p>

##### 🔐 答題：
1. At which phase of the CTI lifecycle is data converted into usable formats through sorting, organising, correlation and presentation?
   
   在 CTI 生命週期的哪個階段，數據通過排序、組織、關聯和呈現轉換為可用的格式？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Processing`

2. During which phase do security analysts get the chance to define the questions to investigate incidents?
   
   安全分析師在哪個階段有機會定義問題以調查事件？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Direction`

>> #### Task 4：CTI 標準和框架

📘 常見威脅情報（CTI）標準與框架總覽：

| 名稱                                                                | 說明                               | 作用                                |
| ----------------------------------------------------------------- | -------------------------------- | --------------------------------- |
| **MITRE ATT&CK**                                                  | 對手行為知識庫，依「戰術與技術」分類               | 🧠 偵測行為模式、建立防禦矩陣                  |
| **TAXII**<br>(Trusted Automated eXchange of Indicator Information) | 威脅情報的交換協議                        | 🔄 支援推播（Channel）與查詢（Collection）模式 |
| **STIX**<br>(Structured Threat Information Expression)            | 用來描述與傳遞威脅情報的資料格式（語言）             | 🧩 結構化定義指標、觀察項、攻擊活動等關係            |
| **Cyber Kill Chain**                                              | 分析攻擊流程的 7 個階段模型（Lockheed Martin） | 🧱 協助判斷駭客目前所處的攻擊階段                |
| **Diamond Model**                                                 | 入侵分析模型，描繪攻擊的四個關鍵面向               | ♦️ 對應攻擊者、受害者、基礎設施、能力              |

MITRE ATT&CK Matrix：

<p align="left">
  <img src="/rooms/images/24_02.png" width="600">
</p>

---

🧱 Cyber Kill Chain 七階段（補充中譯）

| 階段                          | 說明          | 範例                    |
| --------------------------- | ----------- | --------------------- |
| Reconnaissance（偵察）          | 收集目標資訊      | OSINT、蒐集信箱、掃描網路       |
| Weaponisation（武器化）          | 開發惡意載荷      | 植入後門、Word 惡意文件        |
| Delivery（投遞）                | 投送攻擊手法      | 郵件釣魚、USB、網站連結         |
| Exploitation（漏洞利用）          | 利用系統弱點執行攻擊  | EternalBlue、ZeroLogon |
| Installation（安裝）            | 植入惡意程式 / 工具 | Mimikatz、RAT          |
| Command & Control（遠端控制）     | 遠控受害主機、橫向移動 | Cobalt Strike、Empire  |
| Actions on Objectives（達成目的） | 實現駭客意圖      | 資料外洩、加密勒索、破壞形象        |

---

♦️ Diamond Model（鑽石模型）四元素對照

- 可透過「關聯 + 轉向」方式追查攻擊來源與手法，建立完整入侵事件畫像。

| 元素                       | 說明                   |
| ------------------------ | -------------------- |
| **Adversary（攻擊者）**       | 威脅來源（APT、駭客組織）       |
| **Victim（受害者）**          | 攻擊目標（個人、機構）          |
| **Infrastructure（基礎設施）** | 攻擊用系統與受害者資源          |
| **Capabilities（能力）**     | 採用手法與 TTPs（戰術、技術、程序） |

<p align="left">
  <img src="/rooms/images/24_03.png" width="600">
</p>

---

📌 補充應用場景：

- **MITRE ATT&CK** ：用於紅隊模擬攻擊、防禦者偵測行為
- **STIX 搭配 TAXII**：實現企業與社群間的自動化情報交換
- **Cyber Kill Chain**：幫助事件回溯：發現攻擊階段有無被阻擋
- **Diamond Model**：強化調查時的橫向關聯與視覺呈現能力

##### 🔐 答題：
1. What sharing models are supported by TAXII?
   
   TAXII 支援哪些共用模型？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Collection and Channel`

2. When an adversary has obtained access to a network and is extracting data, what phase of the kill chain are they on?
   
   當對手獲得網路訪問許可權並提取數據時，他們處於殺傷鏈的哪個階段？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Actions on Objectives`

>> #### Task 5：實用分析

Question 1、2：對照上圖，得到答案：

<p align="left">
  <img src="/rooms/images/24_04.png" width="600">
</p>

Question 3：完成題目後，獲得 Flag 🎉🎉

<p align="left">
  <img src="/rooms/images/24_05.png" width="600">
</p>

##### 🔐 答題：
1. What was the source email address?
   
   源電子郵件地址是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `vipivillain@badbank.com`

2. What was the name of the file downloaded?
   
   下載的檔案名稱是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `flbpfuh.exe`

3. After building the threat profile, what message do you receive?
   
   構建威脅配置檔後，您會收到什麼消息？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{NOW_I_CAN_CTI}`