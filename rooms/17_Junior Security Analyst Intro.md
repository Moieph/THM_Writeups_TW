# Junior Security Analyst Intro

**🟦 初級安全分析師簡介**

THM路徑：https://tryhackme.com/room/jrsecanalystintrouxo

---

>> #### Task 1：初級安全分析師的職涯

🛡️ 主要職責（Responsibilities）：

| 職責項目                     | 說明                                                   |
|------------------------------|------------------------------------------------------|
| 監控與調查告警               | 持續分析事件記錄與警報（多為 24x7 安全監控環境）                          |
| 設定與管理資安工具           | 操作 SIEM、防毒、防火牆等工具                                    |
| 撰寫與套用 IDS 簽名規則      | 建立基本**入侵偵測系統**（Intrusion Detection System） ，用以識別特定攻擊行為 |
| 參與 SOC 團隊會議            | 與其他分析師討論警報處理、流程改善                                    |
| 建立與升級事件票證           | 紀錄事件，必要時回報給 Tier 2 分析師或組長                            |

---

🎓 常見入門條件（Required Qualifications）：

| 條件項目         | 說明                                                               |
|--------------|------------------------------------------------------------------|
| 資安經驗 0 - 2 年 | 可接受無經驗，適合新手入門                                                    |
| 基礎網路知識       | 需理解 OSI （開放系統互連）、TCP/IP （傳輸控制協定/Internet 協定），可參考 Networking 入門教學 |
| 作業系統基本概念     | 包含 Windows、Linux 使用與結構理解                                         |
| 網頁應用基礎       | 了解 Web 架構與攻擊面（如 XSS、SQLi）                                        |
| 撰寫/程式能力加分    | 會 Python、Bash、PowerShell 等腳本語言者佳                                 |

---

推薦證照（Desired Certification）：<br>
**CompTIA Security+（最常見的入門資安證照）**

---

📈 晉升方向與職涯發展：
- Tier 1：入門級，負責事件初步分析（你目前的角色）
- Tier 2：進階分析師，處理複雜事件、深入調查
- Tier 3：資深分析師 / 威脅獵人，進行行為分析、攻擊趨勢研究

<p align="left">
  <img src="/rooms/images/17_01.png" width="600">
</p>

##### 🔐 答題：
1. What will be your role as a Junior Security Analyst?
   
   作為初級安全分析師，您的角色是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Triage Specialist`

>> #### Task 2：安全運營中心 （SOC）

&nbsp;&nbsp;&nbsp;&nbsp;_SOC（資安營運中心） 是一個 24/7 運作的資安防禦單位_ <br>

核心任務是： **「持續監控、調查、預防並回應 各種網路威脅」**

McAfee 的定義：
「安全團隊負責保護企業資產，例如智慧財產權、人員資料、商業系統與品牌聲譽。他們是組織整體資安架構的實作部門，負責協調各項資安防禦行動。」

👉 SOC 的人數會依公司規模而異。

<p align="left">
  <img src="/rooms/images/17_02.png" width="600">
</p>

---

📋 SOC 三大職責模組整理

| 職責模組           | 說明                                                                 |
|--------------------|----------------------------------------------------------------------|
| 預防與準備         | 情資蒐集、威脅趨勢追蹤、防火牆簽名更新、漏洞修補、封鎖名單管理等        |
| 監控與調查         | 使用 SIEM / EDR 工具監控告警、依嚴重程度分類（Critical → Low）處理       |
| 應變處理           | 對遭入侵主機進行隔離、終止惡意程序、刪除檔案等實際回應動作                |

---

✅ 預防與準備：
- 持續追蹤最新攻擊手法與攻擊者 TTP（策略、技術與程序）
- 維護安全性（如更新防火牆簽名、修補漏洞）
- 管理阻擋/允許清單（IP、域名、應用程式）
- 可參考：APT40 威脅警報（CISA）：https://us-cert.cisa.gov/ncas/alerts/aa21-200a

🔍 監控與調查：
- 工具：**SIEM、EDR**
- 事件分類如消防等級（一級火警～三級火警），以 **Critical → Low** 優先順序處理
- 初階分析師進行 triage（篩選/初步分析），需思考：「**怎麼發生？何時？為什麼？」**
- 使用日誌分析與開源工具輔助調查

🚨應變與處置
- 調查完成後，對受害系統進行：
    - **隔離主機**
    - **終止惡意行為**
    - **清除惡意檔案**
- 協同團隊實施 Incident Response 流程

---
🎯 小總結：SOC 就像是資安界的消防隊

| 比喻角色           | 功能                                             |
|--------------------|--------------------------------------------------|
| 消防隊             | 隨時待命應對火災（資安事件）                     |
| 消防警報           | SIEM 系統告警                                     |
| 火災等級           | 告警等級（Critical、High、Medium、Low）           |
| 火場指揮員         | Tier 2 / Tier 3 資深分析師                         |
| 滅火與清理現場     | 終止攻擊、清除惡意程式、修復受害系統               |

>> #### Task 3：初級安全分析師的一天

🛠️ 日常任務：

| 任務項目                 | 說明                                                               |
|--------------------------|--------------------------------------------------------------------|
| 檢查告警票證             | 每天上班的第一件事：打開事件系統，確認有無新告警產生              |
| 監控網路流量             | 包含 IPS / IDS 系統告警（入侵偵測與預防）                         |
| 調查可疑郵件             | 追蹤釣魚郵件來源、URL、附件等                                     |
| 擷取與分析鑑識資料       | 如記憶體、磁碟映像、Log 等，用來判斷是否為攻擊                     |
| 使用開源情報（OSINT）    | 輔助分析告警真偽、判斷威脅來源                                   |
| 參與事件回應             | 涉及「偵測 ➝ 阻止 ➝ 清除 ➝ 復原」等完整 IR 流程                    |


---

🚨<b>事件處理（Incident Response）</b>可能會花上：
- **幾小時 → 幾天 → 幾週**
- 決定因素包含：
    - 攻擊者是否成功竊取資料？
    - 外洩資料量有多少？
    - 攻擊者是否已橫向移動到其他主機？

---

👨‍💻 成為資安防禦者（Network Defender）前，你需要掌握：

| 基本技能                     | 內容說明                                                         |
|------------------------------|------------------------------------------------------------------|
| 威脅識別與告警分析           | 判斷告警真偽，並能優先處理高風險事件                             |
| 工具操作（SIEM / IDS / IPS） | 熟悉資安工具、能閱讀日誌與建立告警條件                           |
| 鑑識與證據保存流程           | 理解如何合法、正確地擷取證據供後續分析或法務使用                 |
| 回應流程與報告撰寫           | 能配合團隊執行回應任務，並撰寫清晰的處理報告與記錄               |

Question 1：點擊 View Site 打開網頁

<p align="left">
  <img src="/rooms/images/17_03.png" width="600">
</p>

Question 2：找到可疑 IP，並確認是否為惡意

<p align="left">
  <img src="/rooms/images/17_04.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/17_05.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/17_06.png" width="600">
</p>

Question 3：向上級回報，並封鎖 IP，獲得 Flag 🎉🎉

<p align="left">
  <img src="/rooms/images/17_07.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/17_08.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/17_09.png" width="600">
</p>

##### 🔐 答題：
2. What was the malicious IP address in the alerts?
   
   警報中的惡意 IP 位址是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `221.181.185.159`

3. To whom did you escalate the event associated with the malicious IP address?

   您向誰上報了與惡意 IP 位址相關的事件？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Will Griffin`

4. After blocking the malicious IP address on the firewall, what message did the malicious actor leave for you?

   在防火牆上遮罩惡意 IP 位址後，惡意行為者給你留下了什麼資訊？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{UNTIL-WE-MEET-AGAIN}`