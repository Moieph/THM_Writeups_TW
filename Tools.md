# 🔧 Tools

## Linux 系統內建

### `ping`
>測試目標是否存活（ICMP封包）

>Linux內建指令

`ping IP address or website URL`

---

### `nc`
>_netcat_：建立 TCP/UDP 連線、傳輸資料、反向 shell

>Linux內建指令 

`nc -lvnp <port> (listen)`<br>
`nc <IP> <port> (connect)`

<details>
<summary>參數說明</summary>

`nc -lvnp 4444`

| 參數 | 解釋 |
|:----|:----|
| `-l` | listen 模式 |
| `-v` | verbose（顯示更多細節） |
| `-n` | 不做 DNS 查詢 |
| `-p 4444` | 指定監聽 port（可自選） |


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

`chown [新擁有者] 檔案或資料夾`
`chown [新擁有者]:[新群組] 檔案或資料夾`

<details>
<summary>參數說明</summary>

| 指令                            | 說明                             |
|----------------------------------|----------------------------------|
| `chown root file.txt`           | 將擁有者改為 root                |
| `chown root:root file.txt`      | 改為 root 擁有、root 群組        |
| `chown -R user:group myfolder`  | 遞迴更改整個資料夾的擁有權       |


</details>

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

- `-U` [使用者名稱]：指定用哪個帳號連線（如：-U Moieph）
- `-p` [埠號]：指定使用的埠號（預設是 445）

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

### `msfconsole` 
> 啟動 Metasploit 主控台

---

