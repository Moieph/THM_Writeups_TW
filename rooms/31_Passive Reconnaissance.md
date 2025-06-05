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
  <img src="/rooms/images/30_13.png" width="600">
</p>

找到註冊時間及註冊商網址

<p align="left">
  <img src="/rooms/images/30_14.png" width="600">
</p>

找到名稱伺服器網址

<p align="left">
  <img src="/rooms/images/30_15.png" width="600">
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


>> #### Task 5：DNSDumpster

>> #### Task 6：Shodan.io

>> #### Task 7：總結