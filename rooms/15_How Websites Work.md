# How Websites Work

**🌐 網站如何運作**

THM路徑：https://tryhackme.com/room/howwebsiteswork

官方影片：https://youtu.be/iWoiwFRLV4I?si=xJ_OV03qaR59MEiw

---

>> #### Task 1：網站如何運作

網站由兩大主要部分組成：
- 前端（Client-Side）：瀏覽器呈現網站的方式。
- 後端（Server-Side）：伺服器接收請求、處理後回傳資料。

你在瀏覽器發出請求後，伺服器會回應資料，瀏覽器再根據資料呈現畫面。

<p align="left">
  <img src="/rooms/images/15_01.png" width="600">
</p>

##### 🔐 答題：
1. What term best describes the component of a web application rendered by your browser?
   
   哪個術語最能描述瀏覽器呈現的 Web 應用程式元件？
   
&nbsp;&nbsp;&nbsp;&nbsp; `front end`

>> #### Task 2：HTML (Hypertext Markup Language)

🌐 建立網站的**三大技術**：
- HTML：建構網頁結構
- CSS：美化網頁外觀
- JavaScript：讓網頁具有互動功能

---

HTML 基本結構：

````
<!DOCTYPE html>      <!-- 定義為 HTML5 文件 -->
<html>               <!-- 根元素 -->
  <head>             <!-- 頁面資訊，例如標題 -->
  </head>
  <body>             <!-- 頁面主要內容 -->
    <h1>標題</h1>    <!-- 大標題 -->
    <p>段落</p>      <!-- 文字段落 -->
  </body>
</html>
````

---

🏷️ 常見標籤與屬性：
- `<button>`：**按鈕**
- `<img src="img/cat.jpg">`：**圖片**，src 是圖片路徑
- `<p class="bold-text">`：class 用來**套用 CSS 樣式**
- `<p id="example">`：id 用於唯一識別元素，常**搭配 JavaScript 使用**

Question 2：

<p align="left">
  <img src="/rooms/images/15_02.png" width="600">
</p>

Question 3：

<p align="left">
  <img src="/rooms/images/15_03.png" width="600">
</p>

##### 🔐 答題：
2. One of the images on the cat website is broken - fix it, and the image will reveal the hidden text answer!
   
   貓咪網站上的一張圖片壞了 - 修復它，圖片就會露出隱藏的文字答案！
   
&nbsp;&nbsp;&nbsp;&nbsp; `HTMLHERO`

3. Add a dog image to the page by adding another img tag (`<img>`) on line 11. The dog image location is img/dog-1.png. What is the text in the dog image?
   
   通過在第 11 行添加另一個 img 標籤，向頁面添加狗圖像 <`img`>。狗的圖像位置為 img/dog-1.png。狗圖片中的文字是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `DOGHTML`

>> #### Task 3：JavaScript

💡 JavaScript 是什麼？
- **JavaScript（JS）** 是全球最流行的程式語言之一
- 專門用來讓網頁「有互動性」
- 搭配 **HTML** 使用，讓靜態網頁變成動態互動頁面

---

⚙️ JavaScript 可以做什麼？
- 實現 **點擊按鈕改變文字、滑鼠移動觸發動畫**
- 即時更新頁面內容（無需重新載入）
- 例如：按鈕被點擊時，改變樣式或顯示新文字


>> #### Task 4：敏感數據洩露

>> #### Task 5：HTML 注入

<!--
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
   
&nbsp;&nbsp;&nbsp;&nbsp; `TTL`

2. What type of DNS Server is usually provided by your ISP?
   
   您的 ISP 通常提供什麼類型的 DNS 伺服器？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Recursive`

3. What type of server holds all the records for a domain?
   
   什麼類型的伺服器保存域的所有記錄？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Authoritative`

>> #### Task 5：實際操作

打開右側網站實作。

Question 1：

<p align="left">
  <img src="/rooms/images/14_02.png" width="600">
</p>

Question 2：

<p align="left">
  <img src="/rooms/images/14_03.png" width="600">
</p>

Question 3：

<p align="left">
  <img src="/rooms/images/14_04.png" width="600">
</p>

Question 4：

<p align="left">
  <img src="/rooms/images/14_04.png" width="600">
</p>

Question 5：

<p align="left">
  <img src="/rooms/images/14_05.png" width="600">
</p>

##### 🔐 答題：
1. What is the CNAME of shop.website.thm?
   
   shop.website.thm 的別名記錄是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `shops.myshopify.com`

2. What is the value of the TXT record of website.thm?
   
   website.thm 的 TXT 記錄值是多少？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{7012BBA60997F35A9516C2E16D2944FF}`

3. What is the numerical priority value for the MX record?
   
   MX 記錄的數字優先順序值是多少？
   
&nbsp;&nbsp;&nbsp;&nbsp; `30`

4. What is the IP address for the A record of www.website.thm?
   
   www.website.thm 的 A 記錄的 IP 地址是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `10.10.10.10`