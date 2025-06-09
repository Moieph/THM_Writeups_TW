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
- Port Scanning 是攻擊的起點，也是防禦者的警訊
- 不掃 port，你就不知道能攻擊什麼
- `Nmap` 是進行初步偵察與列舉的首選工具

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

- 所有選項（switch）都要包含前面的 `-` 符號，如 `-sS`, `-p`, `-A` 等。

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
   
    您將如何啟動腳本類別「vuln」中的所有腳本？
   
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
- 使用者層面的掃描方式 **（非低層封包操作）**

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

NULL 掃描 `-sN`：

<p align="left">
  <img src="/rooms/images/32_12.png" width="600">
</p>

FIN 掃描 `-sF`：

<p align="left">
  <img src="/rooms/images/32_13.png" width="600">
</p>

Xmax 掃描 `-sX`：

<p align="left">
  <img src="/rooms/images/32_14.png" width="600">
</p>

---

🧠 判斷邏輯：

| 狀態                  | 回應                  | 
| ------------------- | ------------------- | 
| **Closed**          | 回傳 RST（Reset）封包     | 
| **Open / Filtered** | **無回應**（可能開啟或被防火牆擋） | 
| **Filtered**        | 回傳 ICMP unreachable |

---

🛡️ 防火牆繞過效果：

- 可 **繞過僅攔截 SYN 封包的防火牆**
- 但現代防火牆 / IDS 通常已能辨識此類封包類型 → 隱蔽性有限

---

⚠️ 實務限制：

- **Windows 系統 & Cisco 設備**：對所有不正常封包都回傳 RST
   - 導致所有 port 被誤判為 **關閉（Closed）**
- 無法明確確認 port 是開啟還是被擋 → 只能標為 `open|filtered`

---

✅ 實用指令範例：

````
sudo nmap -sN 10.10.10.10     # NULL 掃描
sudo nmap -sF 10.10.10.10     # FIN 掃描
sudo nmap -sX 10.10.10.10     # Xmas 掃描
````

---

🎯 小結：

| 優點                | 缺點                      |
| ----------------- | ----------------------- |
| 有機會繞過部分防火牆與舊型 IDS | 結果不明確，需交叉比對             |
| 偽裝連線特性、難被應用層紀錄    | Windows/Cisco 反應一致，容易誤判 |
| 可搭配其他掃描方式輔助分析     | 現代系統防禦效果有限              |

##### 🔐 答題：
1. Which of the three shown scan types uses the URG flag?
   
   顯示的三種掃描類型中，哪一種使用 URG 標誌？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Xmas`

2. Why are NULL, FIN and Xmas scans generally used?
   
   為什麼使用 NULL、FIN 和 Xmas 掃描？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Firewall Evasion`

3. Which common OS may respond to a NULL, FIN or Xmas scan with a RST for every port?

   哪種常見作業系統可以回應 NULL、FIN 或 Xmas 掃描，以 RST 回應每個端口狀態？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Microsoft Windows`

>> #### Task 9：ICMP 網路掃描

🌐 Ping Sweep 掃描筆記（Nmap -sn）

📌 任務背景（黑箱測試起點）：
- 初次接觸目標網路時，目標是 **繪製網路地圖**
- 揭示哪個 IP 是「**活的主機（Active Hosts）**」、哪些是沒反應的

---

🛠️ 使用指令：`-sn`

✅ 指令範例：

````
nmap -sn 192.168.0.1-254        # 使用範圍方式
nmap -sn 192.168.0.0/24         # 使用 CIDR 表示法
````

---

**CIDR**（Classless Inter-Domain Routing）

- **無類別網域間路由**


- 用來表示 IP 網段範圍 的一種方式，比老舊的 A/B/C 類網域更靈活、更有效率地管理 IP 地址。

````
IP位址/遮罩位數

192.168.1.0/24
````

- IP 範圍是從：192.168.1.0 到 192.168.1.255
- /24 代表「前 24 位是網路位址」，後面 8 位是主機位址（2⁸ = 256 組）

--- 

- 🎯 常見 **CIDR** 範例快速對照表：

| CIDR  | 可用 IP 數（主機） | 子網路遮罩           |
| ----- | ----------- | --------------- |
| `/8`  | 16,777,214  | 255.0.0.0       |
| `/16` | 65,534      | 255.255.0.0     |
| `/24` | 254         | 255.255.255.0   |
| `/30` | 2（用於點對點）    | 255.255.255.252 |
| `/32` | 1（單一主機）     | 255.255.255.255 |

---

🧠 `-sn` 的用途說明：

| 特性                       | 說明                                      |
| ------------------------ | --------------------------------------- |
| 不掃 port                  | 僅進行 **主機存活偵測（Ping Sweep）**，不會執行 port 掃描 |
| 發送 ICMP Echo Request     | 目標有回應 → 判定為「上線」                         |
| 發送 TCP SYN 到 port 443    | 輔助判斷是否有伺服器反應                            |
| 發送 TCP ACK/SYN 到 port 80 | 預設為 TCP ACK，**若非 root 執行則為 SYN**        |
| 本地網段用 ARP 探測（需 sudo）     | 若目標在同一區網，Nmap 會用 ARP 尋找主機（更準確）          |

---

⚠️ 注意事項：
- **部分主機會封鎖 ICMP 回應** → 可能導致誤判為離線
- 結果只能作為 **「初步基線」**，需搭配其他掃描補強

---

🧪 小技巧建議：
- 加上 `-v` 參數查看詳細過程：`nmap -sn -v 192.168.1.0/24`

---

##### 🔐 答題：
1. How would you perform a ping sweep on the `172.16.x.x` network (Netmask: `255.255.0.0`) using Nmap? (CIDR notation)
   
   如何使用 Nmap 在` 172.16.x.x` 網路（網路遮罩：`255.255.0.0`）上執行 ping 掃描？（CIDR 表示法）
   
&nbsp;&nbsp;&nbsp;&nbsp; `nmap -sn 172.16.0.0/16`

>> #### Task 10：NES 腳本概述

⚙️ Nmap Scripting Engine（NSE）筆記

- **Nmap 的腳本引擎模組**


- 腳本語言使用 **Lua**


- 功能包括：
  - 漏洞掃描
  - 認證繞過
  - 弱密碼爆破
  - 自動利用（Exploit）
  - 深度偵察（Discovery）

---

📁 常用 NSE 類別說明：

| 類別          | 用途簡介                           |
| ----------- | ------------------------------ |
| `safe`      | 安全、不影響目標，可放心使用（預設開啟）           |
| `intrusive` | **可能影響目標**，不建議在生產環境中隨意執行       |
| `vuln`      | 掃描目標是否有已知漏洞                    |
| `exploit`   | 嘗試利用漏洞進行攻擊                     |
| `auth`      | 嘗試繞過或驗證登入（如匿名登入 FTP）           |
| `brute`     | 嘗試對目標服務進行帳密暴力破解                |
| `discovery` | 發掘更多服務資訊（如查詢 SNMP、NetBIOS、服務版本等） |

---

🌐 完整腳本庫位置（官方）：

Nmap Script Library: https://nmap.org/nsedoc/

---

🧠 應用場景提示：
- **前期偵察**： `safe`, `discovery`, `auth`
- **滲透進攻**： `vuln`, `exploit`, `brute`, `intrusive`

---

##### 🔐 答題：
1. What language are NSE scripts written in?
   
   NSE 腳本是用什麼語言編寫的？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Lua`

2. Which category of scripts would be a very bad idea to run in a production environment?
   
   在生產環境中運行哪一類腳本是個非常糟糕的主意？
   
&nbsp;&nbsp;&nbsp;&nbsp; `intrusive`

>> #### Task 11：使用 NSE

⚙️ NSE 腳本使用方式整理

---
🧪 啟用整個類別的腳本：

`--script=<類別名稱>`

````
nmap --script=safe 10.10.10.10
nmap --script=intrusive,vuln 10.10.10.10

📌 僅會執行與「開放服務」相關的腳本
````

---
🧪執行單一腳本：

`--script=<腳本名稱>`

````
nmap --script=http-fileupload-exploiter -p 80 10.10.10.10
````

---

🧪執行多個腳本：

`--script=script1,script2`

````
nmap --script=smb-enum-users,smb-enum-shares -p 445 10.10.10.10
````

---

🎯 指定腳本參數（使用 `--script-args`）

✅ 範例（上傳 Web Shell）：

````
nmap -p 80 \
--script=http-put \
--script-args=http-put.url='/dav/shell.php',http-put.file='./shell.php' \
10.10.10.10
````

| 語法格式                   | 說明         |
| ---------------------- | ---------- |
| `script-name.argument` | 針對特定腳本傳入參數 |
| 逗號 `,` 分隔多個參數          | 多參數設定時不可遺漏 |

---

📘 查看指定腳本的說明文件：

`nmap --script-help <script-name>`

`nmap --script-help http-put`

---

🌐 官方 NSE 腳本文件（含參數與用途）：

Nmap Script Library: https://nmap.org/nsedoc/

---

Question 1：於終端機輸入 `nmap --script-help ftp-anon.nse`

<p align="left">
  <img src="/rooms/images/32_15.png" width="600">
</p>

依圖片提示進入該腳本的網址介紹：

https://nmap.org/nsedoc/scripts/ftp-anon.html

<p align="left">
  <img src="/rooms/images/32_16.png" width="600">
</p>


##### 🔐 答題：
1. What optional argument can the ftp-anon.nse script take?
   
   `ftp-anon.nse` 腳本可以採用什麼可選參數？
   
&nbsp;&nbsp;&nbsp;&nbsp; `maxlist`

>> #### Task 12：搜索 Scripts

🔍 如何查找 Nmap 腳本（NSE Scripts）

✅ **方式 1：官方網站**
- 網址：https://nmap.org/nsedoc/
- 提供完整腳本清單、分類、參數範例

✅ 方式 2：本地端路徑
- NSE 腳本預設儲存於：`/usr/local/share/nmap/scripts/`

---

📂 查找腳本方法：

📘 **方法 1：**`grep script.db`

`grep "ftp" /usr/local/share/nmap/scripts/script.db`

- `script.db` 不是資料庫，而是 Nmap 的腳本索引表（純文字格式）
- 可查關鍵字、類別（如：safe、vuln 等）


<p align="left">
  <img src="/rooms/images/32_17.png" width="600">
</p>

📘 **方法 2：**`ls` 直接模糊搜尋

`ls -l /usr/local/share/nmap/scripts/*ftp*`


<p align="left">
  <img src="/rooms/images/32_18.png" width="600">
</p>

---

⚙️ 安裝或新增腳本：

````
sudo wget -O /usr/local/share/nmap/scripts/<script-name>.nse \
https://svn.nmap.org/nmap/scripts/<script-name>.nse

# ✅ 下載後務必執行更新索引指令：

sudo nmap --script-updatedb
````

如本地缺少腳本：

````
sudo apt update && sudo apt install nmap 

# ✅ 下載後務必執行更新索引指令：

sudo nmap --script-updatedb
````

🧠 自製 NSE 腳本也能加入：

- 編寫 Lua 檔案（副檔名 `.nse`）放入 `/usr/local/share/nmap/scripts/`
- 同樣使用 `--script-updatedb` 更新索引

---

🧪 快速檢查 NSE 腳本分類範例：

````
grep "intrusive" /usr/local/share/nmap/scripts/script.db
grep "vuln" /usr/local/share/nmap/scripts/script.db
````

<p align="left">
  <img src="/rooms/images/32_19.png" width="600">
</p>

---

Question 1：根據題目，以 `os` 作為判斷條件，於終端機輸入 

`grep "smb" /usr/local/share/nmap/scripts/script.db` 

找尋與判斷條件相符的腳本

<p align="left">
  <img src="/rooms/images/32_20.png" width="600">
</p>

Question 2：根據題目，於終端機輸入

`cat /usr/local/share/nmap/scripts/smb-os-discovery.nse`

<p align="left">
  <img src="/rooms/images/32_21.png" width="600">
</p>

閱讀該腳本文件，於搜尋欄（`Ctrl+F`）尋找 dependency

<p align="left">
  <img src="/rooms/images/32_22.png" width="600">
</p>


##### 🔐 答題：
1. What is the filename of the script which determines the underlying OS of the SMB server?
   
   確定 SMB 伺服器底層作業系統腳本的檔名是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `smb-os-discovery.nse`

2. Read through this script. What does it depend on?
   
   透過閱讀腳本。判斷它依賴於什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `smb-brute`

>> #### Task 13：防火牆規避

📛 問題：目標主機**封鎖 ICMP（如 Windows 預設）**
- **導致 Nmap 預設無法偵測主機是否存活**
- 掃描會被略過，主機會被誤判為「關機」

---

✅ 解法：使用 `-Pn`

`nmap -Pn <目標IP>`

| 參數    | 說明                                |
| ----- | --------------------------------- |
| `-Pn` | 告訴 Nmap **不要先 ping 掃主機**，直接掃 port |
| 效果    | 可繞過封鎖 ICMP 的防火牆規則                 |
| 缺點    | 若主機真的關機，仍會掃很久（誤以為還活著）             |

---

📡 本地區網環境額外提示：
- 在本地網段中，**Nmap 可使用 ARP 尋找主機**，不受 ICMP 限制

---

🧨 進階防火牆/IDS 規避技巧：

| 參數                      | 功能說明                                         |
|-------------------------| -------------------------------------------- |
| `-f`                    | **封包碎片化**，切小封包降低被偵測機率                        |
| `--mtu <數值>`            | 指定 MTU 封包大小（需為 8 的倍數）                        |
| `--scan-delay <time>ms` | 設定封包之間的延遲，可防止時間頻率觸發防火牆                       |
| `--badsum`              | 發送帶有錯誤 checksum 的封包，用來**探測防火牆是否存在**（正常主機不會回應） |
| `--data-length <數值>`    | 在數據包末尾附加任意長度的隨機數據|

---

🧪 範例：繞過防火牆掃描

`sudo nmap -sS -Pn -f 10.10.10.10`

或加上延遲與 MTU 控制：

`sudo nmap -sS -Pn --scan-delay 200ms --mtu 32 10.10.10.10`

---

##### 🔐 答題：
1. Which simple (and frequently relied upon) protocol is often blocked, requiring the use of the `-Pn` switch?
   
   哪種簡單（且經常依賴）協議經常被阻止，需要使用 `-Pn` 開關？
   
&nbsp;&nbsp;&nbsp;&nbsp; `ICMP`

2. [Research] Which Nmap switch allows you to append an arbitrary length of random data to the end of packets?
   
   [研究] 哪個 Nmap 開關允許您在數據包末尾附加任意長度的隨機數據？
   
&nbsp;&nbsp;&nbsp;&nbsp; `--data-length`

>> #### Task 14：實作

Question 1：開啟虛擬機，輸入 `ping <IP>`

目標機未回應 `ping` 請求

<p align="left">
  <img src="/rooms/images/32_23.png" width="600">
</p>

Question 2、3：輸入 `nmap -sX -vv -p 1-999 <IP>` 進行掃描

確認端口狀態

<p align="left">
  <img src="/rooms/images/32_24.png" width="600">
</p>

Question 4：輸入 `nmap -sS -vv -p 1-5000 <IP>` 進行掃描

確認端口狀態

<p align="left">
  <img src="/rooms/images/32_25.png" width="600">
</p>

Question 5：輸入 `nmap --script=ftp-anon -p 21 <IP>` 進行掃描

確認 FTP 可否匿名登入

<p align="left">
  <img src="/rooms/images/32_26.png" width="600">
</p>

##### 🔐 答題：
1. Does the target ip respond to ICMP echo (`ping`) requests (Y/N)?
   
   目標 IP 是否回應 ICMP 回顯 （`ping`） 請求 （Y/N）？
   
&nbsp;&nbsp;&nbsp;&nbsp; `N`

2. Perform an `Xmas scan` on the first 999 ports of the target -- how many ports are shown to be open or filtered?
   
   對目標的前 999 個端口執行 `Xmas 掃描` -- 顯示有多少個端口處於打開狀態或已篩選狀態？
   
&nbsp;&nbsp;&nbsp;&nbsp; `999`

3. There is a reason given for this -- what is it?
   
   這是有原因的 -- 它是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `No Response`

4. Perform a `TCP SYN scan` on the first 5000 ports of the target -- how many ports are shown to be open?
   
   在目標的前 5000 個埠上執行 `TCP SYN 掃描` -- 顯示有多少個端口處於打開狀態？
   
&nbsp;&nbsp;&nbsp;&nbsp; `No Response`

5. Deploy the `ftp-anon` script against the box. Can Nmap login successfully to the FTP server on port 21? (Y/N)
   
   針對機器部署 `ftp-anon` 腳本。Nmap 能否在埠 21 上成功登錄 FTP 伺服器？（是/否）
   
&nbsp;&nbsp;&nbsp;&nbsp; `Y`

>> #### Task 15：結論

✅ 小結重點回顧：

- 🔍 各類掃描方式（`-sS`, `-sT`, `-sU`, `-sN`, `-sF`, `-sX`）


- 📡 `Ping` 掃描與 `-sn` 的使用方式


- 🔐 防火牆繞過技巧：`-Pn`, `-f`, `--scan-delay`, `--badsum`


- ⚙️ NSE 腳本系統（如何執行、查找、設定參數）


- 🧠 腳本儲存位置與手動安裝方式
`/usr/local/share/nmap/scripts/` + `--script-updatedb`

---

🔗 官方腳本文件庫：
https://nmap.org/nsedoc/

📖 Nmap 使用手冊與各種進階技巧：
https://nmap.org/book/