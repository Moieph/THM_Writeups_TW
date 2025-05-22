# DFIR: An Introduction

**🟦 DFIR：簡介**

THM路徑：https://tryhackme.com/room/introductoryroomdfirmodule

---

>> #### Task 1：介紹
DFIR ➜ Digital Forensics and Incident Response <br>**數位鑑識與事件回應**

>> #### Task 2：對 DFIR 的需求
🧠 什麼是 DFIR？
-  專門用來在發生資安事件時，從數位設備（如電腦、儲存裝置、手機）中蒐集證據、調查攻擊、回復系統。

---
📌 DFIR 的作用是什麼？

| 功能項目                 | 說明                                                             |
|--------------------------|------------------------------------------------------------------|
| 發現攻擊者活動的證據     | 區分真實事件與誤報告警                                           |
| 移除攻擊者的存活點       | 徹底清除攻擊者的立足點，防止再次入侵                             |
| 確認入侵範圍與時間       | 方便與主管、法務、管理層做事件通報與處置                         |
| 找出漏洞來源             | 分析攻擊如何進來，找出應修補的防禦缺口                           |
| 分析攻擊者行為模式       | 建立防禦策略，預防未來重複攻擊                                   |
| 資訊共享                 | 向社群分享攻擊資訊（如 IOC、TTPs）以提升整體防禦力               |

---
🧑‍💻 誰在執行 DFIR？

| 領域                         | 專業技能                                                         |
|------------------------------|------------------------------------------------------------------|
| 數位鑑識（Forensics）         | 專長於找出使用者或攻擊者在數位設備中留下的痕跡與證據             |
| 事件回應（Incident Response） | 專長於調查與回應資安事件，善用鑑識資料進行威脅識別與處置         |

✅ 一位 DFIR 專業人員需要兼具 **數位鑑識能力 + 資安分析能力**，並能靈活運用這兩項知識協同調查與防禦。

---

🔁 為什麼 DFIR 這兩者要結合？

| 整合原因             | 說明                                                         |
|----------------------|--------------------------------------------------------------|
| IR 依賴鑑識資料       | 事件回應要靠鑑識找到入侵路徑與證據                           |
| 鑑識範圍由 IR 定義   | IR 決定哪些設備需要鑑識、鑑識要挖多深                         |
| 雙向支援，缺一不可   | 資安應變與數位證據處理緊密結合，形成互補關係                 |

---
🎯 小結
DFIR 是防守性資安的關鍵領域，不只是查案，更關乎：
- 阻止進一步攻擊
- 精確溝通風險
- 修補安全漏洞
- 建立組織應變能力

##### 🔐 答題：
1. What does DFIR stand for?
   
   DFIR 代表什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Digital Forensics and Incident Response`

2. DFIR requires expertise in two fields. One of the fields is Digital Forensics. What is the other field?
   
   DFIR 需要兩個領域的專業知識。其中一個領域是數位取證。另一個領域是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Incident Response`

>> #### Task 3：DFIR 的基本概念

**DFIR 順序**
1. Artifacts（鑑識物件）<br>
2. Evidence Preservation（證據保全）
3. Chain of Custody（證據持有鏈）
4. Order of Volatility（揮發順序）
5. Timeline Creation（事件時間軸建立）

---

🧩 **Artifacts（鑑識物件）**
- **定義**：證明系統上某些活動曾經發生的「數位痕跡」或「線索」
- **舉例**：攻擊者在 Windows 中用登錄機碼維持存活，這些機碼就可以作為 artifacts
- **來源**：檔案系統、記憶體、網路活動等
- **用途**：用來支持資安事件的推論、調查攻擊者行為

📌 常見系統：
- **Windows**：用於端點、AD 控制器、Exchange 伺服器等
- **Linux**：多用於 Web / 資料庫 / 應用伺服器

---

🧪 **Evidence Preservation（證據保全）**
- 鑑識分析的過程會改變原始資料，因此：
    1. 先**寫入保護（Write-protect）原始證據**
    2. 使用複本進行分析，**保護原始資料不被污染**
- 若分析過程中出錯，可再從原始資料重新複製

---

📦 **Chain of Custody（證據持有鏈）**
- 證據在蒐集後的「每一個流轉階段」都必須記錄與控制
- 若有不相關人員接觸證據，會導致「持有鏈污染」 → 可能失去法律效力
- 每次轉交都需記錄 **誰、什麼時間、交付原因**

---

⚠️ **Order of Volatility（揮發順序）**
- 指不同類型的數位證據，其資料「易失性」不同
- 優先**保全最容易消失**的證據，例如：
  - ✅ RAM（記憶體） → 關機就沒了
  - 🕓 硬碟（Persistent）→ 即使斷電資料仍在

🔁 正確順序應優先擷取記憶體，再處理硬碟或網路日誌等資料

---

🗓️ **Timeline Creation（事件時間軸建立）**
- 把所有 artifacts **按時間順序排列**，建立事件發生過程的全貌
- 幫助分析人員「拼湊故事」、重建攻擊流程
- 可整合多個來源（如 Log、Email、系統事件）形成一條清晰脈絡

---

📘 小結：

| 概念項目              | 說明與重點                                                         |
|-----------------------|--------------------------------------------------------------------|
| Artifacts             | 攻擊或使用行為留下的線索，需完整蒐集與分類                        |
| Evidence Preservation | 原始證據須保護，分析只能在複本上進行                              |
| Chain of Custody      | 每一次證據轉移都需記錄，避免非授權人員觸碰                        |
| Order of Volatility   | 擷取順序：先記憶體、後硬碟；避免資料消失                          |
| Timeline Creation     | 將所有活動組成時間線，建立完整攻擊事件流程                         |

---
Question 2：點擊 「View Site」 打開網頁，點擊該 IP 流量事件時間，加入於表格中（升序）

<p align="left">
  <img src="/rooms/images/18_01.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/18_03.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/18_02.png" width="600">
</p>

將以下紅色事件添入於表格，依時間順序排列後，獲得 Flag 🎉🎉

<p align="left">
  <img src="/rooms/images/18_04.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/18_05.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/18_06.png" width="600">
</p>

##### 🔐 答題：
1. From amongst the RAM and the hard disk, which storage is more volatile?
   
   在 RAM 和硬碟中，哪個存儲的波動性更大？
   
&nbsp;&nbsp;&nbsp;&nbsp; `RAM`

2. Complete the timeline creation exercise in the attached static site. What is the flag that you get after completion?
   
   在附加的靜態網站中完成時間線創建練習。完成後你得到的標誌是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{DFIR_REPORT_DONE}`

>> #### Task 4：DFIR 工具

| 工具名稱         | 說明與用途                                                                 |
|------------------|------------------------------------------------------------------------------|
| Eric Zimmerman 工具 | Windows 平台鑑識分析工具組，支援註冊表、檔案系統、時間軸等分析               |
| KAPE             | 自動化收集與解析鑑識資料，可快速建立事件時間軸                               |
| Autopsy          | 開源鑑識平台，支援行動裝置、硬碟、隨身碟等媒體分析，可安裝外掛擴充功能          |
| Volatility       | 記憶體鑑識工具，支援 Windows / Linux 的記憶體擷取與分析                        |
| Redline          | FireEye 開發的 IR 工具，可擷取系統鑑識資訊，協助事件調查                       |
| Velociraptor     | 進階端點鑑識與事件回應平台，具備即時監控、開源且功能強大                         |

>> #### Task 5：事件回應流程

🛡️ DFIR 在資安營運中的核心用途：**事件回應（IR）**

- 在資安營運（Security Operations, SecOps）中，**數位鑑識**（Digital Forensics） 的主要目的是支援 **事件回應**（Incident Response, IR），幫助有效調查、控制與回復系統。

---

🔁 標準事件回應流程：**NIST vs. SANS**

✅ NIST SP 800-61 定義的 IR 流程：
1. Preparation（準備）
2. Detection and Analysis（偵測與分析）
3. Containment, Eradication, and Recovery（圍堵、清除與回復）
4. Post-incident Activity（事後活動）

✅ SANS 事件處理流程（PICERL）：
1. Preparation（準備）
2. Identification（識別）
3. Containment（圍堵）
4. Eradication（清除）
5. Recovery（回復）
6. Lessons Learned（經驗回顧）

📌 雖然步驟名稱略有不同，實質內容相同。SANS 更細分，有助記憶與操作。

---

🧠PICERL 流程說明

| 階段                         | 說明                                                                 |
|------------------------------|----------------------------------------------------------------------|
| Preparation（準備）          | 建立團隊、流程與技術工具，預先防範與演練，準備好應對未來的資安事件         |
| Identification（識別）       | 透過告警與日誌發現異常，進行分析、篩除誤報，並通知相關單位                   |
| Containment（圍堵）          | 限制事件影響範圍，可能包含短期與長期的隔離或修補行動                         |
| Eradication（清除）          | 根除威脅，清理惡意程式與後門，必須確保進入點已封鎖，否則攻擊者會再次滲透     |
| Recovery（回復）             | 恢復受影響的系統與服務，並確認系統安全與穩定，避免舊威脅再次觸發             |
| Lessons Learned（經驗回顧）  | 撰寫事件報告，討論處理過程、成功與失誤，優化下次事件應變能力                 |


---

🧩 DFIR 如何輔助 IR？
- <b>鑑識資料（Artifacts）</b>協助識別與圍堵來源
- **記憶體分析與日誌調查** 支援威脅根除與橫向移動追蹤
- **時間軸重建** 幫助理清整體攻擊過程
- **證據保存與報告撰寫** 強化經驗回顧與組織記錄

##### 🔐 答題：
1. At what stage of the IR process are disrupted services brought back online as they were before the incident?
   
   在 IR 流程的哪個階段，中斷的服務會像事件發生前一樣恢復在線？
   
&nbsp;&nbsp;&nbsp;&nbsp; `recovery`

2. At what stage of the IR process is the threat evicted from the network after performing the forensic analysis?
   
   執行取證分析後，在 IR 流程的哪個階段將威脅從網路中驅逐出去？
   
&nbsp;&nbsp;&nbsp;&nbsp; `eradication`

3. What is the NIST-equivalent of the step called "Lessons learned" in the SANS process?
   
   在 SANS 流程中，「經驗教訓」的步驟的 NIST 等價物是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Post-incident Activity`
