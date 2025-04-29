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

Question 3：用`showmoung`，列出靶機的NFS共享

- NFS共享名稱為：/home

<p align="left">
  <img src="/rooms/images/12_03.png" width="600">
</p>

Question 4：

>> #### Task 4：利用 NFS

>> #### Task 5：瞭解 SMTP

>> #### Task 6：枚舉 SMTP

>> #### Task 7：利用 SMTP

>> #### Task 8：瞭解 MySQL

>> #### Task 9：利用 MySQL 

>> #### Task 10：結論
