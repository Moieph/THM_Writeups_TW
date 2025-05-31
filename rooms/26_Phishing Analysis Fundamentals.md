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
➜ Internet Message Format

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


Email Header 裡的資訊：
<p align="left">
  <img src="/rooms/images/26_02.png" width="600">
</p>

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

---

🧠 例子解析（視覺化）

```
From: newsletters@ant.anki-tech.com  
Reply-To: reply@ant.anki-tech.com  
```

👉 使用者會以為是在與「newsletters@」對話，實際上點擊「回覆」會發送到 reply@，這是常見的誘導式詐騙手法。

---

Question 1：檢視題目給予之文章 https://web.archive.org/web/20221219232959/https://mediatemple.net/community/products/all/204643950/understanding-an-email-header
<br>
找到與`Reply-To`相同的 Header 資訊

<p align="left">
  <img src="/rooms/images/26_03.png" width="600">
</p>

Question 2：同題目一，找到該敘述

<p align="left">
  <img src="/rooms/images/26_04.png" width="600">
</p>

##### 🔐 答題：
1. What email header is the same as "Reply-to"?
   
   什麼 Email Header 與 「Reply-to」 相同？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Return-Path`

2. Once you find the email sender's IP address, where can you retrieve more information about the IP?
   
   找到電子郵件寄件者的 IP 位址後，您可以在哪裡檢索有關該 IP 的更多資訊？
   
&nbsp;&nbsp;&nbsp;&nbsp; `http://www.arin.net`

>> #### Task 5：電子郵件正文

✉️ Email Body 的兩種格式

| 格式類型           | 說明                                  |
| -------------- | ----------------------------------- |
| **Plain Text** | 單純文字內容，無樣式、無超連結、無圖像。                |
| **HTML 格式**    | 支援圖像、樣式、超連結、JavaScript（危險點）、甚至嵌入表單。 |

Plain Text：
<p align="left">
  <img src="/rooms/images/26_05.png" width="600">
</p>

HTML 格式：
<p align="left">
  <img src="/rooms/images/26_06.png" width="600">
</p>

---

🖼️ HTML Email Body 解析

HTML 格式 Email 可包含：
- `<img>`：嵌入圖片（可能是追蹤像素）
- `<a href>`：可疑的釣魚連結
- `<form>`：可用來騙取帳號密碼
- `<script>`（有些被濾掉）：風險極高

---

📎 附件分析：關鍵 Headers

當 Email 含有附件時，會出現如下結構：

````
Content-Type: application/pdf;
Content-Disposition: attachment; filename="invoice.pdf"
Content-Transfer-Encoding: base64

JVBERi0xLjQKJeLjz9MNCjEgMCBvYmoKPD...
````
| 欄位                            | 說明                          |
| ----------------------------- | --------------------------- |
| **Content-Type**              | 附件格式（如 PDF、DOCX、EXE）        |
| **Content-Disposition**       | 是否為附件（`attachment`）或 inline |
| **Content-Transfer-Encoding** | 通常為 `base64`，代表可轉換為原始檔案     |
| **Filename**                  | 顯示的檔名，可偽裝成安全文件但實為惡意         |

<p align="left">
  <img src="/rooms/images/26_07.png" width="600">
</p>

---

⚠️ 實戰警告
- 千萬不要隨意點開 .html 附件或未知檔案，即使表面是 PDF，也可能是偽裝。
- 即使只是「開啟 HTML 預覽」也有風險（如圖片請求含追蹤器）。
- 若需分析，**可離線解碼 base64**，切勿直接雙擊執行！

---

🧰 附件分析工具（進階建議）

- **base64 解碼器**（如 CyberChef、base64 -d）
- **PDF 分析器**：pdfid.py、pdf-parser.py
- **OLE 工具（分析 Word 附件）**：oletools
- **Hybrid Analysis / Any.Run / VirusTotal**（上傳可疑附件測試）

---

Question 1：根據題目給予之截圖，找出被阻擋圖片的 URL

<p align="left">
  <img src="/rooms/images/26_08.png" width="600">
</p>

Question 2：根據題目給予之截圖，找出附件的名稱

<p align="left">
  <img src="/rooms/images/26_09.png" width="600">
</p>

Question 3：啟動虛擬機，找到 `Email sample` 資料夾中的 `email2.txt`

<p align="left">
  <img src="/rooms/images/26_10.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/26_11.png" width="600">
</p>

將 txt 檔案內的頭、尾部分刪除，只留下 Attachment 的 Base64 

<p align="left">
  <img src="/rooms/images/26_12.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/26_13.png" width="600">
</p>

前往 https://base64.guru/converter/decode/pdf <br>
將 Base64 轉為 PDF

<p align="left">
  <img src="/rooms/images/26_14.png" width="600">
</p>

##### 🔐 答題：
1. In the above screenshots, what is the URL of the blocked image?
   
   在上面的屏幕截圖中，被阻止的圖像的 URL 是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `https://i.imgur.com/LSWOtDI.png`

2. In the screenshots above, what is the name of the PDF attachment?
   
   在上面的螢幕截圖中，PDF 附件的名稱是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Payment-updateid.pdf`

3. In the attached virtual machine, view the information in email2.txt and reconstruct the PDF using the base64 data. What is the text within the PDF?
   
   在連接的虛擬機中，查看 email2.txt 中的資訊，並使用 base64 數據重新構建 PDF。PDF 中的文本是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{BENIGN_PDF_ATTACHMENT}`

>> #### Task 6：網路釣魚的類型

📌 惡意電子郵件類型對照表

| 類型                 | 說明                                          |
| ------------------ | ------------------------------------------- |
| **Spam**           | 大量散佈、未經請求的垃圾郵件。行銷/廣告內容為主。                   |
| **MalSpam**        | 搭載惡意附件或連結的垃圾郵件（例如 ransomware、木馬）。           |
| **Phishing**       | 冒充知名品牌或單位，誘騙使用者洩漏密碼、信用卡等敏感資訊。               |
| **Spear Phishing** | 精準鎖定特定個人或部門（如人資、財務）進行社交工程攻擊。                |
| **Whaling**        | Spear phishing 的高階版，針對 CEO、CFO 等高層主管設計的釣魚信。 |
| **Smishing**       | SMS + Phishing。透過簡訊詐騙手法，引誘點擊惡意連結。           |
| **Vishing**        | Voice + Phishing。用語音（通常是假冒銀行、政府機關）進行詐騙。     |

---

🧠 釣魚郵件常見特徵清單

| 特徵               | 判斷方式舉例                                             |
| ---------------- | -------------------------------------------------- |
| 寄件者名稱與 Email 不一致 | 顯示名為 Amazon，實際 email 卻是 `support@evil.biz`         |
| 標題/內容帶有急迫感       | `URGENT: Your Account Has Been Suspended!`         |
| 使用品牌 LOGO 與設計模仿  | 偽造 Amazon、Google 等 UI，但排版略顯粗糙                      |
| 內容語法錯誤 / 翻譯機文句   | `Your password is been expired, reset immediatly.` |
| 問候語過於通用          | `Dear User`、`Dear Sir/Madam`                       |
| 短網址 / 偽裝超連結      | `http://bit.ly/2i83sk` 實為 `http://malicious.ru`    |
| 附件偽裝成文檔          | `Invoice_2024.pdf.exe`、`Payment_Info.zip`          |

---

🛡️ Defanging：安全轉發技巧

避免誤擊連結或執行惡意程式，可使用「Defang」(CyberChef) 

| 原始內容                         | Defang 後                       |
| ---------------------------- | ------------------------------ |
| `http://malicious.com/login` | `hxxp://malicious[.]com/login` |
| `192.168.1.1`                | `192[.]168[.]1[.]1`            |
| `user@example.com`           | `user[at]example[.]com`        |

---

Question 1 - 3：啟動虛擬機，找到 `Email sample` 資料夾中的 `email3.eml`


<p align="left">
  <img src="/rooms/images/26_15.png" width="600">
</p>

以其他應用程式 `Thunderbird Mail` 開啟

<p align="left">
  <img src="/rooms/images/26_16.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/26_17.png" width="600">
</p>

從寄件人找到其偽裝的公司名稱、來源信箱及主旨

<p align="left">
  <img src="/rooms/images/26_18.png" width="600">
</p>

Question 4：將鼠標移到 `CLICK HERE`，下方顯示其 URL 為 `http://t.teckbe.com`

<p align="left">
  <img src="/rooms/images/26_19.png" width="600">
</p>

到 https://gchq.github.io/CyberChef/ 裡面 defang 該 URL  

<p align="left">
  <img src="/rooms/images/26_20.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/26_21.png" width="600">
</p>

##### 🔐 答題：
1. What trusted entity is this email masquerading as?
   
   這封電子郵件偽裝成什麼受信任的實體？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Home Depot`

2. What is the sender's email?
   
   寄件者的電子郵件是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `support@teckbe.com`

3. What is the subject line? 
   
   主旨是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Order Placed : Your Order ID OD2321657089291 Placed Successfully`

4. What is the website for the - `CLICK HERE` URL in a defanged format?
   
   `CLICK HERE` URL 的 defanged 格式是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `hxxp[://]t[.]teckbe[.]com`

>> #### Task 7：結論

✅ 商業電子郵件詐騙（BEC）簡介

**Business Email Compromise（BEC）** 是一種高階詐騙手法，攻擊者透過下列方式操控公司內部流程：

- 🔓 入侵公司內部員工的信箱（通常是主管或財務部門）
- 📧 用該信箱發送可信指令，如要求匯款、變更帳戶資料
- 💸 員工因信任該帳號，執行非法操作（如匯款到攻擊者帳戶）

---

🎯 常見 BEC 攻擊對象：

- CEO / CFO（假冒下指令）
- 財務部門（執行匯款）
- HR（取得員工資料）
- 法務（更改合約文件）

---

##### 🔐 答題：
1. What is BEC?
   
   什麼是 BEC？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Business Email Compromise`