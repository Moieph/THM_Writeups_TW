# 🧾 Script


### `Active_Recon`
>主動偵查的簡易腳本

1. `traceroute` 追蹤從你電腦到目標 IP 的網路路徑（逐跳顯示）。可以用來判斷是否中間某個路由節點擋住或延遲。


2. 對目標 `ping` 四次，檢查主機是否活著、網路延遲情況、封包損失等。


3. 針對常見的 8 個埠口依序測試

| Port | 協定/服務 | 說明                 |
|------|------------|----------------------|
| 21   | FTP        | 檔案傳輸協定，常用於上傳/下載檔案 |
| 22   | SSH        | 安全遠端連線協定             |
| 23   | Telnet     | 遠端文字控制協定（不加密）       |
| 25   | SMTP       | 郵件傳送協定，常用於發信        |
| 53   | DNS        | 網域名稱系統，負責網域解析       |
| 80   | HTTP       | 超文字傳輸協定，網頁通訊的基礎    |
| 110  | POP3       | 郵件接收協定，下載郵件用        |
| 443  | HTTPS      | 加密的 HTTP，網站安全通訊       |


4. 用 `nc`（Netcat）測試對應的 port 是否開著。


| 參數                    | 功能說明     |
|-----------------------|----------|
| `-n`                  | 避免 DNS 查詢（直接使用 IP，加快速度） |
| `-v`                  | 顯示詳細輸出（Verbose mode） |
| `-z`                  | 不傳送任何資料，只掃描 port（Zero-I/O 模式） |
| `2>/dev/null`         | 把錯誤訊息導向 null，讓畫面輸出更乾淨 |

<details>
<summary>腳本程式碼</summary>

````
TARGET="IP"

echo "[*] 路由追蹤:"
traceroute $TARGET

echo "[*] PING 測試:"
ping -c 4 $TARGET

for port in 21 22 23 25 53 80 110 443; do
    echo "[*] 嘗試連接 $TARGET:$port"
    (echo "" | nc -nvz $TARGET $port) 2>/dev/null
done
````

</details>