# Intro to IR and IM

**🟦 IR 和 IM 簡介**

THM路徑：https://tryhackme.com/room/introtoirandim

---

>> #### Task 1：介紹

IR ➜ Incident Response **事件回應**
IM ➜ Incident Management **事件管理**

>> #### Task 2：事件回應和管理

🧭 事件從哪裡開始？——SOC 運作流程

| 項目                  | 說明                                                    |
|-----------------------|-------------------------------------------------------|
| SOC（資安營運中心）   | 監控全企業安全事件，篩選異常活動，判斷是否升級為事件                            |
| Alert（警示）         | 由 SIEM / EDR / AV / Network Tap Alert  等工具觸發，可為真陽性或誤報 |
| Triage（三分類）      | 分析警示是否嚴重，若達嚴重標準，則升級為 Incident（事件）                     |
| Incident（事件）      | 警示具有後續影響、尚需更多資訊才能解決，即視為事件                             |

---

🧱 事件回應 vs. 事件管理

| 分類                | 問題核心           | 負責內容                                                             |
|---------------------|--------------------|----------------------------------------------------------------------|
| Incident Response   | What happened?     | 技術層面處理：調查攻擊、收集證據、執行數位鑑識、了解事件範圍         |
| Incident Management | How to respond?    | 管理層面處理：調度人員、引導流程、溝通協調、紀錄報告、復原系統       |

🔧 常見工具來源：
- EDR / AV 警示：主機異常行為（如鍵盤監聽）
- 網路監測警示：內網掃描、橫向移動
- SIEM 警示：自訂規則（如 Impossible Travel）

💡 若原始警示不夠詳細，就需透過 數位鑑識（Forensics） 來深入調查，如：
- 擷取硬碟內容分析
- 擷取記憶體（RAM）
- 追蹤橫向移動的行為記錄

---
🔥 事件處理的四個等級（大公司常見架構）

| 等級 | 名稱            | 描述                                                                                   |
|------|------------------|------------------------------------------------------------------------------------------|
| L1   | SOC Incident      | 最小事件，由單一分析師處理，技術性問題，如封鎖寄件者，更新濾信規則                       |
| L2   | CERT Incident     | 多名分析師介入，調查範圍擴大，如多人收到釣魚信、可能有中毒，尚未確認全體影響             |
| L3   | CSIRT Incident    | 全 SOC 投入，調查擴大，已確認攻擊擴散，開始進行全面圍堵、清除、復原行動                   |
| L4   | CMT Incident      | 最高等級 危機處理，由主管、法務、公關、外部單位（如政府/警方）共同應變，甚至可關閉整個系統 |

📌 層級越高 ➤ **投入越多資源、干擾越大，但也越必要**

---

🎯 IR / IM 的價值與必要性
- 架設 SOC 與 IR/IM 團隊雖然成本高，但：
    - 沒有應變計畫時，一次事件可能就會**毀掉整間公司**
    - 根據統計：**60% 中小企業**在資安事件**發生 6 個月內倒閉**
- IR + IM 並非「大公司專利」，而是每一間企業生存保險

##### 🔐 答題：
1. At what level (number only) of an incident would the SOC be placed at high alert and to deal with an incident?
   
   SOC 應在事件的哪個級別（僅編號）處於高度戒備狀態並處理事件？
   
&nbsp;&nbsp;&nbsp;&nbsp; `3`

2. At what level (number only) of an incident would it be classified as a cyber crisis?
   
   在事件的哪個級別（僅編號）會被歸類為網路危機？
   
&nbsp;&nbsp;&nbsp;&nbsp; `4`

3. Which component (IR or IM) is responsible for trying to answer the question: How do we respond to what happened?
   
   哪個元件（IR 或 IM）負責嘗試回答這個問題：我們如何應對發生的事情？
   
&nbsp;&nbsp;&nbsp;&nbsp; `IM`

4. Which component (IR or IM) is responsible for trying to answer the question: What happened?
   
   哪個元件（IR 或 IM）負責嘗試回答以下問題：發生了什麼情況？
   
&nbsp;&nbsp;&nbsp;&nbsp; `IR`

>> #### Task 3：事件期間的不同角色

IR/IM 重要角色職責表：

| 角色                    | 職責說明                                                                 |
|-------------------------|--------------------------------------------------------------------------|
| SOC Analyst             | 第一線接收與處理警示，根據層級分工處理事件，為最早接觸事件的成員之一     |
| SOC Lead / Manager      | 管理 SOC 運作、分配任務，並決定是否將警示升級為事件                       |
| Forensic Analyst        | 負責分析記憶體、硬碟等證據，協助釐清事件過程                               |
| Malware Analyst         | 研究惡意程式運作邏輯，協助挖掘 IoC（攻擊指標），通常具備反組譯能力         |
| Threat Hunter           | 主動搜尋未知威脅，建立新規則提升偵測能力                                 |
| First Responder         | 非 SOC 成員但最早發現異常的業務單位，需保護現場並避免證據損毀             |
| Security Engineer       | 區域/系統資安負責人，負責提供日誌與技術支援                               |
| Information Security Officer (ISO) | 負責管理所屬部門資安，為溝通橋梁，協助整合 IR 團隊與業務團隊        |
| Incident Manager        | 管理事件處理流程、撰寫紀錄、引導行動決策，具備組織與溝通能力               |
| Product Owner           | 專案負責人，熟悉產品架構，能於事件中提供系統實作層面的專業建議             |
| Subject Matter Expert (SME) | 專精特定技術（如 AD、雲端、資料庫）者，協助提供內部結構與攻擊影響判斷   |
| Crisis Manager          | 危機應變領導者，通常為高階主管如 CIO、COO，負責指揮最高層級的回應行動      |
| Executive               | 重大事件時進入應變小組（CMT），包含 CEO、COO、CTO、CISO 等人                |



>> #### Task 4：事件管理流程

>> #### Task 5：事件期間的常見陷阱

>> #### Task 6：結論