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

Question 1：輸入各角色的職責描述，獲得 Flag 🎉🎉

<p align="left">
  <img src="/rooms/images/19_01.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/19_02.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/19_03.png" width="600">
</p>

1. What is the value of the flag you receive after matching the roles and responsibilities?
   
   在匹配角色和職責后，您收到的旗幟為何？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{Roles.and.Responsibilities.of.IR.and.IM}`

>> #### Task 4：事件管理流程

🧭 **NIST 事件管理流程（Incident Management Framework）**

根據 NIST SP 800-61，事件管理分為 **四大階段**：

| 階段名稱                                         | 核心任務說明                                                              |
|--------------------------------------------------|---------------------------------------------------------------------------|
| 1. Preparation（準備）                           | 建立處理事件所需人員、聯繫網絡、SOP、演練與威脅狩獵準則                     |
| 2. Detection & Analysis（偵測與分析）            | 發現事件、評估嚴重性、執行鑑識調查與攻擊分析，協助定義事件範圍             |
| 3. Containment, Eradication, Recovery（圍堵、清除、回復） | 阻止擴散 ➝ 移除攻擊者 ➝ 恢復環境回到正常運作                               |
| 4. Post-Incident Activity（事後回顧）            | 撰寫事件總結報告、整理經驗教訓，優化下次事件的應變效率                     |

<p align="left">
  <img src="/rooms/images/19_04.png" width="600">
</p>

---

**Preparation（準備）**:

&nbsp;&nbsp;&nbsp;&nbsp;_關鍵觀念：事前準備越完善，事件發生時越不慌張、越少錯誤。_ <br>

準備工作包含：

- 📞 建立聯絡樹（Call Tree）與重要關係人列表
- 📚 撰寫並持續更新事件應變 Playbooks
- 🧠 執行桌上兵推 / 網攻演練（War Game）
- 🔍 持續進行威脅狩獵（Threat Hunting）建立偵測規則

---

**Detection & Analysis（偵測與分析）**:

&nbsp;&nbsp;&nbsp;&nbsp;_關鍵問題：到底發生什麼事了？_ <br>

此階段是 **事件回應的核心**，重點在於釐清事件真相、定義範圍：

- 檢查 AV / EDR / SIEM 警示儀表板
- 分析主機與網路鑑識資料（Artifacts）
- 拆解分析惡意程式（Malware）與建立對應偵測簽名
- 📍 含 **Triage 判斷警示是否升級為事件**（若企業有內部分拆）

---

**Containment, Eradication, Recovery**：<br>
（圍堵 ➝ 清除 ➝ 回復）

這是 **事件管理的核心階段**，目標是恢復 BAU（Business as Usual）：

| 子階段       | 說明                                                         |
|--------------|--------------------------------------------------------------|
| Containment  | 快速阻止事件擴大（例如斷網、停用帳號）                       |
| Eradication  | 根除攻擊者存活點（後門、帳號、惡意程式等）                   |
| Recovery     | 恢復系統運作，並確保無後門、系統正常                         |

---

**Post-Incident Activity（事後活動）**：

&nbsp;&nbsp;&nbsp;&nbsp;_關鍵問題：這次事件教會了我們什麼？_ <br>

- 撰寫完整報告（事件發生、處置、影響、回應時程）
- 分析哪些 SOP 有效、哪些地方延誤或出錯
- 更新 Playbook / 偵測規則 / 回應流程
- 內部教學分享與改進流程

---

🌀 為什麼「偵測分析」和「圍堵回復」是循環的？

在事件調查過程中：
- 初期無法完全了解攻擊範圍，但不能等待
- 所以要邊調查邊行動 ➝ 看行動效果，再判斷下一步
- 最終以 **能回復到 BAU（正常業務運作）** 為結束依據

Question 1：輸入IM 流程步驟，獲得 Flag 🎉🎉

<p align="left">
  <img src="/rooms/images/19_05.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/19_06.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/19_07.png" width="600">
</p>

##### 🔐 答題：
1. What is the value of the flag you receive after correctly matching the steps of the incident management process?
   
   在正確匹配事件管理流程的步驟后，您收到的旗幟為何？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{Preparation.is.Key.for.Incident.Management}`

>> #### Task 5：事件期間的常見陷阱

| 失誤類型                        | 說明                                                                                   |
|----------------------------------|----------------------------------------------------------------------------------------|
| Insufficient Hardening           | 系統未經強化即上線，為求效率而略過安全配置，增加被攻擊的可能性                         |
| Insufficient Logging             | 未完整收集與保存日誌，導致藍隊無法偵測或調查事件，等於「盲飛」                         |
| Insufficient / Over-Alerting     | 警示過少導致漏報，警示過多導致誤報疲乏；皆可能讓真正的事件被忽略                         |
| Insufficient Determination of Scope | 事件範圍誤判，低估導致未清除乾淨，高估造成業務中斷與資源浪費                             |
| Insufficient Accountability      | 任務無明確負責人，造成「大家都以為有人做了」，實際上沒人執行                             |
| Insufficient Backups             | 備份不足或未隔離，導致勒索攻擊無法復原；現代 DR 環境可能也會被同步感染                    |

Question 1：遊玩簡易判斷遊戲，獲得 Flag 🎉🎉
<p align="left">
  <img src="/rooms/images/19_08.png" width="600">
</p>

1. What is the value of the flag you receive when you overcome the common pitfalls of a cyber incident?
   
   當您克服網路事件的常見陷阱時，您收到的旗幟為何？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{Avoiding.the.Common.IM.Mistakes}`

>> #### Task 6：結論

**事件回應與事件管理 總結整理（Summary）**

1. 資安事件是「常態」
   - 資安事件無法完全避免，重點是 **如何做好準備、有效應對**


2. 並非所有警示都是事件
   - **警示（Alert） ≠ 事件（Incident）** 
   - 透過 **Triage（三分類）** 決定是否升級為事件，並依嚴重性分級（L1~L4）
   

3.  IR vs IM：兩者互補，缺一不可
    
   | 類型               | 關注核心           | 功能說明                                           |
   |--------------------|--------------------|----------------------------------------------------|
   | Incident Response   | What happened?     | 技術面調查、數位鑑識、了解攻擊範圍                  |
   | Incident Management | How to respond?    | 流程管控、人員調度、行動記錄、回復業務營運          |

4. 多元角色參與事件處理
   - 即使你不是藍隊，也可能是：
        - **第一發現人（First Responder）**
        - **領域專家（SME）**
    - 每個人都有可能被納入事件回應流程中
   

5. 多數企業採用 NIST 四階段事件管理架構：

   | 階段                                               | 功能                                                   |
   |----------------------------------------------------|--------------------------------------------------------|
   | Preparation（準備）                                | 建立流程、演練應變、制定通報與回應策略                  |
   | Detection & Analysis（偵測與分析）                 | 偵測事件、判斷範圍、進行數位鑑識調查                    |
   | Containment, Eradication, Recovery（圍堵 ➝ 清除 ➝ 回復） | 實際處理事件，復原系統、恢復正常營運                    |
   | Post-Incident Activity（事後回顧）                 | 撰寫報告、教訓檢討、優化未來應變策略                    |


6. 常見失誤（Pitfalls）需要事前預防

   - 如：紀錄不全、警示過多、角色責任不明、備份不足等
   - **事前準備與清晰分工** 可降低災難擴散與誤判風險