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
  <img src="/rooms/images/11_01.png" width="600">
</p>

Question 3：對靶機執行`enum4linux`，枚舉靶機的 SMB 資訊，得到工作群組名稱
<p align="left">
  <img src="/rooms/images/11_02.png" width="600">
</p>

Question 4：在 NetBIOS Name Table 中，機器的名稱會出現在 `00`、`03`、`20`。
結合 OS Information，判斷主機名稱為`POLOSMB`。

- `<00>`  Workstation Service（工作站服務名稱）<br>→ 通常代表主機名稱
- `<03>` Messenger Service（訊息傳遞）
- `<20>`  File Server Service（檔案分享服務）<br>→ 檔案伺服器名稱

<p align="left">
  <img src="/rooms/images/11_03.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/11_07.png" width="600">
</p>

Question 5：查看系統版本
<p align="left">
  <img src="/rooms/images/11_04.png" width="600">
</p>

Question 6：靶機允許匿名登錄 <br>
`username''`、`password''`

`//10.10.42.205/profiles Mapping: OK, Listing: OK`<br>
- 「Mapping」= 允許掛載（連線）到該 SMB 分享
- 「Listing」= 允許列出該分享資料夾的檔案與內容

<p align="left">
  <img src="/rooms/images/11_05.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/11_06.png" width="600">
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
- 在 SMB 連接中，使用get命令下載文件

<p align="left">
  <img src="/rooms/images/11_11.png" width="600">
</p>

Question 8：更改 id_rsa 為 600

<p align="left">
  <img src="/rooms/images/11_12.png" width="600">
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

Question 8：Task 3 透過`enum4linux`枚舉，發現有效帳戶名稱為 cactus

<p align="left">
  <img src="/rooms/images/11_13.png" width="600">
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

>> #### Task 6：枚舉 Telnet

>> #### Task 7：利用 Telnet

>> #### Task 8：瞭解 FTP

>> #### Task 9：枚舉 FTP

>> #### Task 11：利用 FTP

