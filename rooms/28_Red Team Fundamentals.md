# Red Team Fundamentals

**🟥 紅隊基礎知識**

THM路徑：https://tryhackme.com/room/redteamfundamentals

---

>> #### Task 1：介紹

🧠 **Red Team Engagement （紅隊演練**）：

| 類型         | 說明                                                   |
| ---------- |------------------------------------------------------|
| 定義         | 模擬「真實攻擊者」行為的全方位演練，測試企業對 **複合式攻擊的偵測與應變能力**。           |
| 目標         | 不只找漏洞，而是 **測試企業整體的防禦流程與反應能力**（例如 SOC、IR 團隊）。         |
| 涉及角色 | Red Team（攻擊方）、Blue Team（防守方）、Purple Team（協調 / 分析雙方行為） |
| 與傳統滲透差異   | 滲透測試找技術漏洞；Red Team 從 **策略層面驗證攻擊流程能否實現，並測試組織反應能力**    |
| 成果回饋     | 通常會包含 **目標是否達成（如滲透 CEO 信箱）+ Blue Team 是否偵測與回應成功**    |


>> #### Task 2：漏洞評估和滲透測試限制

🛡 三種資安測試方式比較：

| 項目       | Vulnerability Assessment（漏洞評估） | Penetration Test（滲透測試）                | Red Team Engagement（紅隊演練）                    |
| -------- |--------------------------------|---------------------------------------|----------------------------------------------|
| 目標       | 找出 **所有主機上的已知漏洞**，提供修補依據       | 測試 **漏洞是否可利用**、模擬駭客從外部/內部**橫向移動**的可能性 | 模擬 **高階駭客（APT）真實攻擊手法**，測試**企業應變、偵測、通報與反制能力** |
| 技術層級     | 初階為主，大多使用**自動化工具**掃描           | 中階以上，需要懂得**漏洞利用與後滲透技術**               | 高階，需要懂得**社交工程、C2、長期潛伏、繞過偵測**等實戰技巧            |
| 是否嘗試入侵 | ❌ 不入侵，只掃漏洞                     | ✅ 嘗試利用漏洞進行入侵                          | ✅ 整體模擬「駭客潛入→橫向滲透→達成目標→維持存活→避偵測」全流程           |
| 防禦機制處理方式 | 通常會**放行或關閉安全防護**避免干擾掃描         | 有時也會放行安全設備提高效率                        | **完整保留真實防禦機制**（IDS、WAF 等不會刻意繞開）              |
| 隱密程度     | 不重要，掃越多越好                      | 不注重隱匿性，會產生大量日誌與告警                     | 高度隱密，模擬駭客潛伏滲透，不易被偵測                          |
| 是否模擬真實駭客攻擊 | ❌ 無模擬                          | ⚠️ 部分模擬：技術面有模擬但**不涵蓋社交工程**或**實體入侵**   | ✅ 全面模擬，連員工開信件點附件都算入考量，包含**APT攻擊流程**          |
| 執行時間    | 幾天～一週                          | 約一至兩週                                 | 幾週到幾個月（視目標範圍而定）                              |
| 是否告知藍隊 | 通常已知                           | 通常已知                                  | 藍隊**通常不知情**，觀察其真實反應                          |

Vulnerability Assessment（漏洞評估）：

<p align="left">
  <img src="/rooms/images/28_01.png" width="600">
</p>

Penetration Test（滲透測試）：

<p align="left">
  <img src="/rooms/images/28_02.png" width="600">
</p>

---

📌 重點觀念：為何 Pentest 不夠

✅ 滲透測試的限制：
- **太吵（Loud）**：Pentest 通常不會避免產生警報，因為目的在找出所有漏洞。
- **忽略非技術向攻擊**：像是釣魚信件、社交工程、USB drop、實體入侵這類**真實風險場景未涵蓋**。
- **安全機制會放寬**：為了效率，可能讓 Pentester 不用繞過防火牆或 IDS。

🚨 而 **APT（高階持續性攻擊）** 會怎麼做？
- Advanced Persistent Threats 
- 長期潛伏：可能潛藏**數月或數年不被發現**。
- 社交工程 + 零日漏洞：用**釣魚郵件、社交工程引誘** + 使用尚未曝光漏洞。
- 不留痕跡：用**反取證工具、記憶體常駐手法、無檔案攻擊**等繞開偵測。

---

🎯 Red Team 的出現正是為了解決這些問題：
- ✅ 模擬真實攻擊場景：從社工、物理滲透、技術攻擊到長期存活。
- ✅ 測試企業的「應變能力」與「偵測與通報流程」。
- ✅ 幫助組織辨識出最真實的風險與缺口，而不是只有技術漏洞。

---

##### 🔐 答題：
1. Would vulnerability assessments prepare us to detect a real attacker on our networks? (Yay/Nay)
   
   漏洞評估是否能讓我們準備好在我們的網路上檢測真正的攻擊者？（是/否）
   
&nbsp;&nbsp;&nbsp;&nbsp; `Nay`

2. During a penetration test, are you concerned about being detected by the client? (Yay/Nay)
   
   在滲透測試期間，您是否擔心被客戶檢測到？（是/否）
   
&nbsp;&nbsp;&nbsp;&nbsp; `Nay`

3. Highly organised groups of skilled attackers are nowadays referred to as ...
   
   高度組織化的熟練攻擊者群體現在被稱為......
   
&nbsp;&nbsp;&nbsp;&nbsp; `Advanced Persistent Threats `

>> #### Task 3：紅隊演練

🛡 Red Team Engagement（紅隊演練）

- 與其像傳統滲透測試專注「找漏洞、測可利用性」，紅隊演練重點在於 **模擬真實駭客攻擊流程**，測試防禦方（藍隊）的偵測與應變能力。


- 紅隊不是來「贏藍隊」，而是協助 **建立更強的偵測與應變能力**

<p align="left">
  <img src="/rooms/images/28_03.png" width="600">
</p>

---

🎯 Red Team vs PenTest 差異比較表：

| 項目   | 滲透測試（PenTest）   | 紅隊演練（Red Team Engagement） |
| ---- | --------------- | ------------------------- |
| 目標   | 找出並驗證漏洞         | 模擬駭客攻擊流程，測試防禦反應           |
| 模擬對象 | 系統、服務與網路        | 真實威脅行為者的 TTP（戰術、技巧、程序）    |
| 偵測   | 通常不在乎被偵測        | 盡量**避免被偵測**，保持潛伏          |
| 社交工程 | 通常不納入           | ✅ 包含（釣魚、冒充、誘導）            |
| 實體入侵 | 通常不納入           | ✅ 包含（撬鎖、RFID 複製）          |
| 報告重點 | 技術弱點與修補建議       | 偵測流程、事件應變、橫向移動與 C2 分析     |
| 目的   | 提升防禦能力的**事前預防** | 提升防禦能力的**即時應變與偵測效率**      |

---

🧠 Red Team 三大攻擊面向：

1. 技術面：
   - 弱點利用、內網橫向滲透、權限提升、C2 架設、避偵測技巧（AV/EPP/EDR/IPS繞過）


2. 社交工程：
   - 假冒郵件、社群釣魚、語音詐騙、假網站誘導登入、USB drop


3. 實體入侵：
   - 撬鎖進入、RFID 複製、門禁漏洞、植入硬體後門

---

🧩 Red Team 三種演練方式：

| 演練類型                      | 說明                                    |
| ------------------------- | ------------------------------------- |
| ✅ **Full Engagement**     | 完整模擬整個攻擊鏈（從初始滲透到目標達成）                 |
| ⚠️ **Assumed Breach**     | 假設駭客已取得某些控制點（如 AD 帳號、內網主機），從這邊開始模擬攻擊  |
| 🧠 **Table-top Exercise** | 純討論模擬，雙方推演不同情境下的反應（如若郵件系統被入侵，藍隊如何應變？） |

---

🏆 常見紅隊目標（Crown Jewels / Flags）：

- 控制內網關鍵伺服器（如 AD、Intranet）
- 偷取敏感資料（如財報、人事、合約）
- 取得機敏帳號或資料庫金鑰
- 建立長期潛伏通道（C2、後門）

---

##### 🔐 答題：
1. The goals of a red team engagement will often be referred to as flags or...
   
   紅隊參與的目標通常被稱為標誌或......
   
&nbsp;&nbsp;&nbsp;&nbsp; `Crown Jewels`

2. During a red team engagement, common methods used by attackers are emulated against the target. Such methods are usually called TTPs. What does TTP stand for?
   
   在紅隊交戰期間，攻擊者使用的常見方法被模擬來對付目標。這種方法通常稱為 TTP。TTP 代表什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Tactics, Techniques and Procedures`

3. The main objective of a red team engagement is to detect as many vulnerabilities in as many hosts as possible (Yay/Nay)
   
   紅隊參與的主要目標是檢測盡可能多的主機中的漏洞 （是/否）
   
&nbsp;&nbsp;&nbsp;&nbsp; `Nay`

>> #### Task 4：參與的團隊和功能

🧱 Red Team Engagement：三大核心小組與紅隊內部分工：

| Team（小組）          | 定義與職責                                    |
| ----------------- | ---------------------------------------- |
| 🔴 **Red Cell**   | 負責進攻模擬，模仿真實攻擊者的戰略與戰術手法，執行整體攻擊行動。         |
| 🔵 **Blue Cell**  | 負責防禦，通常由資安團隊、內部 IT、管理人員組成，代表被攻擊方。        |
| ⚪️ **White Cell** | 裁判與協調者，監督攻防兩方是否遵守演練規範（ROE），維持演練公平、安全與秩序。 |

🔍 備註： White Cell 不參與攻防，而是負責：
- 控制演練環境（網路架構、權限邊界）
- 管理活動協調與目標達成
- 確保雙方行為公正、無偏頗
- 紀錄並評估攻防對應行為（例如紅隊發動釣魚信，藍隊是否有偵測或阻擋）

<p align="left">
  <img src="/rooms/images/28_04.png" width="600">
</p>

---

🔴 Red Cell（紅隊）內部職責分工

| 角色                | 職責                                                                  |
| ----------------- |---------------------------------------------------------------------|
| **Red Team Lead** | 高層規劃與組織整場演練，分配任務給副手與操作手，負責 Engagement 的整體成功。                        |
| **Assistant Lead** | 協助主導者控場、指導操作人員，必要時協助撰寫演練計畫與報告文件。                                    |
| **Operator（操作者）** | 根據上級交辦內容執行實際攻擊任務，包含釣魚、內網滲透、橫向移動、C2 建立、避偵測等。需能靈活理解與執行 Engagement 計畫。 |

---

📌 備註補充

不同公司與團隊規模，紅隊架構可能會進一步細分，如：
   - 專職社交工程手
   - 實體滲透成員
   -  內網 / C2 專家
   -  報告與紀錄負責人

紅隊中的分工，例如：
   - Recon Team：針對目標進行網路足跡蒐集（OSINT）
   - Initial Access Team：處理初始進入點（釣魚、外網服務利用）
   -  Persistence & Lateral Movement：植入、移動與持續控制

---

##### 🔐 答題：
1. What cell is responsible for the offensive operations of an engagement?
   
   哪個單元負責交戰的進攻性作戰？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Red Cell`

2. What cell is the trusted agent considered part of?
   
   受信任的代理被視為哪個單元的一部分？
   
&nbsp;&nbsp;&nbsp;&nbsp; `White Cell`

>> #### Task 5：參與結構

📌 什麼是「Adversary Emulation」？

紅隊的核心功能之一是**模擬真實攻擊者的行為與技術（TTPs）**，包括使用他們可能會採用的工具、策略與流程，以達到「像真的在攻擊一樣」的效果。這可以幫助：

- 測試防禦團隊（藍隊）的偵測與應變能力
- 依照實際威脅場景評估資安控制是否有效
- 建立一套與攻擊者行為接軌的紅隊作業流程

---

📊 常見 Cyber Kill Chain（殺戮鏈）結構

| Kill Chain 名稱                | 特點                                |
| ---------------------------- |-----------------------------------|
| Lockheed Martin Kill Chain   | 最經典、標準化高，強調 **外部入侵**路徑 ，紅藍兩隊都常使用。 |
| Unified Kill Chain           | 整合多種攻擊路徑，涵蓋更廣泛的攻擊階段（內部與外部）。       |
| Varonis Cyber Kill Chain    | 著重資料存取與內部橫向移動。                    |
| Active Directory Attack Cycle | 專注於針對 AD（目錄服務）系統的攻擊流程。            |
| MITRE ATT\&CK Framework    | 攻擊技術最細節的矩陣型資料庫，常被用於 **TTP 對應分析**。 |

  
>> #### Task 6：紅隊參與概述

>> #### Task 7：結論