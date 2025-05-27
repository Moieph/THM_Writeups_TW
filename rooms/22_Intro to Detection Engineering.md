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
🧭 步驟一：**威脅建模（Threat Modelling）**

| 模式               | 說明                                                                 |
|--------------------|----------------------------------------------------------------------|
| 被動式（Reactive） | 回顧近期內部資安事件報告，找出曾遺漏的偵測機制                      |
| 主動式（Proactive）| 結合 MITRE ATT&CK + 情資來源，預測對手可能的 TTPs，事先設計偵測規則 |

✅ 注意：此處「建模」不同於前面提到的偵測類型 Modelling，這裡偏向攻擊面風險評估。

---
🧭 步驟二：**資料來源識別與日誌蒐集（Datasource & Logging）**

>> #### Task 4：偵測工程框架 1

>> #### Task 5：偵測工程框架 2

>> #### Task 6：偵測實作