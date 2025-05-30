# Threat Intelligence Tools

**🟦 威脅情報工具**

THM路徑：https://tryhackme.com/room/threatinteltools

---

>> #### Task 1：房間概況

>> #### Task 2：威脅情報

🧠 **Threat Intelligence（威脅情報）**

📌 定義：透過分析資料與資訊，運用工具與技術，萃取出有意義的模式，幫助我們：
- **預測、辨識、應對** 現有或新興的威脅
- 保護目標包含：**組織、產業、關鍵基礎設施、政府單位**

---

❓ 風險緩解的關鍵問題
- 誰在攻擊你？
- 動機是什麼？
- 他們的能力有多強？
- 有哪些 **可識別的指標（IOC）** 需要注意？

---

🧭 威脅情報的四種分類（四個層級）

| 分類                         | 說明                              | 主要使用對象      |
| -------------------------- | ------------------------------- | ----------- |
| **Strategic Intel（策略層）**   | 高層次趨勢分析，評估整體威脅風景與商業決策風險。        | 高階主管、決策者    |
| **Technical Intel（技術層）**   | 聚焦具體攻擊工具與產出物（如 hash、IP、domain）。 | 資安工程師、IR 團隊 |
| **Tactical Intel（戰術層）**    | 分析攻擊者的 **TTPs（戰術、技術、程序）**。      | 藍隊、防禦團隊     |
| **Operational Intel（作戰層）** | 深入對手的具體目標與攻擊計畫，關注受害資產與操作細節。     | 威脅獵捕、紅隊、SOC |


>> #### Task 3：UrlScan.io

🔍 **Urlscan.io** 使用筆記

免費的網站掃描服務，會模擬瀏覽器操作並記錄網站行為與互動，常用於：

- 安全分析與惡意網站辨識
- 技術偵察與網站快照存證

<p align="left">
  <img src="/rooms/images/25_01.gif" width="600">
</p>

---

🚦 掃描結果包含的關鍵資訊：

| 區塊             | 說明                                      |
| -------------- | --------------------------------------- |
| **Summary**    | 顯示 URL 的總覽資訊：IP、註冊細節、歷史紀錄與網站截圖          |
| **HTTP**       | 展示與該網站建立的 HTTP 連線，以及傳輸的檔案與 MIME 類型      |
| **Redirects**  | 顯示 HTTP 或 JavaScript 重定向資訊              |
| **Links**      | 所有首頁上的外部連結                              |
| **Behaviour**  | 變數、Cookies、JS 活動，有助於辨識網站使用的框架           |
| **Indicators** | 所涉及的 IP、網域名稱與檔案 Hash 值（**不代表惡意，但可供分析**） |

<p align="left">
  <img src="/rooms/images/25_02.gif" width="600">
</p>

---

🔄 即時與歷史掃描頁面：
- **Live Scans**：即時觀察目前全球正在執行的掃描
- **Latest Results**：最新的公開掃描結果列表

---

📌 注意事項：
- 不同日期查詢可能不同結果（網站內容、連線資源會變動）。
- 網站可能包含第三方服務，掃描可能列出 **大量外部網域與 IP**。

---

Question 1 - 4：根據題目截圖作答

<p align="left">
  <img src="/rooms/images/25_03.png" width="600">
</p>

##### 🔐 答題：
1. What was TryHackMe's Cisco Umbrella Rank based on the screenshot?
   
   根據屏幕截圖，TryHackMe 的 Cisco Umbrella Rank 是多少？
   
&nbsp;&nbsp;&nbsp;&nbsp; `345612`

2. How many domains did UrlScan.io identify on the screenshot?
   
   UrlScan.io 螢幕截圖中標識了多少個域 ？
   
&nbsp;&nbsp;&nbsp;&nbsp; `13`

3. What was the main domain registrar listed on the screenshot?
   
   屏幕截圖中列出的 Domain 網域註冊者是什麼 ？
   
&nbsp;&nbsp;&nbsp;&nbsp; `NAMECHEAP INC`

4. What was the main IP address identified for TryHackMe on the screenshot?
   
   屏幕截圖中為 TryHackMe 辨識的主要 IP 位址是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `2606:4700:10::ac43:1b0a`

>> #### Task 4：Abuse.ch

🧠 **Abuse.ch**

- 瑞士伯恩應用科技大學資安研究項目
- 專為 **追蹤惡意程式與指揮控制伺服器（C2）** 設計的免費資源

---

🧭五大資源整理筆記：

| 平台名稱                  | 功能說明                                                   | 重點用途                |
| --------------------- | ------------------------------------------------------ | ------------------- |
| 🧪 **MalwareBazaar**  | 惡意程式樣本分享與分析平台，可上傳、搜尋、獵捕（tag、YARA、AV）                   | 惡意程式樣本收集與分析         |
| 🕸️ **Feodo Tracker** | 專注於追蹤 **Dridex / Emotet / TrickBot / QakBot** 等 C2 伺服器 | 追蹤殭屍網路 C2 IP，提供封鎖清單 |
| 🔒 **SSL Blacklist**  | 提供惡意 SSL 憑證與 JA3 指紋的阻擋清單                               | 用於偵測 / 阻擋異常 TLS 通訊  |
| 🌐 **URLhaus**        | 分享並搜尋惡意 URL，含國別、TLD、ASN 搜尋與匯出                          | 判斷是否為惡意載毒連結         |
| 🦊 **ThreatFox**      | 提供多格式的 IOC（Indicators of Compromise）分享與查詢              | 快速導出 IOC，用於威脅獵捕     |

---

**MalwareBazaar**：
- 功能：
    - 上傳與查找惡意程式
    - 支援 tag、YARA、ClamAV、AV 供應商標記
    - 提供 API 與自動化分析功能
- 用途：惡意樣本分析、自動化威脅情資收集

<p align="left">
  <img src="/rooms/images/25_04.gif" width="600">
</p>

---

**Feodo Tracker**：
- 對象：Dridex、Emotet（Heodo）、TrickBot、QakBot、BazarLoader
- 資源：
  - 最新與歷史 C2 IP 查詢
  - 封鎖清單（CSV、Firewall、IDS ）
用途：用於阻擋知名殭屍網路通訊

<p align="left">
  <img src="/rooms/images/25_05.gif" width="600">
</p>

---

**SSL Blacklist**：
- 功能：
  - 收集 **惡意 SSL 憑證 + JA3/JA3s 指紋**
  - 可匯出 denylist 供 IDS / SIEM 使用
- 用途：阻擋 TLS 連線下的惡意流量、識別 C2 溝通

<p align="left">
  <img src="/rooms/images/25_06.gif" width="600">
</p>

---

**URLhaus**：
- 資源：
    - 惡意網址資料庫，可查 URL、domain、hash
    - 提供國別、ASN、TLD 搜尋與 RSS / CSV 匯出
- 用途：調查載毒網站、封鎖惡意檔案來源

<p align="left">
  <img src="/rooms/images/25_07.gif" width="600">
</p>

---

**ThreatFox**：
- 支援格式：
  - MISP、Suricata、CSV、JSON、DNS RPZ
- 功能：
  - 查詢並匯出 IOC：IP、domain、URL、file hash 等
- 用途：IOC 情資整合、威脅偵測規則建立

<p align="left">
  <img src="/rooms/images/25_08.gif" width="600">
</p>

---
🧰 使用情境舉例：

| 情境                       | 使用平台            |
| ------------------------ | --------------- |
| 想知道一個 URL 是否為惡意載毒連結      | `URLHaus`       |
| 想查詢某個 IP 是否是知名 botnet C2 | `Feodo Tracker` |
| 想搜尋某惡意樣本的變體              | `MalwareBazaar` |
| 想建立 TLS 封鎖清單來阻擋異常通訊      | `SSL Blacklist` |
| 想一次導出所有可用 IOC，建立防禦規則     | `ThreatFox`     |

---

Question 1：進入 ThreatFox 網站資料庫，以語法 IOC:IP 搜尋，並找出其別名

<p align="left">
  <img src="/rooms/images/25_09.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/25_10.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/25_11.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/25_12.png" width="600">
</p>

Question 2：進入 SSL blacklist 網站之 JA3 指紋資料庫，搜尋題目給予之指紋，找出相關連之惡意軟體

<p align="left">
  <img src="/rooms/images/25_13.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/25_14.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/25_15.png" width="600">
</p>

Question 3：進入 URL haus 網站之統計數據，根據題目找到 ASN 編號 AS14061，找到其惡意軟體託管之網路

<p align="left">
  <img src="/rooms/images/25_16.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/25_17.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/25_18.png" width="600">
</p>

Question 4：進入 Feodo Tracker 之網站資料庫，搜尋題目給予之 IP，找出其相關國家

<p align="left">
  <img src="/rooms/images/25_19.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/25_20.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/25_21.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/25_22.png" width="600">
</p>


##### 🔐 答題：

1. The IOC 212.192.246.30:5555 is identified under which malware alias name on ThreatFox?
   
   IOC 212.192.246.30:5555 在 ThreatFox 上被標示的惡意軟體別名為何？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Katana`

2. Which malware is associated with the JA3 Fingerprint 51c64c77e60f3980eea90869b68c58a8 on SSL Blacklist?
   
   哪個惡意軟體與 SSL 黑名單上的 JA3 指紋 51c64c77e60f3980eea90869b68c58a8 相關聯？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Dridex`

3. From the statistics page on URLHaus, what malware-hosting network has the ASN number AS14061? 
   
   從 URLHaus 上的統計資訊頁面中，哪個惡意軟體託管之網路，託管了 ASN 編號 AS14061？ 
   
&nbsp;&nbsp;&nbsp;&nbsp; `DIGITALOCEAN-ASN`

4. Which country is the botnet IP address 178.134.47.166 associated with according to FeodoTracker? 
   
   根據 FeodoTracker 的統計，殭屍網路 IP 位址 178.134.47.166 與哪個國家/地區有關？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Georgia`

>> #### Task 5：網路釣魚工具

🧠 Email Phishing 總覽

**Email Phishing（電子郵件釣魚）** 是一種社交工程攻擊，攻擊者偽裝成可信對象，誘導收件人點擊連結、開啟附件或洩漏敏感資訊。

---

🎯 攻擊目的：
- 植入惡意程式（Malware）
- 收集帳號密碼（Credential Harvesting）
- 金融詐騙
- 資料外洩或勒索攻擊

---

🛠️ PhishTool 工具總覽

| 功能區塊                       | 說明                                |
| -------------------------- | --------------------------------- |
| **分析郵件**                   | 解析郵件的標頭、連結、附件、內容，辨識攻擊意圖與行為        |
| **Heuristic Intelligence** | 整合 OSINT 資源，自動提供威脅來源與可能的 TTP 解析   |
| **分類與報告**                  | 依據分析結果標記為惡意/可疑/安全，產出可供調查與訓練用的鑑識報告 |

---

🧰 社群版功能（免費）：
- 上傳 .eml 郵件檔案進行分析
- 顯示 Headers、Security、Attachments、Message URLs
- 產出標記與解決報告（Resolution）

🏢 企業版額外功能：
- 整合 Gmail / Microsoft 365
- 管理用戶回報信件
- 回饋調查結果給使用者


 PhishingTool 查看 Email 的 Plaintext 和 Source 詳細資訊：
<p align="left">
  <img src="/rooms/images/25_31.gif" width="600">
</p>

---

🔎 Email 分析重點欄位

| 分析區塊                   | 重點檢查項目                                       |
| ---------------------- | -------------------------------------------- |
| **Headers**            | 檢查來源信箱、真實 IP、時間戳記，偵測冒用寄件者                    |
| **Received**           | SMTP 傳遞路徑，追蹤信件是否經過異常跳板                       |
| **X-Headers**          | 收件伺服器加上的額外資訊（如安全過濾記錄、Spam Score）             |
| **Security**           | 檢查 SPF、DKIM、DMARC 是否通過驗證                     |
| **Attachments**        | 列出所有檔案，確認是否有惡意可執行檔或帶毒文件                      |
| **Message URLs**       | 所有信中連結，搭配 URLScan、VirusTotal 驗證              |
| **Plaintext / Source** | 查看郵件原始碼，檢查是否有隱藏 script 或 base64 資料段          |
| **Resolve**            | 設定結案判斷（Phishing、Malware、Safe 等），供內部記錄與報告生成使用 |

---

💡 實務應用建議

當你接到 **.eml 信件樣本**：

1. 先用 **Thunderbird** 開啟查看基本資訊
2. 丟進 **PhishTool** 進行進階分析與解析
3. 補充查詢連結 / 雜湊值：
   - urlscan.io
   - VirusTotal
   - Abuse.ch

---

Question 1 - 3：打開 Emails 資料夾，選取 `Email1.eml`，右鍵以 Thunderbird Mail 開啟

<p align="left">
  <img src="/rooms/images/25_23.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/25_24.png" width="600">
</p>
    
<p align="left">
  <img src="/rooms/images/25_25.png" width="600">
</p>

Question 4：在郵件顯示器的 `More` 中，找到 `View source`，查看原始 IP 地址為何？

<p align="left">
  <img src="/rooms/images/25_26.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/25_27.png" width="600">
</p>

`204.93.183.11` 可能為是原始 IP 位址。它是第一個提到的非內部 IP，表示電子郵件的來源或首次處理的伺服器。

從題目提示中，開啟 `https://gchq.github.io/CyberChef/` ，對該 IP 進行 Defang 處理，得到原始 IP 地址

<p align="left">
  <img src="/rooms/images/25_28.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/25_29.png" width="600">
</p>

Question 5：在郵件顯示器的 `More` 中，找到 `View source`，找到該郵件經過多少躍點到達收件者

<p align="left">
  <img src="/rooms/images/25_30.png" width="600">
</p>

##### 🔐 答題：
1. What social media platform is the attacker trying to pose as in the email?
   
   攻擊者試圖在電子郵件中偽裝成哪個社交媒體平臺？
   
&nbsp;&nbsp;&nbsp;&nbsp; `LinkedIn`

2. What is the senders email address?
   
   寄件者的電子郵件地址是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `darkabutla@sc500.whpservers.com`

3. What is the recipient's email address?
   
   收件者的電子郵件地址是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `cabbagecare@hotsmail.com`

4. What is the Originating IP address? Defang the IP address.
   
   什麼是原始 IP 位址？Defang 該 IP 位址。
   
&nbsp;&nbsp;&nbsp;&nbsp; `204[.]93[.]183[.]11`

5. How many hops did the email go through to get to the recipient?
   
   電子郵件經過多少個躍點才到達收件者？
   
&nbsp;&nbsp;&nbsp;&nbsp; `4`

>> #### Task 6：Cisco Talos 情報

>> #### Task 7：場景 1

>> #### Task 8：場景 2

>> #### Task 9：結論
