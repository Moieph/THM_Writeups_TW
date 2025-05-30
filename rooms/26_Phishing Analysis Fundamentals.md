# Phishing Analysis Fundamentals

**🟦 Phishing Analysis 基礎知識**

THM路徑：https://tryhackme.com/room/phishingemails1tryoe

---

>> #### Task 1：介紹
> 
📧 Spam vs. Phishing：

| 類型           | 說明                                               |
| ------------ | ------------------------------------------------ |
| **Spam**     | 廣告性質的垃圾信，一般無害但大量佔用資源                             |
| **Phishing** | 釣魚攻擊，**偽裝成合法對象誘導使用者點擊惡意連結或執行附件**，可造成入侵、資料外洩等嚴重後果 |

---

🧠 為什麼要重視釣魚信？

- 即使公司部署了多層資安防禦（防毒、EDR、郵件閘道等），只要一位員工點錯連結或執行附件，攻擊者就有可能進入內網、橫向移動，甚至勒索整個系統。

---

🔍 安全分析師要做什麼？

當懷疑信件有問題時，你的任務是：

1. 分析信件內容與標頭（Header）


2. 判斷其是否為釣魚 / 惡意信


3. 找出指標（IOC，如寄件 IP、連結、附件 Hash）


4. 將資訊回饋至資安產品（EDR, SIEM, 郵件防護）更新防禦策略

---

🛠️ 分析釣魚信的常見工具

| 工具/平台       | 功能簡介                     |
| ----------- | ------------------------ |
| Thunderbird | 檢視 .eml 電子郵件原始內容         |
| PhishTool   | 免費釣魚信分析工具，支援標頭解析、附件/連結提取 |
| VirusTotal  | 對附件 / 網域 / IP 做惡意偵測      |
| Abuse.ch    | 查 IOC 是否與知名惡意活動有關        |
| Cisco Talos | 查寄件者 IP / 網域是否有惡意聲譽紀錄    |

---

📬 Email Headers 重點分析欄位

| 欄位名稱             | 功能                                  |
| ---------------- | ----------------------------------- |
| `From:`          | 寄件人名稱（可能偽造）                         |
| `Return-Path:`   | 真實的回信位址，通常為實際來源                     |
| `Received:`      | **郵件經過的每一台 SMTP 伺服器紀錄**，倒序排列，可追查來源路徑 |
| `Message-ID:`    | 唯一訊息編號，可用來查對是否為假冒                   |
| `SPF/DKIM/DMARC` | 是否通過寄件網域驗證政策（失敗代表可能是詐騙或偽造）          |


>> #### Task 2：電子郵件位址

📬 Email 是誰發明的？

- 發明人：**Ray Tomlinson**
- 時間：1970 年代，基於 ARPANET
- 他也讓 @ 符號 成為 email 的核心

---

✉️ 一個 Email Address 的結構

舉例：billy@johndoe.com

| 部分            | 說明                              |
| ------------- | ------------------------------- |
| `billy`       | **使用者信箱（Username / Mailbox）**   |
| `@`           | 分隔符號，由 Ray Tomlinson 引入         |
| `johndoe.com` | **網域（Domain）**，代表 email 所屬伺服器位置 |

📦 類比郵差送信：

- 網域 = 街道名
- 使用者名稱 = 門牌號碼 + 收件人
- 郵差透過這資訊投遞正確的信箱


##### 🔐 答題：
1. Email dates back to what time frame?
   
   電子郵件可以追溯到什麼時間範圍？
   
&nbsp;&nbsp;&nbsp;&nbsp; `1970s`

>> #### Task 3：電子郵件發送

📡 Email 傳輸三大協議

| 協議名稱                                           | 功能            | 說明                       | 預設 Port        |
| ---------------------------------------------- | ------------- | ------------------------ | -------------- |
| **SMTP**<br>(Simple Mail Transfer Protocol)    | **寄出**郵件      | 從寄件人發送郵件到收件人的郵件伺服器       | 25 / 587（推薦）   |
| **POP3**<br>(Post Office Protocol v3)          | **接收**郵件（單機）  | 郵件會下載到單一裝置並從伺服器刪除（若未設保留） | 110 / 995（SSL） |
| **IMAP**<br>(Internet Message Access Protocol) | **接收**郵件（多裝置） | 郵件保留在伺服器，可多裝置同步查看        | 143 / 993（SSL） |

---

📥 POP3 vs IMAP 對照表

| 功能     | POP3               | IMAP     |
| ------ | ------------------ | -------- |
| 郵件存放位置 | 單一裝置               | 雲端伺服器    |
| 傳送郵件記錄 | 僅在寄件裝置上有           | 保存在伺服器   |
| 多裝置同步  | ❌ 不支援              | ✅ 支援     |
| 預設行為   | 下載後刪除伺服器郵件（除非設定保留） | 郵件留在伺服器上 |

---

📤 Email 發送流程（簡化版）

1️⃣ Alexa 用 email client 撰寫信件並按下「傳送」。<br>
2️⃣ SMTP 伺服器查詢 johndoe.com 的 DNS 記錄。<br>
3️⃣ DNS 回傳 johndoe.com 的 mail server 資訊。<br>
4️⃣ SMTP 發送信件，橫跨多個中繼站。<br>
5️⃣ 抵達收件方的 SMTP 伺服器。<br>
6️⃣ 郵件進入 POP3/IMAP server。<br>
7️⃣ Billy 啟動 email client，向伺服器查詢是否有新郵件。<br>
8️⃣ 郵件透過 IMAP 複製或 POP3 下載到 Billy 的裝置。

<p align="left">
  <img src="/rooms/images/26_01.png" width="600">
</p>

##### 🔐 答題：
1. What port is classified as Secure Transport (STARTTLS) for SMTP?
   
   哪個埠被歸類為 SMTP 的安全傳輸 （STARTTLS）
   
&nbsp;&nbsp;&nbsp;&nbsp; `587`

2. What port is classified as Secure Transport for IMAP?
   
   哪個埠被歸類為 IMAP 的安全傳輸？
   
&nbsp;&nbsp;&nbsp;&nbsp; `993`

3. What port is classified as Secure Transport for POP3?
   
   哪個埠被歸類為 POP3 的安全傳輸？
   
&nbsp;&nbsp;&nbsp;&nbsp; `995`

>> #### Task 4：電子郵件標頭

📬 Email 組成結構（IMF 格式）


- **Email Header**（標頭）：說明信件是誰寄的、從哪裡來、經過哪些伺服器等資訊


- **Email Body**（內文）：信件的主體（純文字或 HTML）

---

🔍 Email Header 常見欄位說明

| 欄位名稱                            | 說明                                           |
| ------------------------------- | -------------------------------------------- |
| **From**                        | 寄件人的信箱地址（表面上看到的）                             |
| **To**                          | 收件人的信箱地址                                     |
| **Subject**                     | 郵件主旨                                         |
| **Date**                        | 寄出時間                                         |
| **Reply-To**                    | 點擊「回覆」後會寄到的地址（可與 From 不同）                    |
| **X-Originating-IP**            | 發件端的實際 IP（常見於可疑信）                            |
| **smtp.mailfrom / header.from** | SMTP 驗證使用的寄件者網域，位於 Authentication-Results 中  |
| **Received**                    | 郵件傳遞的每一跳紀錄（由哪個 mail server 傳給哪個 mail server） |
| **Message-ID**                  | 郵件唯一識別碼，可用來追查是否偽造                            |
| **DKIM / SPF / DMARC**          | 驗證結果，用來判斷該郵件是否經過偽造或通過寄件者認證                   |

---

🧠 實際分析技巧

- Step 1: 開啟原始郵件

   使用 Thunderbird、Outlook 或 Gmail 可點選**「檢視原始資料」** 看到完整 Header


- Step 2: 優先觀察以下欄位：

  - **From vs smtp.mailfrom / header.from** → 一致嗎？

  - **Reply-To 是否與 From 不同？** → 可疑的 redirect。

  - **X-Originating-IP** → 查 IP 地理位置和 ASN。

  - **Received 欄位有幾段？經過哪些伺服器？**

  - **Authentication-Results** → SPF、DKIM、DMARC 是否 pass？
    - ❌ fail 時通常是仿冒詐騙的強烈跡象



>> #### Task 5：電子郵件正文

>> #### Task 6：網路釣魚的類型

>> #### Task 7：結論