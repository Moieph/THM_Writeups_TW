# Governance & Regulation  





<!--**📝️ 治理與監管**

THM路徑：https://tryhackme.com/room/cybergovernanceregulation

>> #### Task 1：介紹

>> #### Task 2：為什麼它很重要？

**資訊安全法規(Information Security Regulations)：**

所有產業（金融、醫療、政府、製造）中，只要涉及個人資料（PII），都必須遵守隱私與資料保護法規，以保護民眾資料、維護信任並符合合規要求。

法規是一種外部強制規範，要求組織必須在資訊保護上達到最低標準。

---
🌍常見國際資訊安全法規與標準：

|法規名稱 | 領域 | 說明 |
|-|-|-|
|GDPR |個資保護  | 歐盟法規，規範企業如何蒐集、儲存與處理歐盟公民的個人資料   |
|HIPAA| 醫療 | 美國法案，要求醫療資料處理者保護病患資訊    |
|PCI-DSS|金融支付| 處理信用卡資訊的技術與作業要求，避免持卡人資料洩漏      |
|GLBA|金融| 金融業者需保護顧客的非公開個資（NPI），並說明資料分享方式 |

##### 🔐 答題：
1. A rule or law enforced by a governing body to ensure compliance and protect against harm is called?
   
   由管理機構執行的規則或法律以確保合規性和防止傷害被稱為？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Regulation`
 
2. Health Insurance Portability and Accountability Act (HIPAA) targets which domain for data protection?
   
   健康保險流通與責任法案 （HIPAA） 針對哪個域進行數據保護？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Healthcare`

>> #### Task 3：資訊安全架構
一套有系統的文件規範與制度框架，用來指導組織如何規劃、執行與強化資安措施。


- 資訊安全文件（策略性與管理性）<br> Information Security Documents
  - 五大類型
  
    | 文件類型           | 定義       | 說明與舉例               |
    |----------------|----------|---------------------|
    | 政策（Policies）   | 目標與原則性聲明 | 例：密碼政策、遠端存取政策       |
    | 標準（Standards）  | 強制性技術規範  | 例：最低密碼長度為 12 字元     |
    | 指引（Guidelines） | 最佳建議、非強制 | 例：建議定期更換 Wi-Fi 密碼   |
    | 程序（Procedures） | 明確操作步驟   | 例：資安事件通報流程 SOP      |
    | 基線（Baselines）  | 最低安全門檻   | 例：所有伺服器必須啟用防火牆與日誌紀錄 |
- 撰寫資安治理文件（技術性與流程性）
  - 六大步驟
  
    |步驟 | 說明與舉例 |
    |-|-|
    |1. 確定範圍與目的 |例：密碼政策目的是提升密碼強度，防止帳號被竊取 |
    |2. 法規與業界調研| 參考 GDPR、NIST、ISO 27001 等標準  |
    |3. 撰寫草稿與設計架構|條文要明確、可執行、符合組織價值  |
    |4. 內部審查與核准| 法務、資安部門、高層管理共同審閱|
    |5. 宣導與落實推行| 對員工做教育訓練與角色責任說明 |
    |6. 定期檢討與更新|配合威脅變化或法規調整修正內容 |

<hr>

- 是否都要自己編寫這些文件？<br>
❌ 不一定。有些組織會直接採用現成業界標準
- 選擇適用框架的考量因素：
    1. 法規需求（依地區與產業）
    2. 組織目標與資訊敏感度
    3. 可用資源與專業人力
    4. 威脅情境與風險型態

##### 🔐 答題：
1. The step that involves monitoring compliance and adjust the document based on feedback and changes in the threat landscape or regulatory environment is called?
   
   涉及監控合規性並根據威脅態勢或監管環境的反饋和變化調整文檔的步驟稱為？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Review and update`

2. A set of specific steps for undertaking a particular task or process is called?
   
   執行特定任務或過程的一組特定步驟稱為？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Procedure`

>> #### Task 4：GRC 架構

<details>
<summary><strong>G – Governance（治理）</strong></summary>
組織為達成目標、確保符合法規與標準所建立的整體結構與管理流程（由高階管理層主導）

- 包含設定：
  - 資安策略（Security Strategy）
  - 政策（Policies）
  - 標準（Standards）
  - 稽核與監測機制（Auditing & Monitoring）

📌 負責「方向與規範」的制定與推動
</details>

<details>
<summary><strong>R – Risk Management（風險管理）</strong></summary>
辨識、評估並優先處理資訊風險，目的是降低損害機率與影響

- 包含：
  - 威脅與弱點分析（Threats & Vulnerabilities）
  - 風險評估（Risk Assessment）
  - 控制措施與應變計畫（Controls & Mitigation Plan）

📌 負責「看見風險並主動處理」
</details>

<details>
<summary><strong>Compliance（合規）</strong></summary>
確保組織遵守外部法規、內部政策與產業標準

- 常見法規與標準如：
  - GDPR（一般資料保護法）
  - PCI-DSS（支付卡資料安全標準）
  - HIPAA（健康資訊保護法）


- 包含：
  - 稽核（Audit）
  - 報告（Reporting）
  -改進措施（Corrective Actions）

📌 負責「有沒有做到、做得夠好」
</details>

---
**建立 GRC 架構的七大步驟：**

| 步驟      | 說明與舉例                                                                 |
|---------|---------------------------------------------------------------------------|
| 1. 定義目標與範圍 | 例：針對客戶資料系統建立 GRC，目標：12 個月內資安風險降低 50%             |
| 2. 執行風險評估 | 例：發現弱密碼政策、舊版軟體 → 優先強化存取控制與漏洞修補                  |
| 3. 制定政策與程序 | 例：強制使用強密碼、建立登入記錄機制、防止未授權存取                        |
| 4. 建立治理流程 | 例：組成資安委員會、定期檢討資安投資、定義角色與職責                         |
| 5. 實施控制措施 | 例：部署防火牆、IPS、IDS、SIEM 系統；舉辦員工資安訓練                         |
| 6. 監測與績效衡量 | 例：追蹤政策遵循率、KPI 指標、資安事件回報率                                |
| 7. 持續改進 | 例：資安事件後進行原因分析與對策更新，提升應變能力                         |

---
**GRC 實務範例：金融業的應用**

| 組件              | 實務做法                                                                 |
|-------------------|--------------------------------------------------------------------------|
| Governance        | 指派治理高層，制定銀行保密法、洗錢防制政策、財報規範等                      |
| Risk Management   | 辨識金融詐騙風險：如釣魚詐騙、假 ATM 卡、帳戶被盜用                         |
| Compliance        | 遵守 PCI-DSS、GLBA；採用 TLS、更新系統、做使用者教育防釣魚                 |


##### 🔐 答題：
1. What is the component in the GRC framework involved in identifying, assessing, and prioritising risks to the organisation?
   
   GRC 框架中涉及識別 、評估和確定組織風險優先順序的哪些組成部分？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Risk Management`

2. Is it important to monitor and measure the performance of a developed policy?  (yea/nay)
   
   監控和衡量已制定策略的績效是否重要？（是/否）
   
&nbsp;&nbsp;&nbsp;&nbsp; `yea`

>> #### Task 5：隱私和數據保護

<details>
<summary><strong>General Data Protection Regulation（GDPR）</strong></summary>

| 項目        | 說明                                                                 |
|-------------|----------------------------------------------------------------------|
| 📍 出處/國家 | 歐盟（EU）                                                           |
| 📅 上路時間  | 2018 年 5 月                                                         |
| 🎯 核心目的  | 保護所有歐盟居民的「個人資料（PII）」，防止未經同意的蒐集、處理、外洩           |

---
- GDPR 核心規定重點：
    1. 蒐集前需取得明確同意（明示同意，不可預設打勾）
    2. 個資最小化原則：只能蒐集業務所需的最少資料
    3. 儲存需有保護機制：採用加密、防火牆等資安措施
    4. 必須告知資料用途與處理方式
    5. 允許資料主體行使權利：查詢、更正、刪除、拒絕被處理
---
⚖️ GDPR 罰則機制（二層級）：


| 等級               | 違規情況                                             | 最高罰金                          |
|--------------------|------------------------------------------------------|-----------------------------------|
| Tier 1（重大違規） | 未經同意蒐集、非法分享、處理敏感資料等                  | 4% 營收 or €2000 萬（擇高）        |
| Tier 2（一般違規） | 遲未通報資安事件、缺乏資安政策                          | 2% 營收 or €1000 萬（擇高）        |

</details>

<details>
<summary><strong>Payment Card Industry Data Security Standard（PCI DSS）</strong></summary>

| 項目          | 說明                                                                 |
|---------------|----------------------------------------------------------------------|
| 📍 出處/制定者 | 信用卡產業安全標準協會（由 Visa、MasterCard 等主導）                   |
| 🎯 核心目的    | 保護信用卡資料（Cardholder Data），防止盜刷與資料外洩                   |
| 🌐 適用對象    | 所有處理、儲存、傳輸信用卡資料的實體與線上商家                            |

---
- PCI DSS 核心要求：
    1. 限制資料存取權限（最小權限原則）
    2. 建置防火牆與入侵防禦系統（IPS）
    3. 對敏感資料加密儲存與傳輸
    4. 定期監控與日誌審核
    5. 維護資訊安全政策
    6. 定期進行漏洞掃描與資安測試

</details>

##### 🔐 答題：
1. What is the maximum fine for Tier 1 users as per GDPR (in terms of percentage)?
   
   根據 GDPR 對第 1 層違規者的最高罰款是多少（以百分比表示）？
   
&nbsp;&nbsp;&nbsp;&nbsp; `4`

1. In terms of PCI DSS, what does CHD stand for?
   
   就 PCI DSS 而言，CHD 代表什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `cardholder data`

>> #### Task 6：NIST 資安指南（保護CIA）

<details>
<summary><strong>NIST SP 800-53：資安與隱私控制標準</strong></summary>

| 項目       | 說明                                                                                                  |
|------------|-------------------------------------------------------------------------------------------------------|
| 📍 全名     | Security and Privacy Controls for Information Systems and Organizations                              |
| 🏛️ 發布單位 | 美國國家標準與技術研究院（NIST）                                                                     |
| 🎯 目的     | 提供保護 CIA（機密性、完整性、可用性）的控制清單，建立組織資訊系統與隱私的安全防線                   |
| 📋 架構     | 控制項分為 20 大類（控制家族），涵蓋全面性風險，包括：駭客攻擊、人為錯誤、天災、間諜、系統故障等      |

---
**Key Points  要點：**

<p align="left">
  <img src="/rooms/images/06_01.png" width="600">
</p>

---
**PM：Program Management**

<p align="left">
  <img src="/rooms/images/06_02.png" width="600">
</p>

---

**NIST 800-53 實施建議：**

| 步驟 | 實施建議與說明                                                                 |
|------|--------------------------------------------------------------------------------|
| 1️⃣   | 盤點資料與系統資產：確認哪些資料與系統需要受到保護                            |
| 2️⃣   | 對應控制家族與風險：找出相對應的控制項（如 AC、IR）來處理已識別的風險          |
| 3️⃣   | 建立治理架構與角色責任：清楚界定誰負責何事                                     |
| 4️⃣   | 持續監控與稽核：定期測試與追蹤控制實施成效                                     |
| 5️⃣   | 回饋與改進：根據漏洞、事件與法規調整控制措施                                  |

---

<p align="left">
  <img src="/rooms/images/06_03.png" width="600">
</p>

</details>

<details>
<summary><strong>NIST 800-63B：數位身份驗證指南</strong></summary>



| 項目       | 說明                                                                                      |
|------------|---------------------------------------------------------------------------------------------|
| 📍 全名     | Digital Identity Guidelines – Authentication and Lifecycle Management                     |
| 🎯 目的     | 提供「使用者身份驗證」的標準作法，包括：帳號驗證、憑證管理、多因素驗證（MFA）等             |
| 🌐 覆蓋範圍 | 各層級身份信任程度（LOA）、密碼要求、生物辨識與一次性密碼（OTP）等方式的應用規範             |

</details>

---

🔍NIST 800-53 vs 800-63B 差異比較

| 比較項目   | NIST 800-53                           | NIST 800-63B                            |
|------------|----------------------------------------|-----------------------------------------|
| 用途       | 建立整體資安與隱私控制架構            | 建立數位身份認證與帳號保護機制         |
| 核心對象   | 資訊系統、資安控制、風險管理          | 個人用戶、帳號登入、安全驗證           |
| 代表控制項 | 存取控制、稽核、事件回應、設定管理等  | 密碼政策、多因素驗證、生物識別、OTP     |

##### 🔐 答題：
1. Per NIST 800-53, in which control category does the media protection lie?
   
   根據 NIST 800-53，媒體保護屬於哪個控制類別？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Physical`

2. Per NIST 800-53, in which control category does the incident response lie?
   
   根據 NIST 800-53，事件回應屬於哪個控制類別？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Administrative`

3. Which phase (name) of NIST 800-53 compliance best practices results in correlating identified assets and permissions?
   
   NIST 800-53 合規性最佳實踐的哪個階段（名稱）會導致將已識別的資產和許可權相關聯？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Map`

>> #### Task 7：資訊安全管理與合規
Information Security Management and Compliance

<details>
<summary><strong>ISO/IEC 27001：國際資訊安全管理標準</strong></summary>

| 項目         | 說明                                                                 |
|--------------|----------------------------------------------------------------------|
| 📍 發布機構   | ISO（國際標準組織）與 IEC（國際電工委員會）                                 |
| 📋 全名       | Information Security Management System（ISMS）                        |
| 🎯 目標       | 建立、執行、維運與持續改善資訊安全管理系統                                |
| 🔐 保護範疇   | 組織所有資訊資產（不限於 IT 資料）                                      |
| 🌍 適用產業   | 全球各產業皆適用，尤其是處理大量資料的企業                                |
| 📄 文件結構   | 標準需付費購買，內容包含範圍定義、風險管理、審核與改善等                    |

---

**ISO 27001 核心要素 ：**

| 中文名稱         | 英文原名                            | 簡要說明                                                 |
|------------------|--------------------------------------|----------------------------------------------------------|
| 範圍定義         | Scope                                | 定義 ISMS 的範圍，包括涵蓋的資產與流程                     |
| 資訊安全政策     | Information security policy           | 組織在資訊安全上的高層級方針文件                           |
| 風險評估         | Risk assessment                       | 評估資訊在機密性、完整性與可用性上的風險                  |
| 風險處理         | Risk treatment                        | 採取控制措施將風險降至可接受程度                          |
| 適用聲明         | Statement of Applicability (SoA)      | 說明哪些控制項適用、哪些不適用                            |
| 內部稽核         | Internal audit                        | 定期稽核 ISMS，確保其有效運作                              |
| 管理審查         | Management review                     | 高階管理層定期檢討 ISMS 執行成效                           |

<p align="left">
  <img src="/rooms/images/06_04.png" width="600">
</p>

</details>

<details>
<summary><strong>SOC 2：服務組織資訊保護審核框架</strong></summary>

| 項目         | 說明                                                                 |
|--------------|----------------------------------------------------------------------|
| 📍 發布機構   | AICPA（美國註冊會計師協會）                                              |
| 📋 全名       | Service Organization Control 2                                       |
| 🎯 目標       | 審查服務商是否具備足夠的控制措施來保護客戶資料                          |
| 📑 核心特色   | 屬於審計報告，不屬於標準化規範                                         |
| 🌍 適用對象   | 提供 SaaS、雲端、金融、醫療等服務的供應商                              |

---

- SOC 2 核心五大原則（可選適用）： 

| 原則                   | 說明                                                             |
|------------------------|------------------------------------------------------------------|
| Security（必選）        | 控制未授權存取（如防火牆、存取權限等）                            |
| Availability           | 系統可用性、故障容忍、備援能力等                                  |
| Processing Integrity   | 處理的準確性與完整性                                              |
| Confidentiality        | 敏感資料的加密與存取控制                                           |
| Privacy                | 個人資料的保護與合規使用                                           |

---

- 🔍 SOC 2 審計流程（企業要做的事）：
1. **定義範圍：** 確認需納入審計的系統/服務/位置
2. **選擇審核員：** 找有 SOC 2 經驗的 CPA 審核公司
3. **審核前準備：** 補強資安政策、控制流程、權限配置
4. **正式審核：** 測試控制項、訪談員工、文件查核
5. **獲得報告：** 審核結果、問題點與改善建議可提供客戶參考

---

<p align="left">
  <img src="/rooms/images/06_05.png" width="600">
</p>

</details>

---

🔍ISO 27001 vs SOC 2 差異比較表

| 項目                 | ISO 27001                                 | SOC 2                                      |
|----------------------|--------------------------------------------|--------------------------------------------|
| 發布單位             | ISO / IEC                                  | AICPA（會計師協會）                        |
| 性質                 | 標準（可認證）                              | 審計報告（無認證）                          |
| 是否付費             | 是（購買官方標準）                          | 審計服務需委託，報告內容不公開              |
| 評估對象             | 組織整體資訊安全管理架構                    | 控制措施是否落實，與五大信任原則對應        |
| 國際認可度           | 高（全球皆適用）                            | 主要在北美或與美國客戶合作時要求            |
| 誰最常要求企業實施   | 國際供應鏈、大型跨國企業                     | 客戶（尤其是使用雲端服務者）                 |

##### 🔐 答題：
1. Which ISO/IEC 27001 component involves selecting and implementing controls to reduce the identified risks to an acceptable level?
   
   哪個 ISO/IEC 27001 組成部分涉及選擇和實施控制措施，以將已識別的風險降低到可接受的水準？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Risk treatment`

2. In SOC 2 generic controls, which control shows that the system remains available?
   
   在 SOC 2 通用控制措施中，哪個控制措施顯示系統仍然可用？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Availability`

>> #### Task 8：結論

| 題目                        | 解答                          |
|---------------------------|-----------------------------|
| Phishing Emails           | User Awareness              |
| Man in the Middle Attack  | Secure connection (SSL/TLS) |
| Unregulated/Non Compliant | SOC 2                       |
| Unpatched Software        | Automatic patch management  |
| Data Leakage (EU)         | GDPR                        |

<p align="left">
  <img src="/rooms/images/06_06.png" width="600">
</p>

Question 1 ：下列哪一項是資訊系統和組織的安全和隱私控制的有效 NIST 出版品？
<p align="left">
  <img src="/rooms/images/06_07.png" width="600">
</p>

Question 2 ： 下列哪一個架構主要協助資訊安全管理和合規性？
<p align="left">
  <img src="/rooms/images/06_08.png" width="600">
</p>

獲得 Flag 🎉🎉
<p align="left">
  <img src="/rooms/images/06_09.png" width="600">
</p>

##### 🔐 答題：
1. Click the View Site button at the top of the task to launch the static site in split view. What is the flag after completing the exercise?
   
   按兩下任務頂部的 View Site 按鈕，以在分割檢視中啟動靜態網站。完成練習后的旗幟是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{SECURE_1001}`
