# Intro to Detection Engineering

**🟦 Detection Engineering 簡介**

THM路徑：https://tryhackme.com/room/introtodetectionengineering

---

>> #### Task 1：介紹

Detection Engineering ➜ **偵測工程**

>> #### Task 2：什麼是偵測工程？
🧠 什麼是 Detection Engineering？

- **Detection Engineering（偵測工程）** 是一種持續性工作，專注於建立與優化「威脅偵測邏輯」與流程。


🎯 目的：
- 發現潛在惡意活動
- 發現錯誤配置或風險行為
- 對抗不斷演化的對手行為（如 APT、勒索、橫向移動）

---
🔍 偵測類型分類

| 偵測類型                        | 子類別               | 核心焦點               | 代表方法               |
|---------------------------------|----------------------|------------------------|------------------------|
| **環境導向（Environment-based）**   | Configuration Detection | 偵測配置錯誤           | 比對資產設定值         |
|                                 | Modelling            | 偵測偏離正常的行為     | 行為建模與異常識別     |
| **威脅導向（Threat-based）**        | Indicator Detection  | 偵測已知威脅指標       | 黑名單 / IOC           |
|                                 | Threat Behaviour     | 偵測攻擊者行為（TTPs） | MITRE 行為模式         |

---

**Configuration Detection**（配置檢查）：

✅ 優點：
- 容易實作
- 可橫跨多領域（如網路、身分、資產）

⚠️ 缺點：
- 高動態環境中易產生誤報
- 需假設已熟悉環境結構

---

**Modelling**（行為建模）：

✅ 優點：
- 能偵測未知威脅（因異常行為產生）

⚠️ 缺點：
- 難以解釋背景與真實意圖
- 易將惡意行為納入基準（污染模型）

---

**Indicator Detection**（指標偵測）：

✅ 優點：
- 部署快速、精確度高
- 適合追蹤已知威脅（如 C2 IP、惡意檔案 Hash）

⚠️ 缺點：
- 需「先觀察到」才有依據（被動）
- 攻擊者一換指標就失效

---
**Threat Behaviour Detection**（行為型態偵測）：

✅ 優點：
- 抗變性強，不怕 IOC 更新
- 假陽性率低，適合整合 Playbook 與自動化

⚠️ 缺點：
- 初始建立門檻較高
- 資料量需求大，需完整環境行為基線

---
🧪 Detection as Code（DaC）觀念

- Detection as Code 是將偵測流程視為可版本管理、可測試、可共享的 **「程式碼資產」**。 

🔧 DaC 核心優勢：

| 功能面       | 說明                                                         |
|--------------|--------------------------------------------------------------|
| 版本控制     | 能追蹤規則變更歷程、便於審查與回溯                            |
| 自動化測試   | 搭配 CI/CD，能自動驗證偵測品質與減少誤報                    |
| 跨團隊協作   | 安全團隊能用共通語言（如 YAML、Sigma、YARA）進行交流與共享   |
| 程式碼重用   | 可將偵測邏輯模組化，快速套用到不同場景                        |


<p align="left">
  <img src="/rooms/images/22_01.png" width="600">
</p>

---
✅ 實務結論：如何組合使用？    

| 組合方式                      | 效果                                       |
|-------------------------------|--------------------------------------------|
| Configuration + Modelling     | 強化「環境行為 + 資產狀態」識別            |
| Indicator + Threat Behavior   | 結合「已知威脅」與「可延伸行為」            |
| DaC + SIEM + Playbook         | 建立完整、可自動化的偵測防禦鏈              |

---

##### 🔐 答題：
1. Which detection type focuses on misalignments within the current infrastructure?
   
   哪種檢測類型側重於當前基礎設施中的錯位？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Configuration`

2. Which detection approach involves building an asset or activity baseline profile for detection?
   
   哪種檢測方法涉及構建用於檢測的資產或活動基線配置檔？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Modelling`

3. Which type of detection integrates with defensive playbooks?
   
   哪種類型的檢測與 Defenseive playbook 集成？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Threat Behaviour`

>> #### Task 3：偵測工程方法

🧠 **Detection Gap Analysis** 偵測缺口分析

- 透過系統性流程找出組織中尚未覆蓋的攻擊面與偵測空白區，強化防禦能力。

---

📌 **Detection Engineering 完整流程圖**
1. 威脅建模（Threat Modelling）
2. 資料盤點與日誌收集（Datasource & Logging）
3. 建立行為基準（Baselining）
4. 集中日誌收集（Log Aggregation）
5. 偵測規則撰寫（Rule Writing
6. 部署、自動化與調整（Deployment & Tuning）

---

<details>
<summary><strong>詳細步驟</strong></summary>


🧭 步驟一：**威脅建模（Threat Modelling）**

| 模式               | 說明                                                                 |
|--------------------|----------------------------------------------------------------------|
| 被動式（Reactive） | 回顧近期內部資安事件報告，找出曾遺漏的偵測機制                      |
| 主動式（Proactive）| 結合 MITRE ATT&CK + 情資來源，預測對手可能的 TTPs，事先設計偵測規則 |

✅ 注意：此處「建模」不同於前面提到的偵測類型 Modelling，這裡偏向攻擊面風險評估。

---
📡 步驟二：**資料來源識別與日誌蒐集（Datasource & Logging）**

- 根據預期風險與攻擊方式，盤點現有日誌來源：
    - 如 Sysmon（主機）、EDR、Proxy logs（網路）、IAM 日誌等
  

- 識別：
  - ✅ 哪些資料已具備？
  - ⚠️ 哪些關鍵資料缺漏？

---
📈  步驟三：**建立 Baseline（行為基準）**

| 分類       | 說明                                                                 |
|------------|----------------------------------------------------------------------|
| 高層級基準 | 與 OS 無關，依據資安政策制定廣義標準（如存取時段、通訊協定）        |
| 技術基準   | 依據作業系統設定，例如硬化、網路流量行為、IAM 控制、應用安裝行為等 |

💡 此步驟需要跨部門合作，並應持續滾動更新。

---
🗂️  步驟四：**集中日誌收集（Log Aggregation）**

- 將各來源日誌導入 SIEM / Log Server

- 使用工具如：
    - 🖥️ Sysmon（主機層級）
    - 🌐 Network Sensor（網路層級）
    - 🛡️ EDR / Proxy / VPN logs（安全通訊層級）

---
✍️  步驟五：**偵測規則撰寫（Rule Writing）**

| 日誌類型           | 對應工具/語言     |
|--------------------|------------------|
| Log-based（SIEM）  | Sigma（泛用語言） |
| File-based         | YARA             |
| Network-based      | Snort            |

- 可結合 MITRE TTPs 建立行為模式規則
- 可參考：Sigma / Snort / YARA 課程進一步撰寫方法

---
🔄 步驟六：部署、自動化與調整（Deployment & Tuning）
- ✅ 將測試通過的規則上線
- 📈 長期觀察以下目標並持續優化：
  - 環境變動
  - 攻擊手法演進
  - 誤報率 / 漏報率

</details>

>> #### Task 4：偵測工程框架 1

<details>
<summary><strong>🧠 MITRE 的資安知識體系：</strong></summary>

1. 🔷 **ATT&CK Framework**

- 全名：Adversarial Tactics, Techniques, and Common Knowledge


- 作用：分析並整理各種平台（Windows / Linux / macOS / Mobile）上常見的攻擊者 **TTPs（戰術、技術、程序）**


- 用途：

    - 製作偵測規則與場景模擬（如 Detection Gap Analysis）

    - 建立紅隊與藍隊測試基準


- 對象：Detection Engineers、Threat Hunters、SOC 分析師

2. 🔶 **CAR Framework（Cyber Analytics Repository）** 

- 由 MITRE 發布，提供根據 ATT&CK 對應的 偵測邏輯模板與範例
- 含明確的 log source / query / detection pattern
- 幫助分析師用更科學化、模組化的方式撰寫偵測規則

<p align="left">
  <img src="/rooms/images/22_02.png" width="600">
</p>

</details>

---

🔺 **Pyramid of Pain（金字塔痛苦指標）**
- 概念：偵測不同層級的攻擊指標，對攻擊者造成的「痛苦程度」不同
- 等級越高，攻擊者越難應變：

| 層級（從底層到頂層）          | 偵測項目           | 攻擊者變更難度 |
|-------------------------------|--------------------|----------------|
| Hash Values                   | 檔案雜湊           | 非常容易       |
| IP Addresses                  | 攻擊來源 IP        | 容易           |
| Domain Names                  | C2 網域            | 普通           |
| Network/Host Artifacts        | 指令特徵、路徑等     | 有點困難       |
| Tools                         | 使用的工具          | 困難           |
| TTPs                          | 行為模式（MITRE）   | 非常困難       |

✅ 越往上偵測，對攻擊者影響越大，但實作成本也越高。

<p align="left">
  <img src="/rooms/images/22_03.png" width="600">
</p>

---
🪖 **Cyber Kill Chain（Lockheed Martin）**

- 用途：用「軍事作戰邏輯」模擬資安攻擊步驟
- 7 個階段：
    1. Reconnaissance（偵察）
    2. Weaponisation（武器化）
    3. Delivery（傳遞）
    4. Exploitation（利用漏洞）
    5. Installation（安裝惡意程式）
    6. Command & Control（C2）
    7. Actions on Objectives（目標行動）

🎯 作用：
- 建立事件偵測邏輯、SOC 分析流程
- 教育使用者理解攻擊流程全貌

<p align="left">
  <img src="/rooms/images/22_04.png" width="600">
</p>

---

🧩 **Unified Kill Chain**
- 擴充版 Kill Chain：整合 MITRE ATT&CK + Cyber Kill Chain
- 增加更多細節，將攻擊流程拆解為 18 個階段
- 更適合應用在現代化 APT / 持續性攻擊偵測策略中

<p align="left">
  <img src="/rooms/images/22_05.png" width="600">
</p>

---

##### 🔐 答題：
1. Which framework looks at how to make it difficult for an adversary to change their approach when detected?
   
   哪個框架著眼於如何使攻擊者在檢測到時難以改變其方法？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Pyramid of Pain`

2. What is the improved Cyber Kill Chain framework called?
   
   改進後的 Cyber Kill Chain 框架叫什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `The Unified Kill Chain`

3. How many phases are in the improved kill chain?
   
   改進後的殺傷鏈中有多少個階段？
   
&nbsp;&nbsp;&nbsp;&nbsp; `18`

>> #### Task 5：偵測工程框架 2

📘 **Alerting and Detection Strategy Framework（ADS 框架）**

- 旨為克服 **「警報疲勞」**
- 將檢測規則發佈到生產環境之前必須遵循該流程

| 階段名稱                          | 說明 |
|-----------------------------------|------|
| Goal（目標）                      | 說明設置警報的初衷，以及要偵測的行為類型 |
| Categorisation（分類）            | 將檢測策略對應到 MITRE ATT&CK 的 TTPs，方便分析師理解事件位置與對應 Kill Chain 階段 |
| Strategy Abstract（策略摘要）     | 說明警報背後邏輯、資料來源、誤報避免方式 |
| Technical Context（技術背景）     | 描述策略執行的技術環境，例如涉及的系統平台與工具 |
| Blind Spots & Assumptions（盲點與假設） | 確認可能漏偵區域與策略無法涵蓋的情境 |
| False Positives（誤報來源）       | 敘述可能產生誤報的情況（如環境設定錯誤、合法行為誤判） |
| Validation（驗證）                | 設計測試用例觸發真實警報，進行單元測試 |
| Priority（優先權）                | 設定警報的內部分級標準，非 SIEM 呈現的嚴重程度 |
| Response（回應指南）              | 撰寫分級應變流程與調查指引，供分析師快速處置 |

<p align="left">
  <img src="/rooms/images/22_06.png" width="600">
</p>

---
🧱 **Detection Maturity Level（DML）模型**

| DML 級別 | 對應能力                         | 說明 |
|----------|----------------------------------|------|
| DML-8    | Goals（目標）                   | 能洞察對手的意圖與終極目標（幾乎不可能） |
| DML-7    | Strategy（策略）                | 能識別對手的整體行動策略與企圖 |
| DML-6    | Tactics（戰術）                 | 可發現對手採用的戰術（例如橫向移動） |
| DML-5    | Techniques（技術）              | 辨識特定攻擊者慣用的技術手法（如 DLL Injection） |
| DML-4    | Procedures（流程）              | 偵測具流程性的一連串行為（如 C2 建立 ➝ 資料蒐集 ➝ 外傳） |
| DML-3    | Tools（工具）                   | 偵測特定駭客工具或其功能（如 Mimikatz） |
| DML-2    | Host & Network Artefacts（工件）| 偵測終端與網路端產生的異常事件（如異常網連、可疑檔案產生） |
| DML-1    | Atomic Indicators（原子指標）   | 使用 IP、Domain、Hash 等 IOC 資料比對 |
| DML-0    | None（無）                      | 未建立任何偵測與回應機制 |

📌 **核心觀念：** 成熟度不在於情報收集量，而在於是否能落地應用於「偵測與回應」。

<p align="left">
  <img src="/rooms/images/22_07.png" width="600">
</p>

---

✅ DML 模型用途（原始提出目的）
- 提供統一的術語（lexicon），讓威脅情報溝通更清晰。
- 評估針對特定威脅行為者的偵測成熟度。
- 評估供應商產品的偵測能力。
- 協助在 Yara、Snort、SIEM 規則中標註偵測層級，給分析師上下文參考。

>> #### Task 6：偵測實作

依題目給予 ADS 框架，作答該策略分類為何？

<p align="left">
  <img src="/rooms/images/22_08.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/22_09.png" width="600">
</p>

下列何者包含於「策略摘要」中？

<p align="left">
  <img src="/rooms/images/22_10.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/22_11.png" width="600">
</p>

下列何者包含於「回應計劃」中？

<p align="left">
  <img src="/rooms/images/22_12.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/22_13.png" width="600">
</p>

獲得 Flag 🎉🎉

<p align="left">
  <img src="/rooms/images/22_14.png" width="600">
</p>

##### 🔐 答題：
1. What is the flag?  
   
   旗幟是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{Sup3r-D3t3ct1v3}`