# DNS in Detail

**💻 DNS 詳細資訊**

THM路徑：https://tryhackme.com/room/dnsindetail

官方影片：https://youtu.be/jpTY1S5vs9k?si=JGlGMbYyZBXaa29m

---

>> #### Task 1：什麼是 DNS？

**Domain Name System** = 網際網路的「電話簿」

**📌 主要功能：**
  - 將人類可讀的網址（如 tryhackme.com）
  - ➡️ 轉換成電腦可讀的 IP 位址

🧠 **為什麼需要 DNS？：**
  - IP 位址是每台電腦的唯一地址（像是收件地址）
  - 人類不方便記憶這種數字組合
  - DNS 讓你只需記住「tryhackme.com」就能連到正確的網站

```
IPv4 範例：104.26.10.229
結構：四組數字（0 ~ 255）以句點分隔
```

**🎯 小結：** <br>

- DNS 幫你把「網域名稱」翻譯成「IP 位址」，就像幫你查電話號碼或寄信地址一樣，是現代網路不可或缺的基礎。

##### 🔐 答題：
1. What does DNS stand for?
   
   DNS 代表什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Domain Name System`

>> #### Task 2：域層次結構 

🌍 網域名稱結構總覽：<br>
以`admin.tryhackme.com`為例，結構拆解如下：

```
🔹 Subdomain       ：admin
🔸 Second-Level    ：tryhackme
🔺 Top-Level (TLD)：.com
```

- 🔺 TLD（頂級網域）：<br>
TLD 是網域名稱最右邊的部分，例如：.com、.org、.edu

| 類型   | 說明                             | 範例                    |
|--------|----------------------------------|-------------------------|
| gTLD   | **一般用途（Generic TLD）**     | `.com`, `.org`, `.biz` |
| ccTLD  | **國家代碼（Country Code TLD）** | `.tw`, `.uk`, `.jp`    |

📌 現在已有超過 **2000 種 TLD**，包含 `.online`, `.club` 等新創 TLD。

---

- 🔸 Second-Level Domain（第二層網域）：<br>
這是你實際註冊的主網域，例如 `tryhackme.com` 中的 `tryhackme`

**⚠️ 命名限制：**

- 最長 **63 個字元**（不含 TLD）
- 可使用：`a–z`、`0–9`、`-`（連字號）
- 不可：
  - 以 `-` 開頭或結尾
  - 使用連續兩個 `--`

---

- 🔹 Subdomain（子網域）：<br>
Subdomain 是附加在主網域前方的名稱，例如：<br>
`admin.tryhackme.com` → `admin` 為子網域
`jupiter.servers.tryhackme.com` → 多層子網域

**⚠️ 命名限制：**

- 每層最長 **63 個字元**
- 整體長度不超過 **253 字元**
- 無子網域數量限制
- 命名規則與 **Second-Level Domain** 相同

##### 🔐 答題：
1. What is the maximum length of a subdomain?
   
   子域名的最大長度是多少？
   
&nbsp;&nbsp;&nbsp;&nbsp; `63`

2. Which of the following characters cannot be used in a subdomain ( 3 b _ - )?
   
   以下哪些字元不能在子域 （ 3 b _ - ） 中使用？
   
&nbsp;&nbsp;&nbsp;&nbsp; `_`

3. What is the maximum length of a domain name?
   
   Domain Name 名稱的最大長度是多少？
   
&nbsp;&nbsp;&nbsp;&nbsp; `253`

4. What type of TLD is .co.uk?
   
   .co.uk 是什麼類型的 TLD？
   
&nbsp;&nbsp;&nbsp;&nbsp; `ccTLD`

>> #### Task 3：記錄類型
🌐 DNS 記錄類型（DNS Record Types）：<br>
DNS 不只是解析網站網址，還有多種記錄類型。

---
 🅰️ **A Record（IPv4 解析）**

- ✅ 將網域名稱對應到 **IPv4 位址**
- 📌 範例：`104.26.10.229`

---

**🧱 AAAA Record（IPv6 解析）**

- ✅ 將網域名稱對應到 **IPv6 位址**
- 📌 範例：`2606:4700:0020:0000:0000:0000:681a:0be5`

---

**🔗 CNAME Record（別名記錄）**

- ✅ 將一個網域名稱指向 **另一個網域名稱**
- 📌 範例：`store.tryhackme.com → shops.shopify.com`
- ⚙️ 查出來後會再進行下一次 DNS 查詢以獲得 IP 位址

---

**📧 MX Record（郵件交換記錄）**

- ✅ 指定負責該網域 **收發電子郵件** 的伺服器
- 📌 範例：`alt1.aspmx.l.google.com`
- 🔢 含 **優先順序（priority）**，可指定主伺服器與備援伺服器

---

**📝 TXT Record（文字記錄）**

- ✅ 儲存任意文字型資料，常見用途包括：
  - 📮 驗證哪台伺服器可代表此網域發信（防止詐騙、垃圾郵件）
  - ✅ 驗證網域擁有權（用於第三方服務）

##### 🔐 答題：
1. What type of record would be used to advise where to send email?
   
   將使用什麼類型的記錄來建議將電子郵件發送到何處？
   
&nbsp;&nbsp;&nbsp;&nbsp; `63`

2. What type of record handles IPv6 addresses?
   
   什麼類型的記錄處理 IPv6 位址？
   
&nbsp;&nbsp;&nbsp;&nbsp; `AAAA`

>> #### Task 4：提出請求

<details>
<summary><strong>🌐 DNS 請求流程：</strong></summary>


你輸入網址：www.tryhackme.com：

 1. 本機快取（Local Cache）<br>
    ✅ 有 → 直接回傳 IP（結束）<br>
    ❌ 沒有 → 前往遞迴查詢伺服器<br>


 2. 遞迴 DNS 伺服器（Recursive DNS Server）<br>
    ✅ 有快取 → 回傳 IP（結束）<br>
    ❌ 沒有 → 啟動查詢任務<br>


 3. 根 DNS 伺服器（Root DNS Server）<br>
    - 認出 .com → 回傳：對應 TLD 伺服器<br>


 4. TLD 伺服器（Top-Level Domain Server）<br>
    - 查出：.com 的授權 DNS 是誰


 5. 權威 DNS（Authoritative DNS Server）<br>
    -  取得最終 DNS 紀錄（如 A, CNAME, MX）


 6. 遞迴 DNS 伺服器 <br>
    -  快取結果（依 TTL 秒數）<br>
    -  回傳給原本的用戶端


 7. 使用者電腦取得 IP → 正常瀏覽網頁<br>

</details>

---

**快取與 TTL（Time To Live） ：**<br>
- 每筆 DNS 回應都有 **TTL 值**（以秒為單位）
- 意義是「這筆資料最多可以在本地快取多久」
- TTL 到期後，再次查詢才會重走一次流程

---

快速對應詞彙整理：

| 元件                        | 功能說明                                         |
|-----------------------------|--------------------------------------------------|
| Local Cache                 | 使用者裝置的 DNS 快取                           |
| Recursive DNS Server        | 幫你查到底的遞迴伺服器（通常是 ISP 提供）       |
| Root DNS Server             | 網際網路的根伺服器，指引你去對的 TLD            |
| TLD DNS Server              | 負責 .com、.org、.tw 等頂層網域                 |
| Authoritative Name Server   | 實際儲存某網域 DNS 紀錄的伺服器                 |
| TTL                         | 回應的快取有效時間（秒）                        |

<p align="left">
  <img src="/rooms/images/14_01.png" width="600">
</p>

##### 🔐 答題：
1. What field specifies how long a DNS record should be cached for?
   
   哪個欄位指定 DNS 記錄應緩存多長時間？
   
&nbsp;&nbsp;&nbsp;&nbsp; ``

2. What type of DNS Server is usually provided by your ISP?
   
   您的 ISP 通常提供什麼類型的 DNS 伺服器？
   
&nbsp;&nbsp;&nbsp;&nbsp; ``

3. What type of server holds all the records for a domain?
   
   什麼類型的伺服器保存域的所有記錄？
   
&nbsp;&nbsp;&nbsp;&nbsp; ``

>> #### Task 5：實際操作