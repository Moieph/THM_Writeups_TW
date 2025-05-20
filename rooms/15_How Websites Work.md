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

---

>> #### Task 2：HTML (Hypertext Markup Language)

🌐 建立網站的**三大技術**：
- HTML：建構網頁結構
- CSS：美化網頁外觀
- JavaScript：讓網頁具有互動功能

---

HTML 基本結構：

````
<!DOCTYPE html>     <!-- 定義為 HTML5 文件 -->
<html>              <!-- 根元素 -->
  <head>            <!-- 頁面資訊，例如標題 -->
  </head>
  <body>            <!-- 頁面主要內容 -->
    <h1>標題</h1>   <!-- 大標題 -->
    <p>段落</p>     <!-- 文字段落 -->
  </body>
</html>
````

---

🏷️ 常見標籤與屬性：
- `<button>`：**按鈕**
- `<div>` : division，意思是 **「區塊 / 區段」**
- `<img src="img/cat.jpg">`：**圖片**，src 是圖片路徑
- `<p class="bold-text">`：class 用來**套用 CSS 樣式**
- `<p id="example">`：id 用於唯一識別元素，常**搭配 JavaScript 使用**

---

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

---
<details>
<summary><strong>🔗 JavaScript 的使用方式：</strong></summary>

- 直接寫在 `<script>` 標籤中
- 或用外部檔案引入： `<script src="/js/filename.js"></script>`

---

🧪 實例 1：改變文字內容 <br>
`document.getElementById("demo").innerHTML = "Hack the Planet";`

---

🧪 實例 2：點擊事件改變文字 <br>
`<button onclick='document.getElementById("demo").innerHTML = "Button Clicked";'>Click Me!</button>`

---
📌 常見事件（event）：<br>
事件可以寫在 HTML 元素上，也可以寫在 `<script>` 裡

- onclick：點擊
- onhover：滑鼠懸停

</details>

---

Question 1：在第九行輸入<br>
`document.getElementById("demo").innerHTML = "Hack the Planet";`

<p align="left">
  <img src="/rooms/images/15_04.png" width="600">
</p>

##### 🔐 答題：
1. Click the "View Site" button on this task. On the right-hand side, add JavaScript that changes the demo element's content to "Hack the Planet"
   
   按下此工作上的 「View Site」 按鈕。在右側，添加 JavaScript，將 demo 元素的內容更改為 “Hack the Planet”
   
&nbsp;&nbsp;&nbsp;&nbsp; `JSISFUN`

>> #### Task 4：敏感數據洩露

🚨 什麼是敏感資料外洩？
- 指網站未妥善保護敏感資訊，讓使用者能直接在**前端原始碼**中看到
- 資料通常明文（clear-text）出現，容易被攻擊者利用

---

🕵️‍♂️ 常見錯誤情況：
- HTML 或 JavaScript 原始碼中留有：
  - 登入帳號/密碼
  - 測試用帳號
  - 隱藏功能連結（如 admin 頁面）
  - 註解裡的內部資訊（如 `<!-- TODO: remove test credentials admin:password123 -->`)

---

🔓 攻擊者如何利用？
- 使用「檢視原始碼」功能，查看 HTML / JS 內容
- 搜尋可疑的文字、註解、ID、URL
- 找到登入資訊或內部連結 ➜ 登入系統 ➜ 橫向移動（Lateral Movement）或進一步滲透

---

🔍 評估安全：
- 檢查網頁原始碼是否外洩以下內容：
   - 登入憑證 / API 金鑰
   - 管理後台連結
   - 測試用帳密或功能
   - 註解中的敏感資訊

---

✅ 預防方式
- 上線前移除測試帳號與註解
- 不在前端寫入敏感資料
- 重要資料請透過後端驗證與傳遞

---

Question 1：

<p align="left">
  <img src="/rooms/images/15_05.png" width="600">
</p>

##### 🔐 答題：
1. View the website on this link. What is the password hidden in the source code?
   
   通過此連結查看網站。原始碼中隱藏的密碼是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `testpasswd`

>> #### Task 5：HTML 注入

💥 什麼是 HTML Injection？
- 一種前端漏洞。
- 當網站**未過濾使用者輸入**，直接在頁面上顯示時，就可能被注入 HTML 或 JavaScript 代碼。