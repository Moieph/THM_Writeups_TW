# Putting it all together

**🌐 把全部放在一起**

THM路徑：https://tryhackme.com/room/puttingitalltogether

官方影片：https://youtu.be/Aa_FAA3v22g?si=s_DE2vG42xf-O36S

---

>> #### Task 1：把它們放在一起

🧠 網頁載入流程總結：
1. **DNS 查詢**：電腦透過 DNS 找到網站伺服器的 IP 位址
2. **HTTP 通訊**：使用 HTTP 協定與伺服器溝通
3. **資料回傳**：伺服器回傳 HTML、CSS、JavaScript 等內容
4. **瀏覽器呈現**：瀏覽器解析並顯示完整網頁

<p align="left">
  <img src="/rooms/images/16_01.png" width="600">
</p>

>> #### Task 2：其他元件

**Load Balancer（負載平衡器）**

- 目的：
    - 分散流量，避免單一伺服器過載
    - 提供故障轉移（Failover）功能

- 機制：
    - 輪詢（Round-robin）：依序分配請求
    - 加權（Weighted）：根據伺服器忙碌程度分配
    - 健康檢查（Health Check）：定期確認伺服器是否正常，異常就停止分流

<p align="left">
  <img src="/rooms/images/16_02.png" width="600">
</p>

---

**CDN（內容傳遞網路）**

- **Content Delivery Networks**
- 功能：全球部署伺服器，讓使用者從最近的節點獲取靜態資源（如圖、JS、CSS）

- 優點：
  - 減少主站流量
  - 加快載入速度
  - 增加可用性

---

**資料庫（Databases）**
- 功能：儲存與讀取用戶資料

- 類型：從簡單文字檔到大型叢集系統
    - 常見種類：
      - MySQL、MSSQL（關聯式）
      - MongoDB（NoSQL） 
      - Postgres（開源強大）

---

**WAF（Web 應用防火牆）**

- **Web Application Firewall**
- 位置：位於 **使用者請求與 Web Server 中間**
- 功能：
  - 偵測與阻擋攻擊（如 SQL injection、DDoS）
  - **Rate Limiting**：限制每秒同一 IP 的請求數
  - 可辨別是否來自真實瀏覽器或機器人

<p align="left">
  <img src="/rooms/images/16_03.png" width="600">
</p>

##### 🔐 答題：
1. What can be used to host static files and speed up a clients visit to a website?
   
   什麼可用於託管靜態檔並加快客戶訪問網站的速度？
   
&nbsp;&nbsp;&nbsp;&nbsp; `CDN`

2. What does a load balancer perform to make sure a host is still alive?
   
   負載均衡器執行哪些作來確保主機仍處於活動狀態？
   
&nbsp;&nbsp;&nbsp;&nbsp; `health check`

3. What can be used to help against the hacking of a website?
   
   什麼可以説明防止網站被駭客入侵？
   
&nbsp;&nbsp;&nbsp;&nbsp; `WAF`

>> #### Task 3：伺服器的工作原理

🌐 什麼是 Web Server？
- 軟體，透過 **HTTP 協定** 傳送網頁內容給使用者。
- 常見軟體：**Apache、Nginx、IIS、NodeJS**
- 預設根目錄（儲存網站檔案的地方）：
  - Linux：`/var/www/html`
  - Windows（IIS）：`C:\inetpub\wwwroot`
- 如請求 http://example.com/pic.jpg → 傳送 `/var/www/html/pic.jpg`

---

🏠 Virtual Hosts（虛擬主機）
- 可在同一台伺服器上架設**多個網站**（不同域名）
- 根據 HTTP 請求的 **hostname** 判斷要回應哪個網站
- 每個虛擬主機可設定不同的根目錄
  - 例：
    - one.com → `/var/www/website_one`
    - two.com → `/var/www/website_two`

---

- 📄 靜態內容（Static Content）：
  - 永遠不變，直接從硬碟送出。
    - 如：圖片、CSS、JavaScript、固定 HTML

- ⚙️ 動態內容（Dynamic Content）：
  - 根據請求內容改變畫面
  - 變化由後端程式語言控制
    - 例如：首頁顯示最新文章，或搜尋結果建議

---

🧠 後端（Backend）與前端（Frontend）
- 前端（Frontend）：<br>瀏覽器看到的畫面（HTML、CSS、JS）
- 後端（Backend）：<br>伺服器端的運算與資料處理，用來產生前端畫面
- 使用者看不到後端程式碼，只看到產生的結果

---

💻 常見後端語言
- PHP、Python、Ruby、NodeJS、Perl 等
  - 處理資料庫互動
  - 接收並處理使用者輸入
  - 呼叫外部服務

---

網址：`http://example.com/index.php?name=adam`
- `index.php` → 網站要執行的檔案<br>
- `?name=adam` → 給網站的參數（用來帶資料）
-  GET 方法（使用網址傳參數）

**PHP 程式碼：**<br>
`<html><body>Hello <?php echo $_GET["name"]; ?></body></html>`

- `$_GET["name"]`：從網址參數中抓出「name」的值（也就是 "adam"）<br>
- `echo`：把抓到的字印出來

**輸出：**<br>
`<html><body>Hello adam</body></html>`

👉 使用者看不到 `<?php echo $_GET["name"]; ?>`，因爲是後端在處理

---

##### 🔐 答題：
1. What does web server software use to host multiple sites?
   
   Web 伺服器軟體使用什麼來託管多個網站？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Virtual Hosts`

2. What is the name for the type of content that can change?
   
   可以更改的內容類型的名稱是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Dynamic`

3. Does the client see the backend code? Yay/Nay
   
   用戶端是否看到後端代碼？是/否
   
&nbsp;&nbsp;&nbsp;&nbsp; `Nay`

>> #### Task 4：測驗

<p align="left">
  <img src="/rooms/images/16_04.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/16_05.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/16_06.png" width="600">
</p>

##### 🔐 答題：
1. Flag？

   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{YOU_GOT_THE_ORDER}`
