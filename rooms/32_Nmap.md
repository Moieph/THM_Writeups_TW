# Nmap

**🟥 Nmap**

THM路徑：https://tryhackme.com/room/furthernmap

---

>> #### Task 1：部署

>> #### Task 2：介紹

🚩 Port Scanning 與 Nmap 基礎概念筆記


- 駭客的力量來自資訊。瞭解目標越多，可用攻擊面就越多。
- 滲透前最重要的第一步：<br>列舉（Enumeration）→ 掃描（Port Scanning）

---

🧱 為何要做 Port Scanning？

- 目的是畫出目標的網路服務地圖
- 查出哪些「服務」正運作中（如：Web、SMB、FTP、DNS…）
- 每個服務透過不同的 「連接埠（Port）」 對外開放

---

🔢 常見 Port 對應服務：

| 連接埠號碼 | 對應服務   |
|-------|--------|
| 80    | HTTP   |
| 443   | HTTPS  |
| 139   | NetBIOS |
| 22    | SSH    |
| 25    | SMTP |

🧠 每台設備有 **65535** 個 port，但常用 port 被標準定義（**1024** 個），CTF 中可能有異常設定，需掃描所有可能端口

<p align="left">
  <img src="/rooms/images/32_01.png" width="600">
</p>

---

🔧 舉例說明：

- 你開啟 3 個網頁 → 電腦會開不同的「**高位數隨機 port**」（如 49534、49535）對伺服器的 443 port 發出請求


- 每次連線都由「你電腦的隨機 port」→「目標伺服器的指定 port」

---

🚀 工具選擇：`Nmap`

✅ 為何選 `Nmap`？

- 功能強大、業界標準
- 支援多種掃描模式（TCP、SYN、UDP…）
- 可判別 port 狀態：open / closed / filtered
- NSE（Nmap Script Engine） 可進一步執行漏洞掃描或自動攻擊

---

🔑 結論：
Port Scanning 是攻擊的起點，也是防禦者的警訊
不掃 port，你就不知道能攻擊什麼
`Nmap` 是進行初步偵察與列舉的首選工具

---

##### 🔐 答題：
1. What networking constructs are used to direct traffic to the right application on a server?
   
   使用哪些網路結構將流量定向到伺服器上的正確應用程式？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Ports`

2. How many of these are available on any network-enabled computer?
   
   在任何支援網路的計算機上，有多少個端口可用？
   
&nbsp;&nbsp;&nbsp;&nbsp; `65535`

3. How many of these are considered "well-known"? (These are the "standard" numbers mentioned in the task)
   
   其中有多少被認為是「知名」的？（這些是任務中提到的“標準”數位）
   
&nbsp;&nbsp;&nbsp;&nbsp; `1024`


>> #### Task 3：Nmap 開關

🛠️ Nmap 使用方式總整理（基礎）

✅ 工具特性：
- 可在 **Linux** 與 **Windows** 上執行
- Kali Linux 與 TryHackMe AttackBox 預設已安裝
- 執行方式：使用終端機輸入 `nmap` 搭配參數（switch）

---

🔍 基本指令：

| 功能     | 指令範例       |
| ------ | ---------- |
| 檢視說明   | `nmap -h`  |
| 檢視說明文件 | `man nmap` |

- 所有選項（switch）都要包含前面的 - 符號，如 `-sS`, `-p`, `-A` 等。

---

🧠 小提醒：
- switch 就是你加在 `nmap` 後的功能開關（參數）
- 例如：`nmap -sS 10.10.10.10` → 代表使用 SYN 掃描
- 你可以透過 `nmap -h` 查到所有參數與用途簡介
- 想要更深入的說明，使用 `man nmap` 查閱說明文件

---

Question 1 - 16：於終端機輸入 `nmap -h` 查詢指令

<p align="left">
  <img src="/rooms/images/32_02.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/32_03.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/32_04.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/32_05.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/32_06.png" width="600">
</p>

輸入 `man nmap`，查詢該指令

<p align="left">
  <img src="/rooms/images/32_07.png" width="600">
</p>

##### 🔐 答題：
1. What is the first switch listed in the help menu for a 'Syn Scan' (more on this later!)?
   
   “Syn Scan”的説明功能表中列出的第一個開關是什麼（稍後會詳細介紹！
   
&nbsp;&nbsp;&nbsp;&nbsp; `-sS`

2. Which switch would you use for a "UDP scan"?
   
   您將使用哪個開關進行「UDP 掃描」？
   
&nbsp;&nbsp;&nbsp;&nbsp; `-sU`

3. If you wanted to detect which operating system the target is running on, which switch would you use?
   
   如果要檢測目標在哪個作業系統上運行，您將使用哪個開關？
   
&nbsp;&nbsp;&nbsp;&nbsp; `-O`

4. Nmap provides a switch to detect the version of the services running on the target. What is this switch?
   
   Nmap 提供了一個開關來檢測目標上運行的服務版本。這個開關是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `-sV`

5. The default output provided by nmap often does not provide enough information for a pentester. How would you increase the verbosity?
   
   Nmap 提供的預設輸出通常不能為滲透測試人員提供足夠的資訊。您將如何增加詳細程度？
   
&nbsp;&nbsp;&nbsp;&nbsp; `-v`

6. Verbosity level one is good, but verbosity level two is better! How would you set the verbosity level to two?
   
   詳細級別 1 很好，但詳細級別 2 更好！如何將詳細級別設置為 2？
   
&nbsp;&nbsp;&nbsp;&nbsp; `-vv`

7. What switch would you use to save the nmap results in three major formats?
   
   你會用什麼開關把 Nmap 結果保存成三種主要格式呢？
   
&nbsp;&nbsp;&nbsp;&nbsp; `-oA`

8. What switch would you use to save the nmap results in a "normal" format?
   
   你會用什麼開關把 Nmap 結果保存成 「正常」 格式？
   
&nbsp;&nbsp;&nbsp;&nbsp; `-oN`

9. A very useful output format: how would you save results in a "grepable" format?
   
   一個非常有用的輸出格式：如何將結果保存為 「grepable」 格式？
   
&nbsp;&nbsp;&nbsp;&nbsp; `-oG`

10. Sometimes the results we're getting just aren't enough. If we don't care about how loud we are, we can enable "aggressive" mode. This is a shorthand switch that activates service detection, operating system detection, a traceroute and common script scanning.
   
    有時我們得到的結果還不夠。如果我們不在乎我們的聲音有多大，我們可以啟用 「激進」 模式。這是一個速記開關，用於啟動服務檢測、作系統檢測、traceroute 和常用腳本掃描。
   
&nbsp;&nbsp;&nbsp;&nbsp; `-A`

11. How would you set the timing template to level 5?
   
    如何將 timing template 設置為 level 5？
   
&nbsp;&nbsp;&nbsp;&nbsp; `-T5`

12. How would you tell nmap to only scan port 80?
   
    你會如何告訴 nmap 只掃描端口 80？
   
&nbsp;&nbsp;&nbsp;&nbsp; `-p 80`

13. How would you tell nmap to scan ports 1000-1500?
   
    你會如何告訴 nmap 掃描端口 1000-1500？
   
&nbsp;&nbsp;&nbsp;&nbsp; `-p 1000-1500`

14. How would you tell nmap to scan all ports?
   
    你會如何告訴 nmap 掃描所有端口？
   
&nbsp;&nbsp;&nbsp;&nbsp; `-p-`

15. How would you activate a script from the nmap scripting library (lots more on this later!)?
   
    您將如何從 nmap 腳本庫中啟動腳本（稍後會詳細介紹！
   
&nbsp;&nbsp;&nbsp;&nbsp; `--script`

16. How would you activate all of the scripts in the "vuln" category?
   
   您將如何啟動腳本「vuln」 類別中的所有文稿？
   
&nbsp;&nbsp;&nbsp;&nbsp; `--script=vuln`

>> #### Task 4：掃描類型概述

🚀 Nmap 常見的 Port Scanning 類型：

| 掃描類型        | 參數    | 說明                      |
| ----------- | ----- | ----------------------- |
| TCP Connect | `-sT` | 完整 TCP 三次握手，最穩定但最容易被偵測  |
| SYN 掃描      | `-sS` | 半開式掃描（Half-open），常用、較隱蔽 |
| UDP 掃描      | `-sU` | 掃描 UDP 服務，較慢、結果易模糊      |

---

🧪 其他進階/少見掃描：

| 掃描類型        | 參數    | 特性說明                 |
| ----------- | ----- | -------------------- |
| TCP Null 掃描 | `-sN` | 不設定任何 TCP flag，偽裝用   |
| TCP FIN 掃描  | `-sF` | 僅設 FIN flag，規避部分防火牆  |
| TCP Xmas 掃描 | `-sX` | 設置 FIN、PSH、URG，極度偽裝型 |

---

🛰️ 額外：ICMP 掃描（Ping 掃描）

- 用於偵測目標是否存活（而非特定 port）
- 參數：`-sn`（原為 `-sP`）

---

🧠 建議搭配使用範例：

````
# 半開式 TCP + UDP 掃描
sudo nmap -sS -sU -p- -vv 10.10.10.10

# FIN 掃描
sudo nmap -sF 10.10.10.10

# Xmas 掃描
sudo nmap -sX 10.10.10.10
````


>> #### Task 5：TCP 連接掃描

🔍 TCP Connect 掃描 (`-sT`) 概念整理

- **三次握手（TCP Three-Way Handshake）**

| 階段  | 動作                   |
| --- | -------------------- |
| 1️⃣ | 攻擊端送出 **SYN** 封包     |
| 2️⃣ | 伺服器回應 **SYN/ACK** 封包 |
| 3️⃣ | 攻擊端回覆 **ACK**，完成連線建立 |

<p align="left">
  <img src="/rooms/images/32_08.png" width="300">
</p>


<p align="left">
  <img src="/rooms/images/32_09.png" width="600">
</p>

---

💡 `-sT` 是什麼？

- 全稱：**TCP Connect 掃描**
- 做法：模擬真實連線，對每個 port 執行 完整三次握手
- 使用者層面的掃描方式**（非低層封包操作）**

---

📈 判斷結果依據：

| 回應類型      | 代表什麼                                 |
| --------- |--------------------------------------|
| `SYN/ACK` | Port 為 **開啟（Open）**                  |
| `RST`     | Port 為 **關閉（Closed）**  由 RFC 9293 定義 |
| 無回應（被丟棄）  | Port 為 **被過濾（Filtered）**             |

-  可能被**防火牆干擾**，導致誤判

---


🔧 實際範例：`nmap -sT 10.10.10.10`

---


🧠 小結：
- `-sT` 是最直接、最穩定的掃描方式
- 不需 root 權限即可執行（因為是使用系統 API 發起 TCP 連線）
- 缺點是容易被防火牆與 IDS 偵測
- 若需更隱密，建議改用 `-sS`（SYN 掃描）

---

##### 🔐 答題：
1. Which RFC defines the appropriate behaviour for the TCP protocol?
   
   哪個 RFC 定義了 TCP 協定的適當行為？
   
&nbsp;&nbsp;&nbsp;&nbsp; `RFC 9293`

2. If a port is closed, which flag should the server send back to indicate this?
   
   如果端口已關閉，伺服器應發送回哪個標誌來指示這一點？
   
&nbsp;&nbsp;&nbsp;&nbsp; `RST`

>> #### Task 6：SYN 掃描

🧪 SYN 掃描（-sS）簡介

- **Half-open scan（半開掃描）**
- **Stealth scan（隱匿掃描）**

---

🔄 掃描流程（針對開啟的 port）：

| 步驟  | 說明                                   |
| --- | ------------------------------------ |
| 1️⃣ | Nmap 發送 **SYN 封包**                   |
| 2️⃣ | 目標回應 **SYN/ACK**                     |
| 3️⃣ | Nmap 回應 **RST 封包**（重設）終止連線，**不完成握手** |

<p align="left">
  <img src="/rooms/images/32_10.png" width="300">
</p>

<p align="left">
  <img src="/rooms/images/32_11.png" width="600">
</p>

---

✅ 優點：

| 優點           | 說明                                 |
| ------------ | ---------------------------------- |
| 更隱密（Stealth） | 不完成三次握手 → 較難被舊型 IDS 偵測             |
| 應用層通常不會記錄    | 因為連線未完全建立，大多應用層不會記錄這類請求            |
| 掃描速度快        | 無需真正建立連線 → 節省時間                    |
| 預設模式（需 sudo） | 使用 `sudo` 執行時，Nmap **預設採用 -sS 掃描** |

---

⚠️ 缺點：

| 缺點            | 說明                                       |
| ------------- | ---------------------------------------- |
| 需 **root 權限** | 須用 `sudo` 或設置能力（CAP\_NET\_RAW 等）才能發送原始封包 |
| 部分不穩定服務可能會崩潰  | 生產環境中需小心使用，避免服務異常                        |

---

🔧 實際範例：`sudo nmap -sS 10.10.10.10`

---

🔄 SYN 與 TCP Connect 掃描對比總結：

| 比較項目    | `-sT`（TCP Connect） | `-sS`（SYN Scan） |
| ------- | ------------------ | --------------- |
| 權限需求    | 不需 root            | 需 root / sudo   |
| 偵測隱蔽性   | 易被偵測               | 較隱蔽（舊式 IDS）     |
| 連線狀態    | 完整三次握手             | 半開、主動中斷         |
| 掃描速度    | 較慢                 | 較快              |
| 預設應用層紀錄 | 常常會記錄              | 通常不會記錄          |

---

##### 🔐 答題：
1. There are two other names for a SYN scan, what are they?
   
   SYN 掃描還有另外兩個名稱，它們是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Half-Open, Stealth`

2. Can Nmap use a SYN scan without Sudo permissions (Y/N)?
   
   Nmap 可以在沒有 Sudo 許可權 （Y/N） 的情況下使用 SYN 掃描嗎？
   
&nbsp;&nbsp;&nbsp;&nbsp; `N`

>> #### Task 7：UDP 掃描

📡 UDP 掃描（-sU）筆記

- **無連線（stateless**）：無三次握手，直接送出封包
- 適合速度需求高的應用（如：影音串流）
- 不回應 ≠ 拒絕，導致掃描結果較難判斷

---

✅ Nmap UDP 掃描指令：

`nmap -sU <目標IP>`

---

🧠 結果解讀邏輯：

| 情境                           | Nmap 判定                 |
| ---------------------------- |-------------------------|
| **無回應（常見）**                  | `open`、`filtered`（無法確定） |
| **收到 UDP 回應（少見）**            | `open`（已確認）             |  
| **收到 ICMP Port Unreachable** | `closed`（明確關閉）          |  

- Nmap 會對無回應的 **port** 再送一次確認封包
- 大多數服務不會對空白 UDP 封包有反應 → 判斷困難

---

🐢 缺點：非常慢

- 掃描前 1000 個 UDP port 可耗時 20 分鐘以上
- 建議只掃常見 port，加快速度

---

⚡ 加速建議：

`nmap -sU --top-ports 20 <目標IP>`

- 掃描**最常見的 20 個 UDP port**
- 節省時間，大幅提高效率

---

📘 補充說明：

- Nmap 會根據 port 編號發送 **「協定專屬封包」** 來提高準確度
   - 例如：對 DNS port (53) 送 DNS 封包
- 其餘 port 則多使用**空封包（empty UDP）**

---

##### 🔐 答題：
1. If a UDP port doesn't respond to an Nmap scan, what will it be marked as?
   
   如果 UDP 連接埠沒有回應 Nmap 掃描，它將被標記為什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `open|filtered`

2. When a UDP port is closed, by convention the target should send back a "port unreachable" message. Which protocol would it use to do so?
   
   按照慣例，當 UDP 埠關閉時，目標應發回 “port unreachable” 消息。它將使用哪種協議來執行此作？
   
&nbsp;&nbsp;&nbsp;&nbsp; `ICMP`

>> #### Task 8：NULL、FIN 和 Xmas

🎯 NULL / FIN / Xmas Scan 筆記總整理

- 比 **SYN 掃描還更隱密**的掃描方式
- **繞過防火牆與 IDS 偵測**

---

🔍 各類掃描方式對比：

| 掃描類型    | Nmap 參數 | TCP Flag 特性             | 別名/備註            |
| ------- | ------- | ----------------------- | ---------------- |
| NULL 掃描 | `-sN`   | **無任何 TCP flag**（空封包）   | 極度簡潔             |
| FIN 掃描  | `-sF`   | **僅設定 FIN**（正常關閉連線使用）   | 優雅假裝中斷連線         |
| Xmas 掃描 | `-sX`   | 設定 **PSH、URG、FIN**，像聖誕樹 | 封包像聖誕燈閃爍，得名 Xmas |

---

🧠 判斷邏輯：

| 狀態                  | 回應                  | 
| ------------------- | ------------------- | 
| **Closed**          | 回傳 RST（Reset）封包     | 
| **Open / Filtered** | **無回應**（可能開啟或被防火牆擋） | 
| **Filtered**        | 回傳 ICMP unreachable |


>> #### Task 9：ICMP 網路掃描

>> #### Task 10：NES 腳本概述

>> #### Task 11：使用 NSE

>> #### Task 12：搜索 Scripts

>> #### Task 13：防火牆規避

>> #### Task 14：習題

>> #### Task 15：結論