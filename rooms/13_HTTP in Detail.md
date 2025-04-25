# Http in Detail

**📡 HTTP 詳細資訊**

THM路徑：https://tryhackme.com/room/httpindetail

官方影片：https://youtu.be/XZyapIKV3Rw?si=auDQQuXpd-wBoyFv

---

>> #### Task 1：什麼是 HTTP（S）？

- HTTP（HyperText Transfer Protocol，超文字傳輸協定）
    - 是一種用來**瀏覽網頁的通訊協定**
    - 由 Tim Berners-Lee 及其團隊於 1989～1991 年開發
    - 用來與 **Web 伺服器溝通**，以傳輸網頁資料，例如：
      - **HTML 文件**
      - **圖片**
      - **影片**


- HTTPS（HyperText Transfer Protocol Secure，安全超文字傳輸協定）
  - 是 **HTTP 的加密版。**
  - 具備兩大特性：
    - **資料加密**：防止其他人偷看你與網站之間的資料內容（包含你傳送與接收的資料）。
    - **身份驗證**：確認你連接的是正確的網站伺服器，不是被冒充的假網站。

<p align="left">
  <img src="/rooms/images/13_01.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/13_02.png" width="600">
</p>

##### 🔐 答題：
1. What does HTTP stand for?
   
   HTTP 代表什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `HyperText Transfer Protocol`

2. What does the S in HTTPS stand for?
   
   HTTPS 中的 S 代表什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `secure`

1. On the mock webpage on the right there is an issue, once you've found it, click on it. What is the challenge flag?
   
   在右側的類比網頁上有一個問題，一旦你找到它，就點擊它。什麼是挑戰旗子？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{INVALID_HTTP_CERT}`

>> #### Task 2：請求和回應    

<details>
<summary><strong>URL</strong></summary>
Uniform Resource Locator，統一資源定位符

- URL 就是你在**瀏覽器輸入的網站地址**，例如：https://tryhackme.com
- **讓瀏覽器知道「要去哪裡找資料」的指令**，用來存取網路上的資源

<p align="left">
  <img src="/rooms/images/13_03.png" width="600">
</p>

| 部分名稱        | 說明                                                                 |
|----------------|----------------------------------------------------------------------|
| **Scheme**     | 通訊協定（例如 `http`、`https`、`ftp`）告訴瀏覽器用哪種方式連線。          |
| **User:Pass**  | 使用者帳號與密碼（部分服務需要驗證身份）。                             |
| **Host**       | 主機名稱，例如 `tryhackme.com`，也可以是 IP 位址。                    |
| **Port**       | 連接的「埠號」，常見的有：HTTP 用 80，HTTPS 用 443。                 |
| **Path**       | 檔案或資源的位置，例如 `/view-room`。                                |
| **Query String** | 查詢字串，傳遞額外資料，例如 `?id=1` 是告訴網站你要查 `id=1` 的資料。 |
| **Fragment**   | 網頁中的定位錨點，例如 `#task3`，讓你直接跳到某個區塊。                |

</details>

```
GET / HTTP/1.1
# 此請求發送 GET 方法（有關此內容的更多信息，請參閱HTTP方法任務），使用 / 請求主頁並告知 Web 伺服器我們正在使用HTTP協定版本 1.1。

Host: tryhackme.com
# 我們告訴 Web 伺服器我們想要造訪網站 tryhackme.com

User-Agent: Mozilla/5.0 Firefox/87.0
# 我們告訴 Web 伺服器我們正在使用 Firefox 87 版瀏覽器

Referer: https://tryhackme.com/
# 我們告訴 Web 伺服器，引導我們造訪此網頁的頁面是https://tryhackme.com
# HTTP請求始終以空白行結束，以通知 Web 伺服器請求已完成。
```

```
HTTP/1.1 200 OK                 
# 狀態行：使用 HTTP/1.1 協議，200 表示請求成功 (OK)

Server: nginx/1.15.8           
# 伺服器軟體是 nginx，版本為 1.15.8

Date: Fri, 09 Apr 2021 13:34:03 GMT  
# 回應的時間（世界標準時間 GMT）

Content-Type: text/html        
# 回傳的內容類型是 text/html，也就是網頁

Content-Length: 98             
#回傳的資料長度為 98 bytes（字節）


<html>                        
# <!-- HTML 主體開始 -->
<head>
    <title>TryHackMe</title>   
    # <!-- 瀏覽器標籤顯示的標題 -->
</head>
<body>
    Welcome To TryHackMe.com   
    # <!-- 實際在網頁中看到的內容 -->
</body>
</html>                        
# <!-- HTML 主體結束 -->
```
📦 小結：

| 項目               | 說明                                                       |
|--------------------|------------------------------------------------------------|
| `200 OK`           | 成功拿到首頁                                               |
| 回傳內容           | React SPA 的 HTML 頁面                                     |
| 一長串 JavaScript  | Cloudflare、Intercom、TryHackMe 的追蹤腳本                 |
| 看起來「不友善」？ | 因為是用 CLI，不會 render HTML，直接噴文字給你             |


##### 🔐 答題：
1. What HTTP protocol is being used in the above example?
   
   上面的例子中使用了什麼 HTTP 協定？
   
&nbsp;&nbsp;&nbsp;&nbsp; `HTTP/1.1`

2. What response header tells the browser how much data to expect?
   
   什麼回應標頭告訴瀏覽器預期多少數據？

&nbsp;&nbsp;&nbsp;&nbsp; `Content-Length`

>> #### Task 3：HTTP 方法

| 方法    | 用途說明                                     | 是否改變伺服器資料？          | 常見用途                       |
|---------|----------------------------------------------|-------------------------------|--------------------------------|
| GET     | 從伺服器「取得」資源                         | ❌（讀取而已）                 | 瀏覽網頁、API 查詢             |
| POST    | 傳送資料到伺服器，新增或處理資料             | ✅（通常會新增）               | 表單送出、註冊帳號、登入       |
| PUT     | 傳送資料到伺服器，整體更新現有資源           | ✅（會改變資料）               | 編輯用戶資料、更新整筆資訊     |
| PATCH   | 局部更新資源（只改部分欄位）                 | ✅（會改變資料）               | 更新用戶的單一欄位（如名字）   |
| DELETE  | 要求伺服器「刪除」指定資源                   | ✅（會刪除資料）               | 刪除帳號、移除某個評論         |
| HEAD    | 和 GET 類似，但只要回應 headers，不取回內容 | ❌                             | 測試資源是否存在、抓檔案大小   |
| OPTIONS | 詢問伺服器支援哪些 HTTP 方法                 | ❌                             | CORS 預檢請求（跨來源請求）    |

##### 🔐 答題：
1. What method would be used to create a new user account?
   
   使用什麼方法創建新的用戶帳戶？
   
&nbsp;&nbsp;&nbsp;&nbsp; `POST`

2. What method would be used to update your email address?
   
   將使用什麼方法更新您的電子郵件位址？
   
&nbsp;&nbsp;&nbsp;&nbsp; `PUT`

3. What method would be used to remove a picture you've uploaded to your account?
   
   使用什麼方法刪除您上傳到帳戶的圖片？
   
&nbsp;&nbsp;&nbsp;&nbsp; `DELETE`

4. What method would be used to view a news article?
   
   使用什麼方法查看新聞文章？
   
&nbsp;&nbsp;&nbsp;&nbsp; `GET`

>> #### Task 4：HTTP 狀態碼

| 範圍 | 類別說明        | 常見碼 | 說明                                   |
|------|------------------|--------|----------------------------------------|
| 1xx  | 🌀 資訊回應       | 100    | Continue：繼續請求                     |
| 2xx  | ✅ 成功處理       | 200    | OK：成功                                |
|      |                  | 201    | Created：成功建立（如帳號）             |
| 3xx  | 🌫️ 重定向        | 301    | Moved Permanently：永久搬家             |
|      |                  | 302    | Found：臨時搬家                         |
| 4xx  | ❌ 用戶端錯誤     | 400    | Bad Request：請求格式錯                 |
|      |                  | 401    | Unauthorized：需要登入認證             |
|      |                  | 403    | Forbidden：禁止訪問（即使有登入）       |
|      |                  | 404    | Not Found：找不到資源                   |
|      |                  | 405    | Method Not Allowed：方法錯誤（ex. 用 GET 打 POST） |
| 5xx  | 💥 伺服器錯誤     | 500    | Internal Server Error：伺服器爆炸       |
|      |                  | 503    | Service Unavailable：維護中或爆掉       |

🧠 小技巧記憶法：
- 2xx = 成功
- 3xx = 轉址
- 4xx = 你錯了
- 5xx = 伺服器錯了


##### 🔐 答題：
1. What response code might you receive if you've created a new user or blog post article?
   
   如果您創建了新使用者或博客文章，您可能會收到什麼回應代碼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `201`

2. What response code might you receive if you've tried to access a page that doesn't exist?
   
   如果您嘗試存取不存在的頁面，您可能會收到什麼回應代碼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `404`

3. What response code might you receive if the web server cannot access its database and the application crashes?
   
   如果 Web 伺服器無法存取資料庫並且應用程式崩潰，您可能會收到什麼回應代碼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `503`

4. What response code might you receive if you try to edit your profile without logging in first?
   
   如果您嘗試在未先登錄的情況下編輯個人資料，您可能會收到什麼回應代碼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `401`

>> #### Task 5：Headers

- Request Headers（客戶端 ➜ 伺服器）

| Header 名稱        | 功能說明                                                  |
|--------------------|-----------------------------------------------------------|
| `Host`             | 指定目標主機（多網站共用 IP 時必要）                     |
| `User-Agent`       | 告訴伺服器你用的瀏覽器及版本                             |
| `Content-Length`   | 傳送資料長度（例如送表單）                               |
| `Accept-Encoding`  | 指定瀏覽器支援的壓縮方式（gzip、deflate 等）             |
| `Cookie`           | 用戶端帶回的識別資料（登入狀態、偏好等）                |


- Response Headers（伺服器 ➜ 客戶端）

| Header 名稱         | 功能說明                                                        |
|---------------------|-----------------------------------------------------------------|
| `Set-Cookie`        | 設定 Cookie，讓瀏覽器下次帶回                                 |
| `Cache-Control`     | 告訴瀏覽器是否 & 多久可以快取資源                             |
| `Content-Type`      | 告訴瀏覽器這是什麼類型的資料（HTML、JS、PDF...）              |
| `Content-Encoding`  | 資料是否壓縮，以及使用哪種壓縮方法                             |


🔹 小重點補充：
- **Request Header** =「你送什麼」，可自訂（如curl、Postman）
- **Response Header** =「伺服器回什麼」，看伺服器的設定
- Headers 是滲透測試和偵錯時的重要線索（如 Cookie、伺服器型號、編碼方式）

##### 🔐 答題：
1. What header tells the web server what browser is being used?
   
   哪個標頭告訴 Web 伺服器正在使用哪個瀏覽器？
   
&nbsp;&nbsp;&nbsp;&nbsp; `User-Agent`

2. What header tells the browser what type of data is being returned?
   
   哪個標頭告訴瀏覽器返回什麼類型的數據？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Content-Type`

3. What header tells the web server which website is being requested?
   
   哪個標頭告訴 Web 伺服器正在請求哪個網站？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Host`

>> #### Task 6：Cookies
_<strong>Cookie 是一小段由伺服器發送、儲存在你電腦（瀏覽器）裡的資料</strong>，可用來「記住你是誰」、「儲存網站設定」、「追蹤登入狀態」等_


🕵️ Cookie 運作

1. 你請求一個網站
2. 伺服器回應時，用 Set-Cookie 標頭，儲存一個 Cookie
3. 之後每次發送請求，瀏覽器會帶上 Cookie（用 Cookie 標頭送回）

---

因為 HTTP 是「無狀態（Stateless）」的協議，伺服器不會記住你，所以 Cookie 就是「你的身分證」

---
🍪 Cookie 常見用途：

| 🧠 用途       | 說明                                                                 |
|-------------|----------------------------------------------------------------------|
| **登入驗證** | 儲存登入後的 `session token`，讓伺服器知道你是誰                            |
| **偏好設定** | 像是網站語言、主題模式、介面選擇等                                     |
| **瀏覽記錄** | 例如購物車、上次看過的商品等                                           |

---

Cookie 的樣子（例子）：<br>
`Set-Cookie: sessionid=abc123xyz; Path=/; HttpOnly`

之後你發送請求時，瀏覽器會自動加上<br>
`Cookie: sessionid=abc123xyz`

---

🧰 如何查看 Cookie：
    
  1. 開啟瀏覽器開發者工具（Chrome：F12 或右鍵 ➜ 檢查）
  2. 點選「Network」頁籤
  3. 點任一請求（通常是網頁的主文） 
  4. 查看「Cookies」子頁籤 ➜ 就能看到瀏覽器送出的 Cookie！

---

<p align="left">
  <img src="/rooms/images/13_04.png" width="600">
</p>


>> #### Task 7：發出請求


Question 1 ：
<p align="left">
  <img src="/rooms/images/13_05.png" width="600">
</p>

Question 2 ：
<p align="left">
  <img src="/rooms/images/13_06.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/13_07.png" width="600">
</p>

Question 3 ：

<p align="left">
  <img src="/rooms/images/13_08.png" width="600">
</p>

Question 4 ：

<p align="left">
  <img src="/rooms/images/13_09.png" width="600">
</p>

Question 5 ：

<p align="left">
  <img src="/rooms/images/13_11.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/13_12.png" width="600">
</p>


##### 🔐 答題：
1. Make a GET request to /room
   
   向 /room 發出 GET 請求
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{YOU'RE_IN_THE_ROOM}`

2. Make a GET request to /blog and using the gear icon set the id parameter to 1 in the URL field
   
   向 /blog 發出 GET 請求，並使用齒輪圖示在 URL 欄位中將 id 參數設置為 1
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{YOU_FOUND_THE_BLOG}`

3. Make a DELETE request to /user/1
   
   向 /user/1 發出 DELETE 請求
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{USER_IS_DELETED}`

4. Make a PUT request to /user/2 with the username parameter set to admin
   
   向 /user/2 發出 PUT 請求，並將 username 參數設置為 admin
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{USER_HAS_UPDATED}`

5. POST the username of thm and a password of letmein to /login
   
   將 thm 的使用者名和 letmein 的密碼 POST 到 /login
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{HTTP_REQUEST_MASTER}`


 


