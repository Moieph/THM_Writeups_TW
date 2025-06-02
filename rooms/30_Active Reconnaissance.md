# Active Reconnaissance

**🟥 主動偵察**

THM路徑：https://tryhackme.com/room/activerecon

---

>> #### Task 1：介紹

- Active Reconnaissance（主動偵查）

| 偵查方式     | 特性          | 是否連線目標  | 常見工具                                  |
| -------- | ----------- | ------- | ------------------------------------- |
| **被動偵查** | 觀察目標、分析開放資訊 | ❌ 不直接連線 | WHOIS、Shodan、Google Dorks 等           |
| **主動偵查** | 直接連線、測試目標回應 | ✅ 有連線紀錄 | ping、traceroute、telnet、nc、Web Browser |

>> #### Task 2：瀏覽器

🧠 Web 瀏覽器：被低估的偵查利器

- 📌 所有系統內建，隨手可得
- 📌 可偽裝成「正常使用者」進行探測，低風險、難被察覺
- 📌 結合 DevTools，變身「Recon 平台」

---

🔌 連線層級（Transport Layer）

| 協定       | 預設埠口    | 顯示方式                                                                  |
| -------- | ------- |-----------------------------------------------------------------------|
| HTTP     | TCP 80  | `http://example.com`（不顯示 :80）                                         |
| HTTPS    | TCP 443 | `https://example.com`（不顯示 :443）                                       |
| **自訂埠口** | 任意      | 如： `https://127.0.0.1:8834/`  <br>若該埠口上有對應服務（如 Nessus 在 8834），即可成功連上。 |

---

🛠 開發者工具（DevTools）使用重點

- 打開方式：
    - Windows：Ctrl + Shift + I
    - Mac： Alt / Opt + ⌘(Command) + I

- 可觀察內容包括：
    - **Network**：所有請求（含 API、XHR、Headers、Status）
    - **Cookies**：查看是否含憑證、Session Token
    - **JS**：找內嵌或載入的 JavaScript 程式碼
    - **Site** 結構：推敲網站目錄與路徑

---

🧩 推薦瀏覽器擴充功能（適用於紅隊 / 偵查）

| 工具名稱                                | 作用                         | 補充說明                     |
| ----------------------------------- | -------------------------- | ------------------------ |
| **FoxyProxy**                       | 快速切換代理伺服器（配合 Burp Suite）   | 設定多組 Proxy Profile，一鍵切換  |
| **User-Agent Switcher and Manager** | 偽裝不同設備或瀏覽器                 | 例如：偽裝成 iPhone Safari 使用者 |
| **Wappalyzer**                      | 偵測網站技術棧（如使用的 CMS、框架、JS 套件） | 類似 BuiltWith，但可即時顯示於瀏覽器  |

---

📌 實戰建議：
1. 進入目標網站 → 開啟 DevTools
2. 分析：
   - Network：有哪些重要 JS 請求？有 API？有備援路徑？
   - Cookies：有沒有 JWT、PHPSESSID 等 session 資訊
   - Console：是否有錯誤訊息洩漏敏感資訊
3. 裝上：
    - FoxyProxy → 配合 Burp 攔截請求
    - Wappalyzer → 看用什麼技術（WordPress? jQuery?）
    - User-Agent Switcher → 偽裝使用者身分觀察反應

---

依題旨點擊 `View site`

打開 網頁開發者工具，找到 `script.js`（通常為核心資料與邏輯）

<p align="left">
  <img src="/rooms/images/30_01.png" width="600">
</p>

得出問題總數

<p align="left">
  <img src="/rooms/images/30_02.png" width="600">
</p>

---

##### 🔐 答題：
1. Browse to the following website and ensure that you have opened your Developer Tools on AttackBox Firefox, or the browser on your computer. Using the Developer Tools, figure out the total number of questions.
   
   瀏覽該網站，確保您已在 AttackBox Firefox 或電腦上的瀏覽器上開啟了開發人員工具。使用 Developer Tools（開發人員工具），計算出問題的總數。
   
&nbsp;&nbsp;&nbsp;&nbsp; `8`

>> #### Task 3：Ping

🏓 Ping

- Ping 是一種檢查目標主機是否「上線」的方式，利用「ICMP Echo Request / Echo Reply」來確認能否連通。

---

📦 技術重點整理

| 項目         | 說明                                         |
| ---------- | ------------------------------------------ |
| **通訊協定**   | ICMP（Internet Control Message Protocol）    |
| **封包類型**   | Type 8（Echo Request）<br>Type 0（Echo Reply） |
| **預設行為**   | 會持續傳送直到手動停止（Linux）                         |
| **手動指定次數** | `-c`（Linux）或 `-n`（Windows）                 |

---
💻 操作範例

✅ 成功連線（目標機器開機且允許 ICMP）：<br>

`ping -c 5 MACHINE_IP`

輸出範例：

````
64 bytes from MACHINE_IP: icmp_seq=1 ttl=64 time=0.636 ms
...
5 packets transmitted, 5 received, 0% packet loss
````

☑️ 代表：機器在線、網路連通、ICMP 沒被阻擋

---

輸出範例：

````
From ATTACKBOX_IP icmp_seq=1 Destination Host Unreachable
...
5 packets transmitted, 0 received, +5 errors, 100% packet loss

````

可能原因包括：
- 🚫 目標主機沒開機 / OS 當掉
- 🔌 網路線沒插好 / 交換器故障
- 🔥 被防火牆擋住（Windows 預設會擋）
- ❗ 自己設備沒連網

---

使用 `ping` 的偵查策略

| 策略              | 說明                                                     |
| --------------- | ------------------------------------------------------ |
| 初步偵測            | 檢查哪些目標機器是「開機」且可被掃描的                                    |
| 偽裝偵測            | 有些目標會故意對 Ping 無回應（stealth mode）                        |
| Firewall Bypass | 改用 TCP ping (`hping3` / `nmap -sn -PS`) 避免被 ICMP 擋掉    |
| 分析 TTL & 回應時間 | TTL 可推測作業系統類型（例如 Linux vs Windows）<br>延遲時間可粗估地理距離或擁塞狀況 |

---

🧪 延伸工具

| 工具         | 功能                   | 補充                              |
| ---------- | -------------------- | ------------------------------- |
| `fping`    | 多目標 ping 掃描          | 適合大量 IP 掃描                      |
| `hping3`   | 建構任意 TCP/UDP/ICMP 封包 | 可偽裝成 TCP Ping、偽裝來源 IP           |
| `nmap -sn` | 掃描是否在線               | `nmap -sn 10.10.10.0/24` 檢查哪些存活 |
| `nping`    | Nmap 的 ping 工具，精密可控  | 支援自定 TTL、Delay、協定等              |

---

Question 1：`ping`參數說明
- `-s` (Linux) / `-l` (Windows) ➤ 自訂封包大小（以 bytes 為單位） 

Question 2： ICMP Header 結構

| 欄位              | 大小      | 說明                           |
| --------------- | ------- | ---------------------------- |
| Type            | 1 byte  | ICMP 類型（例如 Echo Request 是 8） |
| Code            | 1 byte  | 更進一步定義類型的代碼                  |
| Checksum        | 2 bytes | 錯誤檢查用的校驗值                    |
| Identifier      | 2 bytes | Echo Request 回應對應用           |
| Sequence Number | 2 bytes | 封包順序追蹤用                      |

Question 3：Windows 預設會擋 `ping`

Question 4：啟動虛擬機，在終端機輸入` ping -c 10 MACHINE_IP`，觀察得到幾個 `ping`回覆

<p align="left">
  <img src="/rooms/images/30_03.png" width="600">
</p>

---

##### 🔐 答題：
1. Which option would you use to set the size of the data carried by the ICMP echo request?
   
   您將使用哪個選項來設定 ICMP ECHO request 所攜帶的數據的大小？
   
&nbsp;&nbsp;&nbsp;&nbsp; `-s`

2. What is the size of the ICMP Header in bytes?
   
   ICMP Header的大小（以位元組為單位）是多少？
   
&nbsp;&nbsp;&nbsp;&nbsp; `8`

3. Does MS Windows Firewall block ping by default? (Y/N)
   
   MS Windows 防火牆預設是否阻止 ping？（是/否）
   
&nbsp;&nbsp;&nbsp;&nbsp; `Y`

4. Deploy the VM for this task and using the AttackBox terminal, issue the command `ping -c 10 MACHINE_IP`. How many ping replies did you get back?
   
   為此任務部署 VM，並使用 AttackBox 終端發出命令 `ping -c 10 MACHINE_IP`。您收到了多少個 ping 回復？
   
&nbsp;&nbsp;&nbsp;&nbsp; `10`

>> #### Task 4：Traceroute

🧭 `traceroute` 是什麼？

`traceroute` 用來追蹤封包從你電腦送到目標主機時經過哪些路由器（hop）

**目的：**
- 找出通訊過程中經過的路由器 IP
- 測量每一跳所花的時間（毫秒）
- 偵測網路延遲或路由問題

---

⚙️ `traceroute` 的原理

1. `traceroute` 並沒有辦法直接知道封包走哪條路徑，它是透過 **「欺騙」路由器** 來取得資訊。
2. 主要靠的是 IP 封包裡的 `TTL`（Time To Live）欄位。

🧩 TTL 是什麼？

- TTL 並不是真正的時間，而是封包最多可以通過幾個路由器
- 每經過一個路由器，TTL 減一
- 當 TTL = 0，路由器就會把封包丟棄，並回傳一個 ICMP 錯誤訊息

🚦 traceroute 怎麼做的？
- 第一次送一個 TTL = 1 的封包 → 第一個路由器會回 ICMP 錯誤。
- 第二次送 TTL = 2 的封包 → 第二個路由器會回 ICMP 錯誤。
- 以此類推，逐步逼出每一跳的 IP 和延遲時間。

---





>> #### Task 5：Telnet

>> #### Task 6：Netcat

>> #### Task 7：把它們放在一起