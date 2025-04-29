# 🔧 Tools

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

### `ping`
>測試目標是否存活（ICMP封包）

>Linux內建指令

`ping IP address or website URL`

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

### `msfvenom`
>產生各種 payload（後門程式、shellcode）

`msfvenom -p <payload> LHOST=<IP> LPORT=<port> -f <format>`

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
### `mkdir`
>建立新資料夾

>Linux內建指令

---
### `mount`
>掛載 NFS 的主要工具

>Linux內建指令

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