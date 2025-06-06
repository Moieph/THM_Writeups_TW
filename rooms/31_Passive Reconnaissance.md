# Passive Reconnaissance

**🟥 被動偵察**

THM路徑：https://tryhackme.com/room/passiverecon

---

>> #### Task 1：介紹

🔧 被動偵察工具（不會驚動目標）：
- `whois`：查詢網域的註冊資訊
- `nslookup` / `dig`：查詢 DNS 記錄

---

🌐 線上服務：
- **DNSDumpster**：DNS 情資查詢工具
- **Shodan.io**：搜尋可公開存取的設備與服務

>> #### Task 2：被動與主動偵察

📖  **偵察**（Reconnaissance）概論：


- 「知己知彼，百戰不殆」——孫子兵法
- 不論攻防，掌握資訊都是關鍵
- 偵察是 **滲透攻擊的第一步**，屬於 **The Unified Kill Chain** 起始階段

---

🔍 偵察分為兩種：

1. **被動偵察**（Passive Reconnaissance）
   - 查詢**公開資訊**，不會與目標互動 
   - 如：
        - 查 DNS 記錄（如：A、MX、NS）
        - 看徵才廣告找出公司使用技術
        - 搜尋新聞與公開文件


2. **主動偵察**（Active Reconnaissance）
    - 直接與目標互動，可能會被發現或觸法
    - 如：
      - 掃描目標伺服器（HTTP、FTP、SMTP 等）
      - 假裝修理人員進入公司
      - 打電話套資訊（社交工程）

⚠️ 主動偵察風險高，需合法授權，否則可能觸法

---

##### 🔐 答題：
1. You visit the Facebook page of the target company, hoping to get some of their employee names. What kind of reconnaissance activity is this? (A for active, P for passive)
   
   您訪問了目標公司的 Facebook 頁面，希望獲得他們的一些員工姓名。這是什麼類型的偵查活動？（A 代表主動，P 代表被動）
   
&nbsp;&nbsp;&nbsp;&nbsp; `P`

2. You `ping` the IP address of the company webserver to check if ICMP traffic is blocked. What kind of reconnaissance activity is this? (A for active, P for passive)
   
   您 `ping` 公司 Web 伺服器的 IP 位址，以檢查 ICMP 流量是否被阻止。這是什麼類型的偵查活動？（A 代表主動，P 代表被動）
   
&nbsp;&nbsp;&nbsp;&nbsp; `P`

3. You happen to meet the IT administrator of the target company at a party. You try to use social engineering to get more information about their systems and network infrastructure. What kind of reconnaissance activity is this? (A for active, P for passive)
   
   您碰巧在聚會上遇到了目標公司的 IT 管理員。您嘗試使用社會工程來獲取有關其系統和網路基礎設施的更多資訊。這是什麼類型的偵查活動？（A 代表主動，P 代表被動）
   
&nbsp;&nbsp;&nbsp;&nbsp; `A`


>> #### Task 3：Whois

📌 WHOIS 是什麼？
- 一種 **查詢網域資訊的通訊協定**（依照 RFC 3912）

- 使用 **TCP port 43** 傳輸請求與回應

- **註冊商**（Registrar） 負責維護該網域的 WHOIS 記錄 

---

🔍 WHOIS 查詢可得資訊：

- **註冊商（Registrar）** 資訊


- **網域持有者（Registrant）** 資訊
    - 姓名、組織、地址、電話等（若未使用隱私保護服務）


- **網域時間紀錄**
    - 註冊時間（Creation Date）
    - 更新時間（Updated Date）
    - 到期時間（Expiration Date）


- **名稱伺服器（Name Server）**
    - 指出 DNS 查詢要問哪一台伺服器

---

🧪 指令用法（Linux 終端機）：

`whois DOMAIN_NAME`

---

Question 1 - 3：啟動終端機，輸入 `whois tryhackme.com`

<p align="left">
  <img src="/rooms/images/31_01.png" width="600">
</p>

找到註冊時間及註冊商網址

<p align="left">
  <img src="/rooms/images/31_02.png" width="600">
</p>

找到名稱伺服器網址

<p align="left">
  <img src="/rooms/images/31_03.png" width="600">
</p>

##### 🔐 答題：
1. When was TryHackMe.com registered?
   
   TryHackMe.com 是什麼時候註冊的？
   
&nbsp;&nbsp;&nbsp;&nbsp; `20180705`

2. What is the registrar of TryHackMe.com?
   
   TryHackMe.com 註冊商是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `namecheap.com`

3. Which company is TryHackMe.com using for name servers?
   
   TryHackMe.com 使用哪家公司作為名稱伺服器？
   
&nbsp;&nbsp;&nbsp;&nbsp; `cloudflare.com`

>> #### Task 4：nslookup、dig

🌐 DNS 查詢工具筆記：`nslookup` & `dig`

---

🧾 `nslookup`（Name Server Lookup）

用來查詢 DNS 紀錄，可指定查詢類型與 DNS 伺服器。



✅ 指令語法：

`nslookup -type=查詢類型 網域名稱 DNS伺服器`


`nslookup -type=A tryhackme.com 1.1.1.1`

`nslookup -type=MX tryhackme.com`


<details>
<summary>常見查詢類型</summary>


| 類型    | 說明       |
| ----- | -------- |
| A     | IPv4 位址  |
| AAAA  | IPv6 位址  |
| MX    | 郵件伺服器    |
| CNAME | 另類名稱（別名） |
| SOA   | 授權起始記錄   |
| TXT   | 自訂文字記錄   |


</details>

---

🔍 `dig`（Domain Information Groper）

功能更強大的 DNS 查詢工具，預設會顯示 TTL 等資訊。

✅ 指令語法：

`dig 網域 查詢類型`

`dig @DNS伺服器 網域 查詢類型`

`dig @1.1.1.1 tryhackme.com MX`

⚠️ 偵察應用小提醒：
- 可藉由 A 查到 IP 進行後續滲透測試
- 可用 MX 查郵件伺服器，觀察是否為舊版或有漏洞的系統
- TXT 記錄有時會揭露設定資訊（如 SPF、Google 驗證碼等）

---

Question 1：開啟虛擬機，輸入`nslookup -type=TXT thmlabs.con`

獲得 Flag 🎉🎉

<p align="left">
  <img src="/rooms/images/31_04.png" width="600">
</p>

##### 🔐 答題：
1. Check the TXT records of thmlabs.com. What is the flag there?
   
   檢查 thmlabs.com 的 TXT 記錄。那裡的旗子是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{a5b83929888ed36acb0272971e438d78}`

>> #### Task 5：DNSDumpster

❓ 為什麼要找子網域？

- 子網域（如 wiki.tryhackme.com, webmail.tryhackme.com）<br>可能暴露額外系統或服務

- 某些子網域未定期更新，可能存在漏洞或弱點

---

🚫 限制：

- `nslookup` 和 `dig` 無法自動列出所有子網域
- 手動查詢各種子網域耗時、低效率

---

🔍 子網域探索方法：

1. **搜尋引擎**

- 用 Google、Bing 等關鍵字搜尋子網域
- 缺點：資料分散，需看很多頁結果

2. **暴力破解法**（Brute Force DNS）

- 使用字典測試常見子網域（如 admin、mail、dev 等）
- 工具如：`Gobuster`、`Sublist3r` 等

3. ✅ **DNSDumpster**（推薦）
- 線上工具，查詢完整 DNS 資訊
- 可查出：
  - 子網域
  -   A、MX、TXT、NS 記錄
  - IP 位址與地理位置
  - 圖形化關係圖（可移動區塊）
  - 部分主機擁有者資訊

---

Question 1：進入 https://dnsdumpster.com/ 

輸入 tryhackme.com 查詢子網域

<p align="left">
  <img src="/rooms/images/31_05.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/31_06.png" width="600">
</p>


##### 🔐 答題：
1. Lookup tryhackme.com on DNSDumpster. What is one interesting subdomain that you would discover in addition to www and blog?
   
   在 DNSDumpster 上查找 tryhackme.com。除了 www 和 blog 之外，您還會發現哪個有趣的子域？
   
&nbsp;&nbsp;&nbsp;&nbsp; `remote`

>> #### Task 6：Shodan.io

🔎 Shodan 是什麼？
- 被稱為「物聯網的 Google」，是一個搜尋連網設備的引擎
- 不像傳統搜尋引擎搜尋網頁，Shodan 專門搜尋：
  - 網路攝影機、工控系統、伺服器、路由器等設備

---

🎯 用途：

1. **滲透測試（被動偵察階段）**
    - 查詢目標設備的：
        - IP 位址
        - 主機位置與託管業者
        - 開放服務 / 伺服器類型與版本
        - SSL/TLS 憑證資訊


2. **防禦面（資安管理）**
    - 瞭解自家有哪些設備暴露在外
    - 偵測誤設、過時設備、未受保護的裝置

---

✅ 補充：
- 可搭配 DNS 查到的 IP 再到 Shodan 搜尋
- 無須付費帳號即可取得大部分資訊
- 進階搜尋語法可參考官方 Help 頁面

---

Question 1 - 3：進入 https://www.shodan.io/

輸入 `Apache` 查詢

<p align="left">
  <img src="/rooms/images/31_07.png" width="600">
</p>

輸入 `nginx` 查詢

<p align="left">
  <img src="/rooms/images/31_08.png" width="600">
</p>

##### 🔐 答題：
1. According to Shodan.io, what is the 2nd country in the world in terms of the number of publicly accessible Apache servers?
   
   根據 Shodan.io 的數據，就可公開訪問的 Apache 伺服器數量而言，世界上排名第二的國家是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `China`

2. Based on Shodan.io, what is the 3rd most common port used for Apache?
   
   根據 Shodan.io，Apache 使用的第 3 個最常見埠是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `8080`

3. Based on Shodan.io, what is the 3rd most common port used for nginx?
   
   根據 Shodan.io，nginx 使用的第 3 個最常見埠是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `5001`

>> #### Task 7：總結

📌 核心概念：

- 被動偵察（Passive Reconnaissance）是**不直接連接目標系統**，但能收集大量資訊的技術，常用於滲透測試或資安評估的初期階段。

---

🛠️ 工具與服務

| 工具 / 服務         | 功能介紹                     |
| --------------- | ------------------------ |
| `whois`         | 查詢網域註冊資訊（註冊商、聯絡資訊、註冊時間）  |
| `nslookup`      | 查詢 DNS 記錄，如 A、MX、TXT 等   |
| `dig`           | 功能更強大的 DNS 查詢工具，支援更多輸出細節 |
| **DNSDumpster** | 線上工具，可視覺化顯示 DNS 架構與子網域資訊 |
| **Shodan.io**   | 搜尋公開連網裝置（如伺服器、攝影機、IoT 等） |
