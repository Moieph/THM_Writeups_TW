# Security Principles  
**⚖️ 安全原則**

THM路徑：https://tryhackme.com/room/securityprinciples 

>> #### Task 1：介紹

>> #### Task 2：CIA 資安三要素

<p align="left">
  <img src="/rooms/images/05_01.png" width="600">
</p>

1. **機密性（Confidentiality）：**<br>確保只有授權的使用者或接收者可以存取資料，防止未授權的存取與洩漏。
2. **完整性（Integrity）：**<br>確保資料未被未經授權地更動，且當資料遭到變更時，我們能夠偵測並追蹤這些變化。
3. **可用性（Availability）：**<br>確保系統或服務在使用者需要時能正常運作，不因攻擊（如 DDoS）或故障而中斷。

<hr>


<details>
<summary><strong>1️⃣ 真實性（Authenticity）</strong></summary>

- <strong>定義</strong>：Authentic 意指「非偽造、非虛假」。
- <strong>說明</strong>：真實性是指資料、文件或檔案確實來自聲稱的來源，而非被偽造或中途竄改。
- ✅ 目的是確保來源的可信度與內容的正當性。

</details>

<details>
<summary><strong>2️⃣ 不可否認性（Nonrepudiation）</strong></summary>

- <strong>定義：</strong>Repudiate 表示「否認、拒絕承認」。 Nonrepudiation 則是防止這種否認發生。
- <strong>說明：</strong>不可否認性是指發送者無法否認其曾經傳送過某個文件或資料，確保事後責任歸屬清晰。
- 🔐 對於線上交易、病患診斷記錄、銀行轉帳等場景，這項特性非常關鍵。

</details>

真實性與不可否認性也是資安設計中不可忽略的重要層面，確保每一筆資料都 **「可信、可驗證、可追溯」**。

---

<details>
<summary><strong>3️⃣ 效用性（Utility）</strong></summary>

- <strong>定義：</strong>效用性是指資訊的實用價值是否仍然存在。
- <strong>說明：</strong>使資訊仍在、也可存取，但如果無法理解或使用，則等同於失去效用。
- <strong>🔐 如：</strong>使用者遺失了解密金鑰，雖然筆電與硬碟仍在，也無法使用裡面的加密資料，該資訊即喪失效用（utility lost）。

</details>

<details>
<summary><strong>4️⃣ 擁有權（Possession）</strong></summary>

- <strong>定義：</strong>擁有權是指資訊的實體控制權是否仍掌握在合法擁有者手中。
- <strong>說明：</strong>即便資料未被刪除或竄改，只要落入未授權者手中，也等同於失去對該資料的控制。
- <strong>🧨 例如：</strong>
  - 攻擊者偷走備份硬碟 → 我們失去資訊的實體控制。
  - 勒索軟體加密資料 → 雖資料仍在，我們卻無法使用，亦屬「擁有權喪失」。

</details>

---

以下題目為隨機出現：

Q1：在警察檢查站，警察懷疑車輛登記文件為假。該員警認為缺少哪項安全功能？
<p align="left">
  <img src="/rooms/images/05_02.png" width="600">
</p>

Q2：一家飯店強調其 WiFi 網路每週 7 天、每天 24 小時均可連線。飯店重視哪個安全功能？
<p align="left">
  <img src="/rooms/images/05_03.png" width="600">
</p>

Q3：你去兌現一張支票，銀行出納員讓你等了五分鐘，為了確認支票簽發人的簽名。銀行櫃員正在檢查哪些安全功能？
<p align="left">
  <img src="/rooms/images/05_05.png" width="600">
</p>

Q4：指揮官強調，在任務進行期間，軍隊不應該向任何人透露他們的位置。指揮官希望擁有哪種安全功能？ 
<p align="left">
  <img src="/rooms/images/05_06.png" width="600">
</p>

Q5：兩家公司正在就某項協議進行談判；然而，他們希望對協議的細節保密。他們強調哪個安全功能？
<p align="left">
  <img src="/rooms/images/05_04.png" width="600">
</p>

獲得 Flag 🎉🎉
<p align="left">
  <img src="/rooms/images/05_07.png" width="600">
</p>

##### 🔐 答題：
1. Click on "View Site" and answer the five questions. What is the flag that you obtained at the end?
   
   查看網站並回答五個問題。你最後得到的旗幟是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{CIA_TRIAD}`

>> #### Task 3：DAD 攻擊三要素

<p align="left">
  <img src="/rooms/images/05_08.png" width="600">
</p>

1. **Disclosure（洩漏）** 是「機密性（Confidentiality）」的對立面。換句話說，機密資料遭到洩漏，就是對機密性的攻擊。
2. **Alteration（竄改）** 是「完整性（Integrity）」的對立面。如：支票的完整性極重要，一旦被篡改就無法信任
3. **Destruction / Denial（摧毀／拒絕）** 是「可用性（Availability）」的對立面。當系統或資料遭摧毀，或無法存取，即是對可用性的打擊。

##### 🔐 答題：
1. The attacker managed to gain access to customer records and dumped them online. What is this attack?
   
    攻擊者設法訪問了客戶記錄並將其轉儲到網上。這種攻擊是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Disclosure`

1. A group of attackers were able to locate both the main and the backup power supply systems and switch them off. As a result, the whole network was shut down. What is this attack?
   
    攻擊者找到主電源和備用電源系統並將其關閉。結果，整個網路都關閉了。這種攻擊是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Destruction/Denial`


>> #### Task 4：安全模型（Security Model）

<details>
<summary><strong>Bell-LaPadula 模型</strong> 「不可上讀，不可下寫」</summary>
<i>重點在「機密性 Confidentiality」</i>

- 模型目的：

    此模型的目標是透過「存取控制規則」來防止未授權使用者存取敏感資訊，確保機密性不被破壞。

1. 簡單安全性原則（Simple Security Property）：<br>
**又稱：**「不可向上讀」（No Read Up, NRU）<br>
**規則：** 低安全等級的主體（Subject）不能讀取高安全等級的物件（Object）。<br>
**目的：** 防止機密資料被低權限者讀取。

2. 星號安全性原則（Star Security Property）<br>
**又稱：**「不可向下寫」（No Write Down, NWD）<br>
**規則：** 高安全等級的主體不能寫入到低安全等級的物件。<br>
**目的：** 避免機密資訊洩露給低權限者。

任意性安全原則（Discretionary Security Property）

使用存取矩陣（Access Matrix）來控制誰能對哪些物件執行哪些操作。




</details>






設備識別：<br>
IP 位址（可更改） MAC 位址（不可更改）

為了能在網路中通訊，設備必須能被辨識，就像人有名字與指紋一樣。

<details>
<summary> IP （Internet Protocol）位址</summary>
&nbsp;
<p align="left">
  <img src="/rooms/images/04_01.png" width="600">
</p>

1. 類似「名字」，可更改
2. 每台設備在網路中都有一組 IP 位址 <br>
- 分為：
  - 私人 IP：在內部網路中使用，如 192.168.x.x
  - 公共 IP：與外部網路通訊時使用，由 ISP 分配
    - 公共 IP 可共用（如多台設備透過一個路由器上網）
<hr>
IPv4 vs IPv6：

- IPv4：最多約 42 億個位址，逐漸用完<br>
- IPv6：可用位址達 340 兆兆兆（2¹²⁸），解決位址不足問題

</details>

<details>
<summary> MAC 位址（Media Access Control）唯一且固定</summary>
&nbsp;

- 類似「指紋」，出廠時寫死在網卡上，格式如：a4:c3:f0:85:ac:2d

<hr>

MAC 偽裝（MAC Spoofing）
1. MAC 可被偽造，造成安全風險
2. 若防火牆僅依 MAC 判斷是否放行，容易被冒用<br>

🛜 公共 Wi-Fi（如咖啡店）常依 MAC 控管使用者權限與流量

</details>

---
Part 1：偽裝 Alice 裝置的 MAC 地址進行通信：
<p align="left">
  <img src="/rooms/images/04_02.png" width="600">
</p>
Part 2：獲得 Flag 🎉🎉
<p align="left">
  <img src="/rooms/images/04_03.png" width="600">
</p>


##### 🔐 答題：
1. What does the term "IP" stand for?
   
   “IP”一詞代表什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Internet Protocol`

2. What is each section of an IP address called?
   
   IP 位址的每個部分叫什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Octet`

3. What does the term "MAC" stand for?

     “MAC”一詞代表什麼？

&nbsp;&nbsp;&nbsp;&nbsp; `Media Access Control`

4. What does the term "MAC" stand for?å

     “MAC”一詞代表什麼？

&nbsp;&nbsp;&nbsp;&nbsp; `Media Access Control`

5. Deploy the interactive lab using the "View Site" button and spoof your MAC address to access the site.  What is the flag?

     使用「View Site」 （查看網站） 按鈕部署互動式實驗室，並偽造您的 MAC 位址以訪問該網站。標誌是什麼？

&nbsp;&nbsp;&nbsp;&nbsp; `THM{YOU_GOT_ON_TRYHACKME}`

>> #### Task 4：Ping (ICMP) 
Ping 是一個基本網路工具，用來檢查兩台設備間的連線是否正常。

- 工作原理：
  - 使用 ICMP 協定 傳送「echo」封包到目標設備 
  - 目標回傳「echo reply」封包 
  - 依此測量延遲時間（毫秒），確認是否能通訊

  
`ping IP address or website URL`

---
Part 1：於上方輸入 IP address: 8.8.8.8
<p align="left">
  <img src="/rooms/images/04_04.png" width="600">
</p>
Part 2：獲得 Flag 🎉🎉
<p align="left">
  <img src="/rooms/images/04_05.png" width="600">
</p>

##### 🔐 答題：
1. What protocol does ping use?
   
    ping 使用什麼協定？
   
&nbsp;&nbsp;&nbsp;&nbsp; `ICMP`

2. What is the syntax to ping 10.10.10.10?
   
    ping 10.10.10.10 的語法是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `ping 10.10.10.10`

3. What flag do you get when you ping 8.8.8.8?
    
    ping 8.8.8.8 時得到什麼標誌？

&nbsp;&nbsp;&nbsp;&nbsp; `THM{I_PINGED_THE_SERVER}`