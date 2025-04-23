# Offensive Security Intro
**🟥 進攻性安全入門**

THM路徑：https://tryhackme.com/room/offensivesecurityintro
>> #### Task 1：進攻性安全介紹

##### 🔐 答題：
1. Which of the following options better represents the process where you simulate a hacker's actions to find vulnerabilities in a system?
   
    以下哪個選項更能代表您模擬駭客查找系統中漏洞的過程？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Offensive Security`

---

>> #### Task 2：入侵你的第一台機器

&nbsp;&nbsp;&nbsp;&nbsp;步驟 1️⃣：打開終端機（Terminal）

&nbsp;&nbsp;&nbsp;&nbsp;步驟 2️⃣：使用 Gobuster 尋找隱藏的網站頁面

&nbsp;&nbsp;&nbsp;&nbsp;  `gobuster -u http://fakebank.thm -w wordlist.txt dir`

<details>
<summary> &nbsp;Gobuster 指令參數解釋</summary>

| **TAG** | **FUNCTION** |
|---------|--------------|
| `-u`    |目標網站的 URL|
| `-w`    |使用的字典清單檔（wordlist.txt） |
| `dir`   |執行目錄掃描模式 |

</details>

<p align="left">
  <img src="/rooms/images/01_01.png" width="600">
</p>

透過字典清單，掃出 `/bank-transfer` 為該網域內的隱藏路徑，HTTP碼狀態碼顯示 200（成功處理）回到瀏覽器輸入 `http://fakebank.thm/bank-transfer`


&nbsp;&nbsp;&nbsp;&nbsp;步驟 3️⃣：從帳號 2276 匯 2000 美元至 8881

<p align="left">
  <img src="/rooms/images/01_03.png" width="600">
</p>

##### 🔐 答題：
1. Above your account balance, you should now see a message indicating the answer to this question. Can you find the answer you need?
   
    在您的帳戶餘額上方，您會看到一條消息，指示此問題的答案。

&nbsp;&nbsp;&nbsp;&nbsp; `BANK-HACKED`

---



