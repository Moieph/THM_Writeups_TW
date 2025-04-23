# Cyber Kill Chain  

**⚔️ 網路攻擊鏈**

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

---

