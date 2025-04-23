# Governance & Regulation  
**📝️ 治理與監管**

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


- 資訊安全文件（策略性與管理性） Information Security Documents
  - 五大類型
    - | 文件類型           | 定義       | 說明與舉例               |
      |----------------|----------|---------------------|
      | 政策（Policies）   | 目標與原則性聲明 | 例：密碼政策、遠端存取政策       |
        | 標準（Standards）  | 強制性技術規範  | 例：最低密碼長度為 12 字元     |
        | 指引（Guidelines） | 最佳建議、非強制 | 例：建議定期更換 Wi-Fi 密碼   |
        | 程序（Procedures） | 明確操作步驟   | 例：資安事件通報流程 SOP      |
        | 基線（Baselines）  | 最低安全門檻   | 例：所有伺服器必須啟用防火牆與日誌紀錄 |
- 撰寫資安治理文件（技術性與流程性）
  - 六大步驟
    - |步驟 | 說明與舉例 |
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


<!--<details>
<summary><strong>1️⃣ 真實性（Authenticity）</strong></summary>

- <strong>定義</strong>：Authentic 意指「非偽造、非虛假」。
- <strong>說明</strong>：真實性是指資料、文件或檔案確實來自聲稱的來源，而非被偽造或中途竄改。
- ✅ 目的是確保來源的可信度與內容的正當性。

</details>

<details>
<summary><strong>2️⃣ 不可否認性（Nonrepudiation）</strong></summary>

- <strong>定義：</strong>Repudiate 表示「否認、拒絕承認」。 Nonrepudiation 則是防止這種否認發生。
- <strong>說明：</strong>不可否認性是指發送者無法否認其曾經傳送過某個文件或資料，確保事後責任歸屬清晰。
- 🔐 對於線上交易、病患診斷記錄、銀行轉帳等場景，這項特性非常關鍵。

</details>

真實性與不可否認性也是資安設計中不可忽略的重要層面，確保每一筆資料都 **「可信、可驗證、可追溯」**。

---

<details>
<summary><strong>3️⃣ 效用性（Utility）</strong></summary>

- <strong>定義：</strong>效用性是指資訊的實用價值是否仍然存在。
- <strong>說明：</strong>使資訊仍在、也可存取，但如果無法理解或使用，則等同於失去效用。
- <strong>🔐 如：</strong>使用者遺失了解密金鑰，雖然筆電與硬碟仍在，也無法使用裡面的加密資料，該資訊即喪失效用（utility lost）。

</details>

<details>
<summary><strong>4️⃣ 擁有權（Possession）</strong></summary>

- <strong>定義：</strong>擁有權是指資訊的實體控制權是否仍掌握在合法擁有者手中。
- <strong>說明：</strong>即便資料未被刪除或竄改，只要落入未授權者手中，也等同於失去對該資料的控制。
- <strong>🧨 例如：</strong>
  - 攻擊者偷走備份硬碟 → 我們失去資訊的實體控制。
  - 勒索軟體加密資料 → 雖資料仍在，我們卻無法使用，亦屬「擁有權喪失」。

</details>

---

💭 以下題目為隨機出現：

Q1：在警察檢查站，警察懷疑車輛登記文件為假。該員警認為缺少哪項安全功能？
<p align="left">
  <img src="/rooms/images/05_02.png" width="600">
</p>

Q2：一家飯店強調其 WiFi 網路每週 7 天、每天 24 小時均可連線。飯店重視哪個安全功能？
<p align="left">
  <img src="/rooms/images/05_03.png" width="600">
</p>

Q3：你去兌現一張支票，銀行出納員讓你等了五分鐘，為了確認支票簽發人的簽名。銀行櫃員正在檢查哪些安全功能？
<p align="left">
  <img src="/rooms/images/05_05.png" width="600">
</p>

Q4：指揮官強調，在任務進行期間，軍隊不應該向任何人透露他們的位置。指揮官希望擁有哪種安全功能？ 
<p align="left">
  <img src="/rooms/images/05_06.png" width="600">
</p>

Q5：兩家公司正在就某項協議進行談判；然而，他們希望對協議的細節保密。他們強調哪個安全功能？
<p align="left">
  <img src="/rooms/images/05_04.png" width="600">
</p>

獲得 Flag 🎉🎉
<p align="left">
  <img src="/rooms/images/05_07.png" width="600">
</p>

##### 🔐 答題：
1. Click on "View Site" and answer the five questions. What is the flag that you obtained at the end?
   
   查看網站並回答五個問題。你最後得到的旗幟是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{CIA_TRIAD}`

>> #### Task 3：DAD 攻擊三要素

<p align="left">
  <img src="/rooms/images/05_08.png" width="600">
</p>

1. **Disclosure（洩漏）** 是「機密性（Confidentiality）」的對立面。換句話說，機密資料遭到洩漏，就是對機密性的攻擊。
2. **Alteration（竄改）** 是「完整性（Integrity）」的對立面。如：支票的完整性極重要，一旦被篡改就無法信任
3. **Destruction / Denial（摧毀／拒絕）** 是「可用性（Availability）」的對立面。當系統或資料遭摧毀，或無法存取，即是對可用性的打擊。

##### 🔐 答題：
1. The attacker managed to gain access to customer records and dumped them online. What is this attack?
   
    攻擊者設法訪問了客戶記錄並將其轉儲到網上。這種攻擊是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Disclosure`

1. A group of attackers were able to locate both the main and the backup power supply systems and switch them off. As a result, the whole network was shut down. What is this attack?
   
    攻擊者找到主電源和備用電源系統並將其關閉。結果，整個網路都關閉了。這種攻擊是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Destruction/Denial`


>> #### Task 4：安全模型（Security Model）

<details>
<summary><strong>Bell-LaPadula 模型</strong> 「不可上讀，不可下寫」</summary>
<i>重點在「機密性 Confidentiality」</i>

- 模型目的：

    此模型的目標是透過「存取控制規則」來防止未授權使用者存取敏感資訊，確保機密性不被破壞。

1. **簡單安全性原則（Simple Security Property）**<br>
又稱：「不可向上讀」（No Read Up, NRU）<br>
規則：低安全等級的主體（Subject）不能讀取高安全等級的物件（Object）。<br>
✅ 目的：防止機密資料被低權限者讀取。

2. **星號安全性原則（Star Security Property）**<br>
又稱：「不可向下寫」（No Write Down, NWD）<br>
規則：高安全等級的主體不能寫入到低安全等級的物件。<br>
✅ 目的：避免機密資訊洩露給低權限者。

3. **任意性安全原則（Discretionary Security Property）**<br>
使用存取矩陣（Access Matrix）來控制誰能對哪些物件執行哪些操作。

- 舉例矩陣：

|  主體   | 物件 A  |  物件 B |
|-|-------|-|
|Subject 1| 寫入    |  無存取權限|
|Subject 2| 讀 / 寫 |讀取|

- 常見權限類型： 
  - Read（讀）：可以查看資源內容
  - Write（寫）：可以修改資源內容
  - Execute（執行）：可以執行程式／指令
  - Delete（刪除）：可以刪除資源
  - No Access（無權限）：禁止任何操作

---

⚠️ 模型限制：

1. Bell-LaPadula 是**針對機密性保護**設計，不處理完整性或可用性問題。
2. 不適用於**檔案共享或協作需求**，因此在現代動態資訊系統中功能有限。

</details>

<details>
<summary><strong>Biba 模型</strong> 「不可下讀、不可上寫」</summary>
<i>重點在「完整性（Integrity）」</i>

- 模型目的：

    保護資料的正確性與一致性，防止未授權的資料修改，避免資料遭竄改或污染。

1. **簡單完整性原則（Simple Integrity Property）**<br>
又稱：「不可向下讀」（No Read Down, NRD）<br>
高完整性等級的使用者不能讀取低完整性等級的資料。<br>
✅ 目的：避免信任高的人被低可信資料污染。

2. **星號完整性原則（Star Integrity Property）**<br>
又稱：「不可向上寫」（No Write Up, NWU）<br>
低完整性等級的使用者不能寫入高完整性等級的資料。<br>
✅ 目的：避免不可信使用者汙染高可信資料。

---

⚠️ 模型限制：

1. 無法處理「內部威脅（Insider Threat）」
2. 僅限完整性控制，無法**涵蓋機密性與可用性問題**
3. 在實務上不易應用於**開放協作與動態內容的系統**

</details>

<details>
<summary><strong>Clark-Wilson 模型</strong>「高度要求資料正確性、防止未授權操作」</summary>
<i>重點在「完整性（Integrity）」</i>

- 模型目的：

    確保商業環境中資料的一致性、準確性與合法修改，特別強調使用「受控程序」進行資料存取與修改。

1. **CDI（Constrained Data Item）受限資料項目**<br>
我們需要保護其完整性的資料（例如財務報表、交易紀錄）。<br>
只能透過轉換程序來操作，不可隨意存取或修改。<br>

2. **UDI（Unconstrained Data Item）非受限資料項目**<br>
非受控資料來源，例如使用者輸入、系統輸入等。<br>
需經過轉換程序處理後，才能變成 CDI。<br>

3. **TP（Transformation Procedure）轉換程序**<br>
特定編碼好的操作（如寫入、更新），必須通過授權驗證並能維護資料完整性。<br>
所有對 CDI 的變更必須透過這些程序進行。<br>

4. **IVP（Integrity Verification Procedure）完整性驗證程序**<br>
**用來檢查 CDI 是否符合預期狀態或一致性規範。** <br>
確保沒有非法改動發生。<br>


---

**核心邏輯：**<br>
不允許任何人直接操作關鍵資料（CDI）。<br>
必須透過經授權與驗證的操作流程（TP)，並配合完整性檢查 (IVP)。<br>
✅ 這種做法符合現代**企業級系統的管控流程設計**

---

舉例說明：

- 🏦 一家銀行的轉帳系統：
  - 金額資料（CDI）不得由使用者自行輸入或更改
  - 使用者輸入的資料（UDI）會經 TP 驗證與處理，若通過才能更新 CDI
  - 系統定期執行 IVP，確認帳戶餘額等資料未遭竄改

</details>

---
💭 以下題目為隨機出現：

Q1：哪個模型不能向下讀取？
<p align="left">
  <img src="/rooms/images/05_09.png" width="600">
</p>
Q2：哪個模型不能向上讀取？
<p align="left">
  <img src="/rooms/images/05_10.png" width="600">
</p>
Q3：哪個模型不能向下寫入？
<p align="left">
  <img src="/rooms/images/05_11.png" width="600">
</p>
Q4：哪個模型不能向上寫入？
<p align="left">
  <img src="/rooms/images/05_12.png" width="600">
</p>

獲得 Flag 🎉🎉
<p align="left">
  <img src="/rooms/images/05_13.png" width="600">
</p>

##### 🔐 答題：
1. Click on "View Site" and answer the four questions. What is the flag that you obtained at the end?
   
   按兩下「View Site」 並回答四個問題。你最後得到的旗幟是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{SECURITY_MODELS}`

>> #### Task 5：深度防禦（Defence-in-Depth）
深度防禦是一種資安策略，主張建立多層次的安全防線來保護系統，因此也被稱為：**✅ 多層安全（Multi-Level Security）**

這種策略不依賴單一防禦措施，而是透過「層層設防」來降低攻擊成功的機率。

>> #### Task 6：ISO/IEC 19249

**📝 五大「架構原則」（Architectural Principles）DALEV**

1. 領域分離：Domain Separation <br>
    將相關元件（資料/應用）歸為同一領域並賦予統一的安全屬性，例如 x86 中的 Ring 0 vs Ring 3。
2. 分層設計：Layering <br>
    如 OSI 七層網路模型，強調每層皆可施加安全策略，對應防禦縱深（Defence-in-Depth）概念。
3. 封裝：Encapsulation <br>
    如 OOP 中的物件封裝，透過方法（例如 API）存取資料，避免錯誤輸入與未授權存取。
4. 冗餘：Redundancy <br>
    保障可用性與完整性，例如 RAID 5、雙電源，出錯時仍能持續運作且偵測錯誤資料。
5. 虛擬化：Virtualization <br>
    透過虛擬機、雲端服務實現沙盒、安全隔離、監控惡意行為。

---

**📝 五大「設計原則」（Design Principles）LACCP**

1. 最小權限：Least Privilege   <br>
    使用者僅獲得完成任務所需的最小權限，例如只能閱讀、不能編輯。
2. 攻擊面最小化：Attack Surface Minimisation <br>
    關閉不必要服務、刪除預設帳號等，減少攻擊入口。
3. 中央化參數驗證：Centralized Parameter Validation <br>
    所有輸入都應集中驗證，防止漏洞如 RCE、DoS。
4. 中央化安全服務：Centralized General Security Services <br>
    例如集中式認證伺服器，統一管理所有安全功能。
5. 錯誤與例外處理：Preparing for Error and Exception Handling  <br>
    設計 Fail-Safe 系統，避免錯誤導致洩漏或安全破口。

##### 🔐 答題：
1. Which principle are you applying when you turn off an insecure server that is not critical to the business?
   
   當您關閉對業務不重要的不安全伺服器時，您應用了什麼原則？
   
&nbsp;&nbsp;&nbsp;&nbsp; `2`

2. Your company hired a new sales representative. Which principle are they applying when they tell you to give them access only to the company products and prices?
   
   您的公司聘請了一位新的銷售代表。當他們告訴您僅允許他們訪問公司的產品和價格時，他們應用了什麼原則？
   
&nbsp;&nbsp;&nbsp;&nbsp; `1`

3. While reading the code of an ATM, you noticed a huge chunk of code to handle unexpected situations such as network disconnection and power failure. Which principle are they applying?
   
   在閱讀 ATM 的代碼時，您注意到有一大段代碼用於處理網路斷開和電源故障等意外情況。他們應用了什麼原則？
   
&nbsp;&nbsp;&nbsp;&nbsp; `5`

>> #### Task 7：零信任 / 信任但驗證

<details>
<summary><strong>Trust but Verify（信任但驗證）</strong></summary>

<strong>核心概念：</strong>即使你信任某個人或系統，也應該設定機制來持續驗證其行為是否正常。

「信任」是一種操作上的前提，但「驗證」是一種持續性的安全行動。

- 實務方法：
  - 建立 日誌紀錄機制（logging）
  - 定期審查行為記錄（如網頁瀏覽、系統操作）
  - 搭配自動化安全工具：
    - Proxy（代理伺服器）
    - IDS（入侵偵測系統）
    - IPS（入侵防禦系統）

📌 向現實妥協式的資安策略，在不完全否定信任的情況下，強化驗證機制。

</details>

<details>
<summary><strong>Zero Trust（零信任架構）</strong></summary>

<strong>核心概念：</strong>將「信任」視為一種弱點（vulnerability）<br>「永不信任，永遠驗證（Never trust, always verify）」

- 信任不再基於：
  - 網路位置（內部 / 外部）
  - 裝置擁有權（企業電腦 vs 個人電腦）
- 所有資源存取都需：
  - 身分驗證（Authentication）
  - 權限授權（Authorization）

---

**✅  優點：**<br>
可有效防範 內部威脅（Insider Threats）。<br>
一旦發生資安事件，影響能被侷限在小區域。

---

實作關鍵技術：<br>
- 微分段（Microsegmentation）
  - 將網路劃分成極小單位（甚至是單一主機）
  - 每段之間都需進行驗證與存取控制
  - 加強內部資安隔離，減少橫向移動風險

📌 Zero Trust 是趨勢，但也需兼顧業務效率。<br>
在可行的情況下應用 Zero Trust，但不能為安全犧牲業務運作。

</details>

>> #### Task 8：漏洞、威脅、風險

1. Vulnerability（漏洞／弱點）<br>
    **定義：** 系統中存在的一種弱點，可能被攻擊者利用。<br>
   可以理解為 **「可以被攻擊的點」**
2. Threat（威脅）<br>
    **定義：** 與漏洞相關聯的 **「潛在危害行為或攻擊者」**。<br>
   可以理解為 **「誰會利用這個弱點造成破壞」** 
3. Risk（風險）<br>
    **定義：攻擊者利用漏洞的可能性 × 造成的影響程度**。<br>
    可以理解為 **「這件壞事真的發生的機率與損害」** 

---

範例：玻璃門的展示間

|  名稱   | 解釋 | 
|-|-------|
|Vulnerability（漏洞）| 玻璃門與窗戶材質脆弱，容易被破壞（玻璃本身就是弱點）   |
|Threat（威脅）| 小偷或破壞者可能打破玻璃進行入侵 |
|Risk（風險）| 小偷真的打破玻璃闖入的機率 × 店內損失的財物與營運影響|

---

範例：醫院資料庫漏洞

|  名稱   | 解釋 | 
|-|-------|
|Vulnerability（漏洞）| 醫院使用的資料庫有未修補的安全漏洞 |
|Threat（威脅）| 已有攻擊者發佈了漏洞的攻擊程式（Proof of Concept exploit）|
|Risk（風險）|資料被竊或遭竄改的機率 × 對病患安全與醫院信譽的損害|
