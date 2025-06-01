# Red Team Engagements

**🟥 紅隊演練**

THM路徑：https://tryhackme.com/room/redteamengagements

---

>> #### Task 1：介紹

📌 常見的紅隊演練類型（Types of Engagements）

| 類型                      | 說明                                 |
| ----------------------- | ---------------------------------- |
| **Tabletop Exercises**  | 桌面模擬，針對特定威脅場景進行策略討論與決策演練（無實際攻擊）    |
| **Adversary Emulation** | 模擬特定攻擊者（如 APT）完整的 TTPs，測試組織偵測與回應能力 |
| **Physical Assessment** | 針對實體環境進行評估，如社交工程、門禁入侵、實體資產存取測試     |


>> #### Task 2：定義範圍和目標

📘 **Red Team Engagement**：目標設定與範疇界定

---

🎯 **清晰的客戶目標（Client Objectives）**
- 客戶目標是整個紅隊行動的基石。
- 目標應由 **紅隊與客戶雙方共同討論**，確保理解一致、期待一致。
- 若無具體目標，整場 Engagement 將 **缺乏結構與規劃**，容易失控或無效。


🧩 客戶目標的功能：
- 設定行動的主軸與節奏
- 奠定文件撰寫與規劃基礎
- 影響後續的 **規則制定（Rules of Engagement） 與 範疇定義（Scope）**

---

⚔️ Engagement 形式分類

| 分類                          | 說明                                          |
| --------------------------- | ------------------------------------------- |
| 一般滲透測試（Penetration Test）    | 著重於測試內部/網路系統弱點，通常較廣泛、不特定對象，使用通用 TTPs。       |
| 特定對手模擬（Adversary Emulation） | 根據客戶所屬產業（如金融業）模擬特定 APT（如 APT38）行為，目標與技術更聚焦。 |

📌 選擇哪種形式，需依照「客戶目標」與資源決定。

---

🧾 Engagement 範疇（Scope）

- **Scope 是「你能做／不能做」的範圍**，應由 **客戶設定**，紅隊僅可建議或提出爭議。


常見條款範例：

````
- 不得進行資料外洩行為（No exfiltration of data）
- 不可觸碰正式環境伺服器（Production servers are off-limits）
- 子網段 10.0.3.8/18 為不可攻擊目標（Out of Scope）
- 子網段 10.0.0.8/20 為可測試目標（In Scope）
- 不可造成任何系統停機（No system downtime）
- 嚴禁外洩任何 PII 資料（PII exfiltration prohibited）
````

---

🔍  紅隊角度的分析要點

- **動態解讀客戶目標與範疇**，思考若你是攻擊者該如何規劃行動。
- 即便只有目標與範疇，也要能根據這些資訊推導出自己的 **Engagement Plan 行動計畫草案**。
- 若 Scope 不合理，也可由紅隊提出協商建議。

---

🧠 總結流程圖：

````
1️⃣ 客戶目標（Client Objectives）
     ↓
2️⃣ Engagement 類型判定（PT / Emulation）
     ↓
3️⃣ 紅隊策略與資源規劃
     ↓
4️⃣ 客戶設定範疇（Scope）
     ↓
5️⃣ 撰寫 Engagement Plan（行動計畫書）
````
---
閱讀題旨並依序作答

<p align="left">
  <img src="/rooms/images/29_01.png" width="600">
</p>

---

##### 🔐 答題：
2. What CIDR range is permitted to be attacked?
   
   允許攻擊的 CIDR 範圍是多少？    
   
&nbsp;&nbsp;&nbsp;&nbsp; `10.0.4.0/22`

3. Is the use of white cards permitted? (Y/N)
   
   允許使用白卡嗎？（是/否）    
   
&nbsp;&nbsp;&nbsp;&nbsp; `Y`

4. Are you permitted to access "*.bethechange.xyz?" (Y/N)
   
   您是否允許訪問 「*.bethechange.xyz？（是/否）
   
&nbsp;&nbsp;&nbsp;&nbsp; `N`

>> #### Task 3：交戰規則

📄 **紅隊演練規則**（Rules of Engagement，RoE）

- RoE 是一份 **具有法律效力的正式文件**，明確記錄紅隊與客戶雙方的行動範圍與權責。
- 通常為第一份進入規劃階段的正式文件。
- 涵蓋：**客戶目標、行動範圍、技術限制、責任分工、聯絡窗口、雙方授權**。
- 通常會搭配 **外部合約或 NDA（保密協議）** 使用。

---

📑 RoE 標準章節結構（依 redteam.guide 整理）

| 區塊名稱                                                    | 說明                                    |
| ------------------------------------------------------- |---------------------------------------|
| **Executive Summary**（執行摘要）                             | 概要說明文件內容與授權範圍。                        |
| **Purpose**（目的）                                         | 定義 RoE 文件存在的理由。                       |
| **References**（參考標準）                                    | 如 HIPAA、ISO 27001 等引用依據。              |
| **Scope**（範疇）                                           | 明確記錄可攻擊與不可攻擊的範圍（如 IP、系統、時段）。          |
| **Definitions**（術語定義）                                   | 解釋文件中會用到的專業術語。                        |
| **Rules of Engagement & Support Agreement**（雙方義務與支持條款）  | 定義雙方技術與行政責任，例如：資源協助、事前溝通流程等。          |
| **Provisions**（補充條款）                                    | 增補或例外事項，如臨時許可、特定通道白名單等。               |
| **Requirements, Restrictions & Authority**（紅隊要求與限制）     | 紅隊操作的具體授權與操作限制（例如不得使用 DoS、不可破壞資料）。    |
| **Ground Rules**（基本限制規則）                                | 明確限制紅隊互動方式，如社工不能打擾實體工作人員。             |
| **Resolution of Issues / Points of Contact**（聯絡窗口與問題處理） | 所有關鍵聯絡人與問題升級機制（客戶聯絡人 / 紅隊指揮官 / 白隊裁判）。 |
| **Authorization**（授權聲明）                                 | 客戶明確授權紅隊執行該 Engagement 的聲明。           |
| **Approval**（雙方簽署）                                      | 客戶與紅隊雙方正式簽署同意，具有法律效力。                 |
| **Appendix**（附錄）                                        | 附加補充資訊、圖表、背景資料等。                      |

---

📌 注意事項
- RoE 不是完整行動規劃，而是 **法律框架與合作條件**。
- 真正的技術細節與階段任務會在後續的 **Engagement Plan（行動計畫書）** 中補充。
- 需確保所有條文都具備明確性與可執行性，避免產生解釋歧義。

---


閱讀題旨下載 ROE 文件，閱讀並回答題目

<p align="left">
  <img src="/rooms/images/29_01.png" width="600">
</p>



---

##### 🔐 答題：
2. How many explicit restriction are specified?
   
   指定了多少個顯式限制？   
   
&nbsp;&nbsp;&nbsp;&nbsp; `3`

3. What is the first access type mentioned in the document?
   
   文件中提到的第一種訪問類型是什麼？    
   
&nbsp;&nbsp;&nbsp;&nbsp; `Phishing`

4. Is the red team permitted to attack 192.168.1.0/24? (Y/N)
   
   紅隊可以攻擊 192.168.1.0/24 嗎？（是/否） 
   
&nbsp;&nbsp;&nbsp;&nbsp; `N`

>> #### Task 4：活動策劃

🧠 從「商業規劃」進入「技術行動」：紅隊活動的 4 種核心計畫（Campaign Planning）

- 前面談的是： 客戶目標、範圍、RoE 等「商業 / 法律層面」
- 現在要做的是： 將這些資訊 **具體轉換為技術作戰計畫與指令流程**
- 每個紅隊內部會有自己的 SOP，但以下這套是 **結合軍事作戰文件精簡化的標準架構**，適合用來撰寫、溝通與執行。

---

📊 紅隊活動的 4 大技術計畫（Campaign Plan）

| 計畫類型                       | 說明                                | 常見內容                      |
|----------------------------| --------------------------------- | ------------------------- |
| **Engagement Plan**（演練計畫）  | 技術需求總覽；是整體作戰的起點。                  | 作戰概念（CONOPS）、人力與資源配置、時間安排 |
| **Operations Plan**（作戰計畫）  | 將 Engagement Plan 拆解為具體操作細節與職責分工。 | 操作員名單、已知目標資訊、各人職責         |
| **Mission Plan**（任務計畫）     | 實際指令與執行時間表，模擬實際攻擊者步驟。             | 指令、時間目標、操作員分工             |
| **Remediation Plan**（補救計畫） | 任務完成後的處理建議與回報方式。                  | 報告範本、漏洞修補建議、協助會議流程        |


>> #### Task 5：演練計劃

🧠 Engagement Documentation 演練文件內容概覽（技術版）

- Engagement Documentation 是 **Campaign Plan 的實體化延伸**

---

📄 **Engagement Plan（演練計畫）**

| 元件                      | 說明                                     |
| ----------------------- | -------------------------------------- |
| **CONOPS（作戰概念）**        | 用非技術性的語言說明：紅隊將如何實現客戶目標、攻擊目標。適合讓業主閱讀理解。 |
| **Resource Plan（資源規劃）** | 時程、紅隊所需資源（人力、設備、雲端環境等）。這些資訊對任務成功至關重要。  |

---

📄 **Operations Plan**（作戰計畫）

| 元件                               | 說明                           |
|----------------------------------| ---------------------------- |
| **Personnel（人員配置）**              | 任務所需的成員、職位與技能。               |
| **Stopping Conditions（中止條件）**    | 遇到哪些情況要中止？如：觸發防禦、影響業務等。      |
| **RoE（Optional）**                | 可以複製或簡化 RoE 的關鍵條款，用來提醒技術執行者。 |
| **Technical Requirements（技術需求）** | 為了成功完成任務，紅隊需具備的知識、技能或先備資訊。   |

---

📄 **Mission Plan**（任務計畫）

| 元件                         | 說明                                   |
| -------------------------- | ------------------------------------ |
| **Command Playbooks（Optional）**  | 寫出具體的指令、工具、執行時機與原因。適用於大隊伍、有新手或複雜行動時。 |
| **Execution Times（執行時程）**  | 不只起始時間，也可能規範某個工具何時執行、持續多久。           |
| **Responsibilities（任務分工）** | 誰負責哪段流程與任務，避免重疊與疏漏。                  |

---

📄 **Remediation Plan**（補救計畫，Optional）

| 元件                                   | 說明                               |
| ------------------------------------ | -------------------------------- |
| **Report（報告）**                       | 總結活動成果、發現的問題與漏洞報告。               |
| **Remediation / Consultation（補救建議）** | 提出修補建議，或與客戶召開修復協調會議。可併入報告中或另行進行。 |


>> #### Task 6：作戰構想

✅ CONOPS （作戰概念）的核心精神

&nbsp;&nbsp;&nbsp;&nbsp;_「寫給不懂技術的客戶，但又不能太空泛。」_ <br>

- 給 **客戶 / 業主** 一個清晰、無需技術背景就能理解的計畫概要
- 給 **紅隊成員** 一個統整概覽，作為後續 Campaign 計畫的基礎文件

---

📄 CONOPS 應包含的關鍵要素

| 項目                                       | 說明                                               |
| ---------------------------------------- | ------------------------------------------------ |
| **Client Name（客戶名稱）**                    | 公司或組織名稱                                          |
| **Service Provider（紅隊執行單位）**             | 紅隊服務提供者                                          |
| **Timeframe（測試時程）**                      | 例如：2025/06/01 \~ 2025/06/14                      |
| **General Objectives / Phases（總目標與階段）**  | 例如：模擬外部駭客滲透、內部橫向移動、無檔案持久化等                       |
| **Other Training Objectives（附加訓練目標）**    | 如模擬資料外洩 (exfiltration)、側錄指令等                     |
| **High-Level Tools/Techniques（高階工具與技巧）** | 不需太細，但可以列：如使用 Cobalt Strike、OSINT、Spear Phishing |
| **Threat Group to Emulate（模擬對象的威脅組織）**   | 如：APT38、Lazarus Group（如果適用）                      |

範例：

````
# CONOPS - Concept of Operations

## Client Name
ACME Financial Corporation

## Service Provider
FH Cyber Red Team Unit

## Timeframe
June 1st, 2025 – June 14th, 2025

## General Objectives / Phases
- Assess perimeter defenses through external adversary emulation
- Gain internal access and simulate lateral movement
- Assess incident response readiness of Blue Team

## Other Training Objectives
- Simulate data exfiltration without triggering detection
- Test endpoint resilience against known attack techniques

## High-Level Tools / Techniques
- Open-source reconnaissance (OSINT)
- Spear phishing (custom payloads)
- Cobalt Strike for command and control
- Mimikatz for credential harvesting

## Threat Group to Emulate
APT38 – a financially motivated North Korean state-sponsored group known for targeting banking infrastructure
````

---

閱讀題旨並依序作答

<p align="left">
  <img src="/rooms/images/29_03.png" width="600">
</p>

---

##### 🔐 答題：
3. How long will the engagement last?
   
   參與將持續多長時間？   
   
&nbsp;&nbsp;&nbsp;&nbsp; `1 Month`

4. How long is the red cell expected to maintain persistence?
   
   紅細胞預計能維持多長時間？    
   
&nbsp;&nbsp;&nbsp;&nbsp; `3 Weeks`

5. What is the primary tool used within the engagement?
   
   參與中使用的主要工具是什麼？   
   
&nbsp;&nbsp;&nbsp;&nbsp; `Cobalt Strike`

>> #### Task 7：資源計劃

✅ Resource Plan 的核心精神

&nbsp;&nbsp;&nbsp;&nbsp;_直接、明確、可執行，不要像 CONOPS 一樣敘述，要用清單方式列出。_ <br>

---

📄 Resource Plan 範本架構

````
# Resource Plan

## Header
- Engagement Resource Plan – ACME Financial Corporation
- Drafted by: Red Team Lead – FH Cyber
- Date: 2025/05/20

## Customer
- ACME Financial Corporation

---

## Engagement Timeline

- **Engagement Period**: 2025/06/01 ~ 2025/06/14
- **Reconnaissance Phase**: 2025/06/01 ~ 2025/06/02
- **Initial Compromise**: 2025/06/03 ~ 2025/06/06
- **Post-Exploitation & Persistence**: 2025/06/07 ~ 2025/06/12
- **Reporting & Remediation**: 2025/06/13 ~ 2025/06/14

---

## Knowledge Required (Optional)

### Reconnaissance
- OSINT collection (social media, domain intel)
- Passive subdomain enumeration (Amass, Sublist3r)

### Initial Compromise
- Spear phishing techniques
- Payload generation (Cobalt Strike, msfvenom)

### Post-Exploitation
- Credential dumping (Mimikatz)
- Lateral movement (WMI, PSExec)
- Persistence techniques (Registry, Scheduled Tasks)

---

## Resource Requirements

### Personnel
- 1x Red Team Lead
- 1x Operator (Phishing & Payload)
- 1x Operator (Lateral Movement & Persistence)
- 1x Report Writer

### Hardware
- 2x Kali Linux laptops
- 1x VPN Gateway Server
- 1x Dedicated C2 Server

### Cloud
- 1x AWS EC2 instance (for redirector)
- 1x DigitalOcean droplet (for phishing site hosting)

### Miscellaneous
- Custom phishing domain
- Pre-approved C2 IP whitelist
- Internal test accounts (provided by client)
````

---

依題旨點擊 `View site`

<p align="left">
  <img src="/rooms/images/29_04.png" width="600">
</p>


---

##### 🔐 答題：
2. When will the engagement end? (MM/DD/YYYY)
   
   演練何時結束？（MM/DD/YYYY）  
   
&nbsp;&nbsp;&nbsp;&nbsp; `11/14/2021`

3. What is the budget the red team has for AWS cloud cost?
   
   紅隊的 AWS 雲成本預算是多少？   
   
&nbsp;&nbsp;&nbsp;&nbsp; `$1000`

4. Are there any miscellaneous requirements for the engagement? (Y/N)
   
   參與是否有任何其他要求？（是/否）  
   
&nbsp;&nbsp;&nbsp;&nbsp; `N`


>> #### Task 8：作戰計畫

>> #### Task 9：任務計劃

>> #### Task 10：結論