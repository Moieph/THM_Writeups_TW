# 🔧 Tools

### `nmap`
>掃描主機、開放的 port 和服務資訊

<details>
<summary><strong>參數說明</strong></summary>

| 指令 | 功能說明 |
|:----|:----|
| `nmap -sn <IP>` | 只探測主機是否存活（Ping 掃描，不掃 port） |
| `nmap <IP>` | 快速掃描目標主機，**預設掃描前 1000 個常見 port** |
| `nmap -p- <IP>` | 掃描 **所有 0-65535 個 port**（慢但全面） |
| `nmap -sV <IP> -p <Port>` | 掃描指定的 port，並嘗試探測服務版本 |
| `nmap -A -p <Port> -T4 <IP>` | 掃描指定 port，且啟用 **Aggressive mode**（OS 偵測、版本偵測、traceroute、script 掃描），T4 表示速度加快 |

</details>

---

### `enum4linux`
>枚舉（列舉）Windows SMB 資訊

`enum4linux -a <IP>`

<details>
<summary><strong>參數說明</strong></summary>

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
<summary><strong>參數說明</strong></summary>
- -U [使用者名稱]：指定用哪個帳號連線（如：-U Moieph）
- -p [埠號]：指定使用的埠號（預設是 445）

</details>

---

### `ping`
>測試目標是否存活（ICMP封包）

`ping IP address or website URL`

---

### `tcpdump`
>抓取網路封包（分析流量）

`sudo tcpdump -i <interface>`

<details>
<summary><strong>參數說明</strong></summary>

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

`nc -lvnp <port> (listen)`<br>
`nc <IP> <port> (connect)`

<details>
<summary><strong>參數說明</strong></summary>

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



