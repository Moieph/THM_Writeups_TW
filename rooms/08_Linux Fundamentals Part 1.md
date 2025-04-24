# Linux Fundamentals Part 1 

**🐧 Linux 基礎知識 部分 1**

- THM路徑：https://tryhackme.com/room/linuxfundamentalspart1

- 官方影片：https://youtu.be/42u_2e6eNF4?si=5G3x-KfvIMHzU84a

>> #### Task 1：介紹

>> #### Task 2：Linux 的背景知識

🐧 Linux 發行版（Flavours）

「Linux」不是單一系統，而是統稱一系列 基於 **UNIX** 的作業系統。<br>
因為是 **開源**，所以可以根據用途發展出不同版本（大小、功能不一）。

---

常見發行版：

- **Ubuntu、Debian**：用途廣泛，可當伺服器也可當桌面系統  
- 📁 **Ubuntu Server 只需 512MB RAM 就能跑！**

##### 🔐 答題：
1. Research: What year was the first release of a Linux operating system?
   
   研究：Linux 作系統的首次發佈是哪一年？
   
&nbsp;&nbsp;&nbsp;&nbsp; `1991`

>> #### Task 3：與您的第一台 Linux 電腦互動（瀏覽器內）

>> #### Task 4：運行您的前幾個命令

基礎指令：

| 指令    | 說明                                     |
|---------|------------------------------------------|
| `echo`  | 輸出你指定的文字（例如：`echo Hello`）   |
| `whoami`| 顯示你目前登入的使用者名稱                |

如果字串中有一個或多個空格，則應使用雙引號將其引起來，例如： `echo "Hello Friend!"`。

##### 🔐 答題：
1. If we wanted to output the text "TryHackMe", what would our command be?
   
   如果我們想輸出文本 「TryHackMe」，我們的命令會是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `echo TryHackMe`

2. What is the username of who you're logged in as on your deployed Linux machine?
   
   您在部署的 Linux 電腦上登錄的使用者的使用者名是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `tryhackme`

>> #### Task 5：與檔案系統交互！

| 指令     | 全名（Full Name）         | 中文說明                                    |
|----------|----------------------------|---------------------------------------------|
| `ls`     | **listing**                | 列出目前目錄下的檔案與資料夾               |
| `cd`     | **change directory**       | 切換目錄（例如： `cd /home/user`）         |
| `cat`    | **concatenate**            | 查看檔案內容、串接檔案內容                  |
| `pwd`    | **print working directory**| 顯示目前所在的路徑位置                      |

##### 🔐 答題：
1. On the Linux machine that you deploy, how many folders are there?
   
   在您部署的 Linux 電腦上，有多少個資料夾？
   
&nbsp;&nbsp;&nbsp;&nbsp; `4`

2. Which directory contains a file? 
   
   哪個目錄包含檔？
   
&nbsp;&nbsp;&nbsp;&nbsp; `folder4`

3. What is the contents of this file?
   
   這個文件的內容是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Hello World`

4. Use the cd command to navigate to this file and find out the new current working directory. What is the path?
   
   使用 cd 命令導航到此檔案並找出新的當前工作目錄。路徑是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `/home/tryhackme/folder4`









<!--

THM路徑：https://tryhackme.com/room/cyberkillchainzmt

>> #### Task 1：介紹

Kill Chain（殺戮鏈）原為軍事術語，指的是攻擊流程的結構：<br>
**目標識別 → 下令攻擊 → 執行摧毀**

>> #### Task 2：階段 1️⃣ Reconnaissance（偵察）

**定義：**
    Reconnaissance 是攻擊者在發動攻擊前的「情報蒐集階段」，目的是收集目標系統與受害者的所有可得資訊，進行攻擊規劃。

- OSINT（開放式情報）
  - Open-Source Intelligence，即透過公開資源蒐集目標資料
  - 通常為攻擊鏈的 **第一步**
  - 攻擊者會蒐集的資訊包括：公司規模、員工名單、電子郵件地址、電話號碼、網域名稱（子網域）、社群媒體公開資料

---

- Email Harvesting（電子郵件蒐集）
  - 透過公開、付費或免費來源取得電子郵件地址
  - 常用於發動 **釣魚攻擊（Phishing）**
    - 偷取登入帳密、信用卡資訊等敏感資料

##### 🔐 答題：
1. What is the name of the Intel Gathering Tool that is a web-based interface to the common tools and resources for open-source intelligence?
   
   Intel Gathering Tool 是一個基於 Web 的介面，用於開源智慧的常用工具和資源，它的名稱是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `OSINT Framework`

2. What is the definition for the email gathering process during the stage of reconnaissance?
   
   偵查階段的電子郵件收集過程的定義是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `email harvesting`

>> #### Task 3：階段 2️⃣ Weaponization（武器化）

**定義：**
    Weaponization 是指攻擊者將惡意程式（Malware）與漏洞利用程式（Exploit）**結合成可傳送的惡意載荷（Payload）**，以供後續投遞與執行。

此階段通常 **不與受害者直接互動**，純粹在幕後製作「攻擊武器」。

| 術語      | 定義                                                       |
|-----------|------------------------------------------------------------|
| **Malware** | 惡意軟體，用於破壞、干擾或未經授權存取系統                     |
| **Exploit** | 利用系統或應用漏洞的程式碼或手法                             |
| **Payload** | 實際在目標系統上執行的惡意程式碼                              |


---

🛠️武器化常見手法：

| 手法                   | 說明                                                                 |
|----------------------|----------------------------------------------------------------------|
| 📝 感染的 Office 文件     | 將惡意巨集（Macro）或 VBA 指令碼植入 Word/Excel 文件中                |
| 💾 USB 蠕蟲病毒植入        | 製作感染 USB 的惡意 Worm，並公開散播（如在公共場合丟置）              |
| 🛠️ 選擇 C2（指揮控制）技術    | 用於遠端執行命令、下發更多惡意程式（參考 MITRE ATT&CK）              |
| 🔐 選擇後門（Backdoor）植入方式 | 預先設定存取管道，繞過目標系統的安全機制                              |

---
- 🎯 小結：
  - Weaponization 是 **攻擊準備工作中的核心階段**。
  - 此階段強調「整合」惡意程式與漏洞利用，形成可用的攻擊武器 。
  - 優化 Payload 製作流程可大幅提升攻擊成功率與隱蔽性。

##### 🔐 答題：
1. This term is referred to as a group of commands that perform a specific task. You can think of them as subroutines or functions that contain the code that most users use to automate routine tasks. But malicious actors tend to use them for malicious purposes and include them in Microsoft Office documents. Can you provide the term for it? 
   
   此術語稱為執行特定任務的一組命令。您可以將它們視為子例程或函數，其中包含大多數使用者用於自動執行日常任務的代碼。但惡意行為者傾向於將它們用於惡意目的，並將其包含在 Microsoft Office 文檔中。您能提供這個術語嗎？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Macro`

>> #### Task 4：階段 3️⃣ Delivery（投遞）
**定義：**
    Delivery 是指攻擊者選擇方式**將惡意程式（Payload / Malware）送達目標裝置**的階段。

此階段是駭客從「準備」轉向「行動」的第一步，方式多樣且具社交工程特性。

---

📬 常見攻擊投遞方式：

| 攻擊手法                          | 說明                                                                                      |
|-------------------------------|-------------------------------------------------------------------------------------------|
| 🐦 Phishing Email（釣魚郵件）       | 最常見的傳遞方式，透過 Email 傳送惡意附件或連結。<br>🧠 **Spear Phishing（目標式釣魚）**：攻擊特定人員，信件內容高度擬真。 |
| 💽 USB Drop Attack（USB 放毒攻擊）  | 攻擊者將含有惡意程式的 USB 散佈於咖啡廳、停車場等地點，誘使人員撿起並插入電腦。                   |
| 💧 Watering Hole Attack（水坑攻擊） | 鎖定目標族群常造訪網站，植入惡意程式。<br>📕 當受害者造訪該站，即會遭遇 **Drive-by Download（隱性下載）**，不知不覺感染惡意程式。<br><br>📌 **攻擊流程**：<br>1. 偵察常用網站<br>2. 利用漏洞植入惡意內容<br>3. 利用「看似無害」的信件或誘因，引導使用者造訪該站（如：促銷、公告） |

---
- 🎯 小結：
  - Delivery 是 **攻擊啟動關鍵點**，任何一種傳遞成功都會開啟後續階段（如 Exploitation）。
  - 此階段大量依賴 **社交工程 + 技術混合**。
  - 針對個別對象（如 Spearphishing、USB 偽裝）往往更有效且更難偵測。

##### 🔐 答題：
1. What is the name of the attack when it is performed against a specific group of people, and the attacker seeks to infect the website that the mentioned group of people is constantly visiting. 
   
   當針對特定人群執行攻擊時，攻擊者試圖感染上述人群不斷訪問的網站，攻擊名稱是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Watering hole attack`

>> #### Task 5：階段 4️⃣ Exploitation（利用）
**定義：**
    Exploitation（利用） 指的是攻擊者在成功投遞惡意程式後，**觸發漏洞或利用受害者操作**，來執行惡意程式碼、取得系統控制權。

這是 Cyber Kill Chain 中關鍵的 **「突破口」**：從「存在惡意」→「實際執行」。

---

🧨可能使用的 Exploit 方式：

| 攻擊手法                                       | 說明                                                                 |
|------------------------------------------------|----------------------------------------------------------------------|
| 🔗 點擊惡意連結或開啟附件                      | 例如觸發巨集、下載勒索程式                                             |
| 🕳️ Zero-day Exploit（零日漏洞）               | 尚未被公開或修補的漏洞，幾乎無法事先偵測。<br>🗣️ FireEye 定義：攻擊一發生「無偵測空窗期」 |
| 🛠️ 利用已知漏洞                                 | 如作業系統漏洞、瀏覽器插件漏洞、Apache 等 Server 弱點                  |
| 🧠 利用人為漏洞                                 | 如弱密碼、重複使用密碼、社交工程誘導                                   |

---

**🕸️ 橫向移動（Lateral Movement）**

**定義（CrowdStrike）：** 攻擊者在取得初步存取後，進一步橫向移動至其他裝置或系統以擴大控制與數據存取。

- 常見做法包括：
  - 竊取憑證（如 Token、Hash、Session）
  - 利用 SMB、RDP、PsExec 等協議跳轉至其他機器
  - 透過 AD 結構識別高價值目標（如 Domain Controller）  


##### 🔐 答題：
1. Can you provide the name for a cyberattack targeting a software vulnerability that is unknown to the antivirus or software vendors? 
   
   您能否提供針對防病毒軟體或軟體供應商未知的軟體漏洞的網路攻擊的名稱？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Zero-day`

>> #### Task 6：階段 5️⃣ Installation（安裝）

**定義：**
    Installation（安裝）是指攻擊者在成功進入系統後，植入惡意後門或持久存取機制，確保未來能夠持續控制系統，即使被中斷連線或系統重啟也能重新連線。

---

🧱核心概念：**Backdoor（後門）**
- 又稱 **「存取點（Access Point）」** 
- 允許攻擊者**繞過安全機制、躲避偵測、保留控制權**
- 可分為：
  - **臨時後門**：初步存取點（可能會被刪除）
  - **持久後門（Persistent Backdoor）**：即使遭清除或系統修補後，仍可重新滲透

---

🎯 攻擊者常見持久化技術：

| 技術手法                                      | 說明                                                                                                                      |
|-----------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| 🖥️ **Web Shell 安裝**                         | - 利用 `.php`、`.asp`、`.jsp` 等語言植入惡意 Web Shell<br>- 讓攻擊者可透過 Web 操控伺服器<br>- 難以偵測，常偽裝成網站檔案                                   |
| 💻 **Meterpreter 後門**                       | - 使用 Metasploit 架構中的 Meterpreter Payload 安裝後門<br>- 提供攻擊者互動式 Shell，可執行惡意指令                                               |
| ⚙️ **修改 / 建立 Windows 服務**（MITRE T1543.003） | - 利用 `sc.exe` 或 `reg` 建立 / 修改服務，惡意程式可開機自動執行<br>- 常假裝成系統程式（例如：Windows Update Helper）欺騙管理員                                                          |
| 🪛 **修改註冊表啟動鍵或啟動資料夾**（MITRE T1547.001） | - 加入惡意執行檔於啟動區域註冊表 `Run` 鍵，或放進啟動資料夾<br>- 路徑如：<br> 單一使用者：`C:\Users\<username>\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup`<br> 所有使用者：`C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp` |
| 🕰️ **Timestomping（時間戳偽造）**             | - 修改檔案的建立、修改、存取時間<br>- 偽裝成系統原生檔案，混淆調查與鑑識工具                                                                              |

##### 🔐 答題：
1. Can you provide the technique used to modify file time attributes to hide new or changes to existing files? 
   
   您能否提供用於修改檔案時間屬性以隱藏新檔案或對現有檔案的更改的技術？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Timestomping`

2. Can you name the malicious script planted by an attacker on the webserver to maintain access to the compromised system and enables the webserver to be accessed remotely? 
   
   您能否說出攻擊者在 Web 伺服器上植入的惡意腳本，以保持對受感染系統的訪問並允許遠端存取 Web 伺服器？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Web shell`

>> #### Task 7：階段 6️⃣ Command & Control（指揮與控制）

**定義：**
    **Command and Control（C2 或 C&C）** 是攻擊者與已感染主機建立溝通通道的過程，讓攻擊者能遠端操控、下指令、傳送惡意載荷或收集資料。

| 名詞        | 說明                                      |
|-------------|-------------------------------------------|
| C2 Channel  | 攻擊者與受感染系統間的通訊管道             |
| Beaconing   | 被感染裝置定期與 C2 Server 聯繫，保持通訊連線狀態 |

---

🛠️ 常見的 C2 通訊協議與方式：

| 通訊方式                       | 描述                                                                 |
|------------------------------|----------------------------------------------------------------------|
| **HTTP / HTTPS（port 80 / 443）** | 🔥 最常見！<br>將惡意通訊混入一般網路流量中，躲過防火牆與監控系統 |
| **DNS Tunneling**            | 受感染的機器不斷向攻擊者的 DNS 伺服器發出 DNS 請求<br>🔁 可規避 HTTPS 過濾，難以察覺 |
| **舊方法：IRC（Internet Relay Chat）** | 傳統 C2 通訊協議，現已不常用，容易被偵測  

---

- **C2 Server 可由攻擊者或另一被攻陷主機架設**
- 多層 C2 架構有助於躲避偵測與分析

---

🕵🏻‍♂️ 實務偵測重點：

| 行為特徵                      | 可能意義                        |
|------------------------------|---------------------------------|
| 主機定時向同一 IP／網域連線    | Beaconing 行為                  |
| DNS 請求頻繁、格式異常        | DNS Tunneling 疑慮              |
| HTTPS 請求但內容為亂碼／不合規 | 隱藏資料傳輸可能性              |
| 非辦公時間大量資料外傳        | 可疑遠端操控或 exfiltration 行為 |

---

🎯 小結：

- **C2 是駭客攻擊流程中 最關鍵的持續控制手段**
- 現今常用 **HTTP/HTTPS、DNS Tunneling** 取代傳統 IRC

- 安全人員應部署：
  - 行為分析（UEBA）
  - DNS 記錄監控
  - 出站流量白名單化與深度封包檢測（DPI）

##### 🔐 答題：
1. What is the C2 communication where the victim makes regular DNS requests to a DNS server and domain which belong to an attacker.  
   
   受害者向屬於攻擊者的 DNS 伺服器和域發出常規 DNS 請求的 C2 通訊是什麼。
   
&nbsp;&nbsp;&nbsp;&nbsp; `DNS Tunneling`

>> #### Task 8：階段 7️⃣ Actions on Objectives（目標行動）

**定義：**
    攻擊者在建立後門、持久化、控制通道之後，**親手實現他最初的意圖**，包含竊密、破壞、勒索、持續滲透等。

---

👾 可能採取的攻擊行動：

| 攻擊行動 | 說明 |
|----------|------|
| 🪪 收集憑證 | 利用工具如 Mimikatz 擷取記憶體中帳密或憑證 |
| 🛠 權限提升 | 透過錯誤設定（如共享權限、服務帳號）提權至系統或網域管理員 |
| 🧠 內部偵察 | 掃描內部網段、互動機器或資源，尋找漏洞與資產 |
| 🔁 橫向移動 | 控制更多機器，擴大滲透與控制範圍 |
| 📤 資訊收集與外洩（Exfiltration） | 傳送敏感資訊至外部 C2 或儲存空間 |
| 🧹 刪除備份與隱蔽痕跡 | 移除原機備份，常與勒索行動搭配（使用 `vssadmin delete shadows`） |
| 🪓 覆蓋或破壞資料 | 操作資料刪除、覆寫磁碟、破壞關鍵系統設定 |

---

🧾 Exfiltration（資料外洩）補充說明：

| 項目 | 內容 |
|------|------|
| 🎯 目標 | 獲取並傳出企業機密、帳號密碼、客戶資料、商業文件 |
| 📚 常用手法 | - 壓縮後傳送至 C2 Server  <br> - 使用加密通訊（HTTPS, DNS Tunneling） <br> - 利用雲端空間（如 Dropbox API） <br> - 偽裝成正常流量傳送資料 |
| 🧙‍♂️ 難以察覺的關鍵點 | - 時間分散傳輸（低頻流量） <br> - 使用正規協議如 DNS / HTTPS <br> - 加密資料封包難以辨識內容 |

---

🔐 防禦建議：

| 方向 | 重點技術 |
|------|-----------|
| 流量監控 | 出站資料異常行為分析、DLP、防火牆封鎖未授權通訊 |
| 檔案完整性 | 使用 FIM（File Integrity Monitoring）偵測刪除或修改行為 |
| 記錄分析 | SIEM 收錄異常日誌，例如大量 VSS 刪除、權限變更 |
| 備份管理 | 建立離線備份點，避免單一系統被清除所有復原資料 |

---

🧠 小結：

Actions on Objectives 是駭客「收網」的時刻。

一旦進入此階段，受害者若無良好偵測與備援，**將承受高額金錢損失、商譽重創、營運癱瘓。**




##### 🔐 答題：
1. Can you provide a technology included in Microsoft Windows that can create backup copies or snapshots of files or volumes on the computer, even when they are in use?  
   
   您能否提供 Microsoft Windows 中包含的技術，該技術可以創建計算機上檔或卷的備份副本或快照，即使它們正在使用中也是如此？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Shadow Copy`

>> #### Task 9：實踐分析

| 攻擊階段                         | 技術名稱                              |
|----------------------------------|-----------------------------------|
| Reconnaissance（偵察）          |                                   |
| Weaponization（武器化）         | PowerShell（軟像執行技術）                |
| Delivery（傳送）                | Spearphishing Attachment          |
| Exploitation（利用）            | Exploit Public-Facing Application |
| Persistence / Priv. Esc.        | Dynamic Linker Hijacking          |
| Command & Control（C2）         | Fallback Channels                 |
| Actions on Objectives（目標達成）| Data from Local System            |

<p align="left">
  <img src="/rooms/images/07_01.png" width="600">
</p>


<p align="left">
  <img src="/rooms/images/07_02.png" width="600">
</p>

##### 🔐 答題：
1. What is the flag after you complete the static site?  
   
   完成靜態網站後，標誌是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{7HR347_1N73L_12_4w35om3}`

>> #### Task 10：結論

🛡 Cyber Kill Chain 的限制與補充建議：

✅ **優點：**
- **協助理解攻擊流程**：從偵察到目標達成，幫助防禦者分析與攔截攻擊行為。
- **改善網路防禦策略**：可以用來補強防線、檢查缺口。

❌ **缺點與限制：**

| 限制點                     | 說明                                                                 |
|----------------------------|----------------------------------------------------------------------|
| 太久沒更新（2011 年版）   | 缺乏針對現代攻擊手法的更新，容易產生防禦落差。                       |
| 聚焦在惡意程式與網路邊界 | 忽略了像是帳號濫用、合法憑證濫用等**內部威脅（Insider Threat）**。 |
| 難以處理複合式攻擊       | 現代攻擊者會結合多種 TTP（策略、技術、程序）以規避偵測，傳統模型難以完整捕捉。 |
| 無法單靠簽章識別惡意     | 對抗「變異化惡意程式」（如修改檔案 hash）與靈活攻擊方式的能力有限。   |