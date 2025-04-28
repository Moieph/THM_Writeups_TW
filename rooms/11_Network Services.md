# Network Services

**🌐 網路服務**

THM路徑：https://tryhackme.com/room/networkservices

---

>> #### Task 1：建立聯繫

>> #### Task 2：瞭解 SMB

<details>
<summary><strong>伺服器訊息塊協定（SMB）</strong></summary>

- Server Message Block<br><strong>是一種用來在網路中分享資源的通訊協定</strong>

✅ 功能包括：
- 檔案共享（File Sharing）
- 印表機共享（Printer Sharing）
- 存取串列埠（Serial Port）
- 管道與 API 存取（Named Pipes / APIs）

---

SMB 讓「用戶端」能從遠端「像操作本機一樣」存取伺服器上的資源
</details>

<details>
<summary><strong>SMB 運作方式</strong></summary>

- SMB 是一種「**請求-回應協定**（Response-Request Protocol）」
- 用戶端（Client）和伺服器（Server）透過多次訊息互動建立連線
- 通訊協定底層可透過：
  - **TCP/IP（最常見，含 NetBIOS over TCP/IP）**
  - NetBEUI（較舊）
  - IPX/SPX（較罕見）

---

建立連線後，用戶端可以：

- 開啟遠端共享資料夾
- 閱讀 / 寫入檔案
- 操作共享印表機或資源
- 像使用自己電腦一樣操作伺服器資源（但是在網路上完成的！）

</details>


<details>
<summary><strong> 💻 誰在使用 SMB？</strong></summary>

| 作業系統 / 工具 | 說明 |
|----------------|------|
| **Windows**    | 從 Windows 95 開始即內建 SMB 支援 |
| **Samba**      | 開源實作，讓 Linux/Unix 也能支援 SMB 協定（可當成 SMB 伺服器） |

🧠 延伸知識

- SMB 也常見於內網滲透測試中，如利用漏洞進行：
    - **SMB Relay 攻擊**
    - **未授權存取共享資料夾**
    - **利用弱密碼登入取得資料**
- 知名漏洞：EternalBlue（MS17-010） 針對 SMB

</details>

##### 🔐 答題：
1. What does SMB stand for?  
   
   SMB 代表什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Server Message Block`

2. What type of protocol is SMB?
   
   SMB 是什麼類型的協定？
   
&nbsp;&nbsp;&nbsp;&nbsp; `response-request`

3. What protocol suite do clients use to connect to the server?    
   
   用戶端使用什麼協定套件連接到伺服器？
   
&nbsp;&nbsp;&nbsp;&nbsp; `TCP/IP`

4. What systems does Samba run on? 
   
   Samba 可以在哪些系統上運行？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Unix`



>> #### Task 3：枚舉 SMB

- **`nmap` ：掃描網路開放的服務與主機**

| 功能             | 指令                                      | 解說                             |
|------------------|-------------------------------------------|----------------------------------|
| 探測主機是否在線 | `nmap -sn 192.168.1.0/24`                 | 只 Ping 掃，不掃 port（-sn = --sP） |
| 快速掃描常見 port | `nmap <IP>`                               | 掃描 1000 個常見 port             |
| 全 Port 掃描     | `nmap -p- <IP>`                            | 掃 0~65535 所有 port              |
| 指定 Port        | `nmap -p 22,80,443 <IP>`                  | 只掃特定 port                     |
| 指定 Port        | `nmap -sV -p 21 <IP>`                     | 掃描特定 port 的版本              |


- **`enum4linux`：枚舉（列舉）Windows SMB 資訊**

| 參數 | 功能說明 |
|------|----------|
| `-U` | 獲取使用者清單（User list） |
| `-M` | 獲取機器名稱清單（Machine list） |
| `-N` | 傾印名稱清單（Name list dump，與 `-U`、`-M` 不同） |
| `-S` | 獲取共享資源清單（Share list） |
| `-P` | 顯示密碼政策資訊（Password policy） |
| `-G` | 顯示群組與成員清單（Group + Members） |
| `-a` | 執行以上所有功能（全自動基本列舉） |


---

Question 1、2：對靶機執行`nmap`掃描，找到 3 個 Port 和 SMB 在哪個 Port 上運行

<p align="left">
  <img src="/rooms/images/11_01.jpg" width="600">
</p>

Question 3：對靶機執行`enum4linux`，枚舉靶機的 SMB 資訊，得到工作群組名稱
<p align="left">
  <img src="/rooms/images/11_02.jpg" width="600">
</p>

Question 4：在 NetBIOS Name Table 中，機器的名稱會出現在 `00`、`03`、`20`。
結合 OS Information，判斷主機名稱為`POLOSMB`。

- `<00>`  Workstation Service（工作站服務名稱）<br>→ 通常代表主機名稱
- `<03>` Messenger Service（訊息傳遞）
- `<20>`  File Server Service（檔案分享服務）<br>→ 檔案伺服器名稱

<p align="left">
  <img src="/rooms/images/11_03.jpg" width="600">
</p>

<p align="left">
  <img src="/rooms/images/11_07.jpg" width="600">
</p>

Question 5：查看系統版本
<p align="left">
  <img src="/rooms/images/11_04.jpg" width="600">
</p>

Question 6：靶機允許匿名登錄 <br>
`username''`、`password''`

`/profiles Mapping: OK, Listing: OK`<br>`

- 「Mapping」= 允許掛載（連線）到該 SMB 分享
- 「Listing」= 允許列出該分享資料夾的檔案與內容

<p align="left">
  <img src="/rooms/images/11_05.jpg" width="600">
</p>

<p align="left">
  <img src="/rooms/images/11_06.jpg" width="600">
</p>

##### 🔐 答題：
1. Conduct an nmap scan of your choosing, How many ports are open?
   
    執行您選擇的 nmap 掃描，打開了多少個埠？
   
&nbsp;&nbsp;&nbsp;&nbsp; `3`

2. What ports is SMB running on? Provide the ports in ascending order.
   
    SMB 在哪些埠上運行？按升序提供埠。
   
&nbsp;&nbsp;&nbsp;&nbsp; `139/445`

3. Let's get started with Enum4Linux, conduct a full basic enumeration. For starters, what is the workgroup name?    
   
    讓我們從 Enum4Linux 開始，進行一個完整的基本枚舉。工作群組名稱是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `WORKGROUP`

4. What comes up as the name of the machine? 
   
    機器的名稱是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `POLOSMB`

5. What operating system version is running?    
   
    運行的是什麼作系統版本 ？
   
&nbsp;&nbsp;&nbsp;&nbsp; `6.1`

6. What share sticks out as something we might want to investigate?    
   
    哪些分享資料夾值得我們調查？
   
&nbsp;&nbsp;&nbsp;&nbsp; `profiles`

>> #### Task 4：利用 SMB

`smbclient`： 連接 SMB 分享的命令列工具

`smbclient //[IP]/[SHARE] -User -Port`

---

Question 3：透過`smbclient`匿名訪問靶機後，輸入`help`確認可以使用哪些指令：

<p align="left">
  <img src="/rooms/images/11_08.png" width="600">
</p>

Question 4：輸入`more "Working From Home Information.txt` 讀取該文字檔：

<p align="left">
  <img src="/rooms/images/11_09.png" width="600">
</p>

Question 5、6：SMB 共享之 profiles 屬於 John Cactus 且公司還為他配置 ssh 服務：（按`Q`退出`more`模式）

<p align="left">
  <img src="/rooms/images/11_10.png" width="600">
</p>

Question 7：前往 .ssh 資料夾輸入`get id_rsa`下載私鑰到虛擬機上

- 查看 .ssh 文件夾：「id_rsa」文件為私鑰、「id_rsa.pub」文件為公鑰
- 在 「id_rsa.pub」 公鑰文件的內容末尾，可能會注明和密鑰相關的ssh用戶名稱
- 在 SMB 連接中，使用`get`命令下載文件

<p align="left">
  <img src="/rooms/images/11_11.png" width="600">
</p>

Question 8：更改 id_rsa 為 600

<p align="left">
  <img src="/rooms/images/11_12.jpg" width="600">
</p>


- Linux 權限說明：

| 數字 | 對應權限 | 說明       |
|------|----------|------------|
| 7    | rwx      | 讀寫執行   |
| 6    | rw-      | 讀寫       |
| 5    | r-x      | 讀 + 執行  |
| 4    | r--      | 只有讀     |
| 0    | ---      | 無權限     |

- `600` 意思為：

| 使用者       | 權限          |
|--------------|---------------|
| 擁有者（你） | 讀 & 寫 ✅    |
| 群組         | 沒有 ❌       |
| 其他人       | 沒有 ❌       |

Question 8：Task 3 透過`enum4linux`枚舉，發現有效帳戶名稱為 cactus，並嘗試以其私鑰 id_rsa 登入 ssh 服務


<p align="left">
  <img src="/rooms/images/11_13.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/11_14.png" width="600">
</p>

登入後，以 `ls` 列出檔案，`cat` smb.txt，獲得 Flag 🎉🎉

<p align="left">
  <img src="/rooms/images/11_15.png" width="600">
</p>


##### 🔐 答題：
1. What would be the correct syntax to access an SMB share called "secret" as user "suit" on a machine with the IP 10.10.10.2 on the default port?
   
    在預設埠上具有 IP 為 10.10.10.10.2 的電腦上，以使用者「suit」身份訪問名為「secret」的 SMB 共用的正確語法是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `smbclient //10.10.10.2/secret -U suit -p 445`

3. Does the share allow anonymous access? Y/N?
   
    共用是否允許匿名訪問？是/否？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Y`

4. Great! Have a look around for any interesting documents that could contain valuable information. Who can we assume this profile folder belongs to?
   
    太好了！環顧四周，尋找任何可能包含有價值資訊的有趣文檔。我們可以假設這個配置檔資料夾屬於誰？
   
&nbsp;&nbsp;&nbsp;&nbsp; `John Cactus`

5. What service has been configured to allow him to work from home?
   
    配置了哪些服務以允許他在家工作？
   
&nbsp;&nbsp;&nbsp;&nbsp; `ssh`

6. Okay! Now we know this, what directory on the share should we look in?
   
    好！現在我們知道了，我們應該查看共用上的哪個目錄？
   
&nbsp;&nbsp;&nbsp;&nbsp; `.ssh`

7. This directory contains authentication keys that allow a user to authenticate themselves on, and then access, a server. Which of these keys is most useful to us?
   
    此目錄包含允許使用者在伺服器上對自己進行身份驗證，然後訪問伺服器的身份驗證密鑰。這些鍵中哪一個對我們最有用？
   
&nbsp;&nbsp;&nbsp;&nbsp; `id_rsa`

8. What is the smb.txt flag?
   
    什麼是 smb.txt 的旗子？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{smb_is_fun_eh?}`

>> #### Task 5：瞭解 Telnet
連線語法：`telnet [ip] [port]”`

---

Telnet 漏洞類型（Types of Telnet Exploit）

1. Telnet 本身的不安全性：
    - ❌ **沒加密** → 所有資料明文傳送（帳密可被攔截）
    - ❌ **存取控制薄弱** → 常見弱密碼或匿名登入
    - ❌ **常被錯誤設定** → 最容易被攻擊的點！
2. CVE 漏洞庫（可查 Telnet 相關漏洞）
    - https://www.cvedetails.com/
    - https://cve.mitre.org/<br>CVE（Common Vulnerabilities and Exposures）是已公開安全漏洞編號，每編號對應一種弱點。
3. ✅ 實戰中更常遇到的情況是：
    - 配置錯誤（如帳號沒設密碼、用戶名硬編在服務裡）
    - 被當作後門或 debug 用途埋在奇怪 port

##### 🔐 答題：
1. What is Telnet?      
   
   什麼是 Telnet？
   
&nbsp;&nbsp;&nbsp;&nbsp; `application protocol`

2. What has slowly replaced Telnet?     
   
    是什麼慢慢取代了 Telnet？
   
&nbsp;&nbsp;&nbsp;&nbsp; `ssh`

3. How would you connect to a Telnet server with the IP 10.10.10.3 on port 23?
   
    您將如何連接到埠 23 上 IP 為 10.10.10.3 的 Telnet 伺服器？
   
&nbsp;&nbsp;&nbsp;&nbsp; `telnet 10.10.10.3 23`

4. The lack of what, means that all Telnet communication is in plaintext?  
   
    缺少什麼，意味著所有 Telnet 通信都是明文的？
   
&nbsp;&nbsp;&nbsp;&nbsp; `encryption`


>> #### Task 6：枚舉 Telnet

Question 1 - 4：`nmap -p- 靶機IP` 進行全端口掃描，發現 8012 端口有開；`nmap 靶機IP` 快速掃瞄 1000 個常用端口，未發現開啟端口。

<p align="left">
  <img src="/rooms/images/11_16.png" width="600">
</p>

Question 6、7：進階掃描 8012端口 `nmap -A -p 8012 -T4 靶機IP`

- fingerprint-string：**指紋字串**，是 nmap 主動送出一些常見的連線請求，看伺服器回什麼反應
- X11Probe：nmap 嘗試模仿「X11 圖形界面」的連線行為，結果**有回應（正規服務不該有反應）**
- SKIDY'S BACKDOOR：8012 port 上可能藏有漏洞或惡意服務！

<p align="left">
  <img src="/rooms/images/11_17.png" width="600">
</p>

##### 🔐 答題：
1. How many ports are open on the target machine?    
   
    目標計算機上打開了多少個埠 ？
   
&nbsp;&nbsp;&nbsp;&nbsp; `1`

2. What port is this?
   
    這是什麼埠 ？
   
&nbsp;&nbsp;&nbsp;&nbsp; `8012`

3. This port is unassigned, but still lists the protocol it's using, what protocol is this?     
   
    此埠未分配，但仍列出它使用的協定 ，這是什麼協定？
   
&nbsp;&nbsp;&nbsp;&nbsp; `tcp`

4. Now re-run the nmap scan, without the -p- tag, how many ports show up as open?
   
    現在重新運行 nmap 掃描，沒有 -p- 標籤，有多少個埠顯示為打開？
   
&nbsp;&nbsp;&nbsp;&nbsp; `0`

6. Based on the title returned to us, what do we think this port could be used for?
   
    根據返回給我們的標題，我們認為這個埠可以用來做什麼 ？
   
&nbsp;&nbsp;&nbsp;&nbsp; `a backdoor`

7. Who could it belong to? Gathering possible usernames is an important step in enumeration.
   
    它可能屬於誰？收集可能的使用者名是枚舉中的一個重要步驟。
   
&nbsp;&nbsp;&nbsp;&nbsp; `Skidy`

>> #### Task 7：利用 Telnet

>> #### Task 8：瞭解 FTP

>> #### Task 9：枚舉 FTP

>> #### Task 11：利用 FTP

