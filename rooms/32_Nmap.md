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

| 連接埠號碼 | 對應服務    |
| ----- | ------- |
| 80    | HTTP    |
| 443   | HTTPS   |
| 139   | NetBIOS |
| 445   | SMB     |

🧠 每台設備有 65535 個 port，但常用 port 被標準定義，CTF 中可能有異常設定，需掃描所有可能埠

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



>> #### Task 3：Nmap 開關

>> #### Task 4：掃描類型概述

>> #### Task 5：TCP 連接掃描

>> #### Task 6：SYN 掃描

>> #### Task 7：UDP 掃描

>> #### Task 8：NULL、FIN 和 Xmas

>> #### Task 9：ICMP 網路掃描

>> #### Task 10：NES 腳本概述

>> #### Task 11：使用 NSE

>> #### Task 12：搜索 Scripts

>> #### Task 13：防火牆規避

>> #### Task 14：習題

>> #### Task 15：結論