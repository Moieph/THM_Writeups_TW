# Defensive Security Intro
**防禦性安全入門**

> #### Task 1：防禦性安全介紹

1. 使用者資安意識（User cyber security awareness）<br>
  提升使用者的資安知識，有助防範攻擊。


2. 資產紀錄與管理（Documenting and managing assets）<br>
   掌握系統與裝置資產，才能提供適當防護。


3. 系統更新與修補（Updating and patching systems）<br>
   定期更新設備，避免漏洞被利用。


4. 預防性安全設備（Setting up preventative security devices）<br>
   防火牆控管流量，IPS 阻擋已知攻擊。


5. 日誌記錄與監控（Setting up logging and monitoring devices）<br>
   記錄與監控可偵測異常活動，防止入侵。

##### 🔐 答題：
1. Which team focuses on defensive security?
   
    哪個團隊專注於防禦性安全？
   
&nbsp;&nbsp;&nbsp;&nbsp; `
Blue Team  `

---

> #### Task 2：防禦安全領域


<details>
<summary> 安全營運中心 ( SOC ) Security Operations Center</summary>  
&nbsp;&nbsp;&nbsp;&nbsp;────────────<br>
  
 &nbsp;&nbsp;&nbsp;&nbsp;漏洞（Vulnerabilities）：</b> <br>
 &nbsp;&nbsp;&nbsp;&nbsp;發現漏洞應儘速修補，無法修補時採其他防護措施。修補不一定由 SOC 執行。

 &nbsp;&nbsp;&nbsp;&nbsp;違反政策（Policy violations）：<br>
 &nbsp;&nbsp;&nbsp;&nbsp;使用者若違反公司安全規範（如上傳機密資料），即屬違規行為。

 &nbsp;&nbsp;&nbsp;&nbsp;未授權活動（Unauthorized activity）：<br>
 &nbsp;&nbsp;&nbsp;&nbsp;帳號遭盜用登入，SOC 需即時偵測與阻擋，避免損害擴大。

 &nbsp;&nbsp;&nbsp;&nbsp;網路入侵（Network intrusions）：<br>
&nbsp;&nbsp;&nbsp;&nbsp;入侵風險無法完全避免，需快速偵測阻止後續攻擊。

</details>

<details>
<summary> 威脅情報（Threat Intelligence）</summary>

&nbsp;&nbsp;&nbsp;&nbsp;_蒐集與潛在敵人相關資訊，目的是預測攻擊、提前防禦。_

&nbsp;&nbsp;&nbsp;&nbsp;────────────<br> 
&nbsp;&nbsp;&nbsp;&nbsp;識別威脅行為者<br>
&nbsp;&nbsp;&nbsp;&nbsp;預測攻擊模式<br>
&nbsp;&nbsp;&nbsp;&nbsp;擬定應對策略，降低風險

</details>

<details>
<summary> 數位取證和事件回應 ( DFIR ・Digital Forensics and Incident Response）</summary>

&nbsp;&nbsp;&nbsp;&nbsp;_用科學方法調查攻擊，分析證據。_

&nbsp;&nbsp;&nbsp;&nbsp;────────────<br>

1. 檔案系統（File System）<br>
   分析硬碟影像，可看出程式安裝、檔案建立與刪除痕跡。
2. 系統記憶體（System memory）<br>
   記憶體取證可發現未寫入磁碟的惡意程式。
3. 系統日誌（System logs）<br>
   記錄系統活動，即使攻擊者刪除痕跡，可能留線索
4. 網路日誌（Network logs）<br>
   分析封包記錄，判斷是否遭攻擊及其影響。
</details>

<details>
<summary> 事件回應（Incident Response）</summary>

&nbsp;&nbsp;&nbsp;&nbsp;_面對資料外洩或網路攻擊，事件回應能減少損害、加速恢復。應事先制定計畫。_

&nbsp;&nbsp;&nbsp;&nbsp;────────────<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**四大階段：**

1. 準備（Preparation）：<br>
   建立訓練有素的應變團隊，預防事件發生
2. 偵測與分析（Detection and Analysis）:<br>
   偵測異常並分析事件嚴重程度
3. 遏制、根除、復原（Containment, Eradication, and Recovery）：<br>
   控制事件影響、清除威脅並恢復系統
4. 事件後活動（Post-Incident Activity）：<br>
  記錄報告與經驗教訓，強化未來防禦


<p align="center">
  <img src="/rooms/images/02_01.png" width="600">
</p>

</details>

<details>
<summary> 惡意軟體分析（Malware Analysis）</summary>

&nbsp;&nbsp;&nbsp;&nbsp;_惡意軟體是用來破壞或操控系統的程式、文件或檔案。_

&nbsp;&nbsp;&nbsp;&nbsp;────────────<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**常見類型：**<br> 

- 病毒（Virus）：
附著程式、傳播感染，破壞或刪除檔案
- 特洛伊木馬（Trojan Horse）：
假裝正常程式，實暗藏惡意控制功能
- 勒索軟體（Ransomware）：
加密檔案、勒索贖金換解密金鑰

&nbsp;&nbsp;&nbsp;&nbsp;────────────<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**惡意軟體分析目標：**<br> 

- 靜態分析（Static analysis）：

  不執行程式，透過程式碼檢查惡意行為，需懂組合語言。

- 動態分析（Dynamic analysis）：

   在安全環境中執行程式，觀察其實際行為與影響。

</details>


##### 🔐 答題：
1. What would you call a team of cyber security professionals that monitors a network and its systems for malicious events?
   
    您如何稱呼監控網路及其系統是否存在惡意事件的網路安全專業人員團隊？

&nbsp;&nbsp;&nbsp;&nbsp; `Security Operations Center`

2. What does DFIR stand for?
   
   DFIR 代表什麼？

&nbsp;&nbsp;&nbsp;&nbsp; `Digital Forensics and Incident Response`

3. Which kind of malware requires the user to pay money to regain access to their files?

   哪種惡意軟體需要用戶付費才能重新獲得對其檔的訪問許可權？

&nbsp;&nbsp;&nbsp;&nbsp; `Ransomware `

> #### Task 3：防禦性安全的實際範例

假設您是負責保護銀行的安全運營中心 （SOC） 分析師。該銀行的 SOC 使用安全資訊和事件管理 （SIEM） 工具，該工具從各種來源收集與安全相關的資訊和事件，並將它們顯示在一個儀錶板中。如果 SIEM 發現可疑情況，將生成警報。

---

Part 1：檢查 SIEM 儀表面板中的警報中，找到可疑 IP 地址(143.110.250.149)
<p align="left">
  <img src="/rooms/images/02_02.png" width="600">
</p>

Part 2：檢查 IP 地址以查看它是否是惡意的或可疑的
<p align="left">
  <img src="/rooms/images/02_03.png" width="600">
</p>

Part 3：查看檢查結果，我們知道 IP 地址143.110.250.149是惡意的，需要將其上報給相關的工作人員。
<p align="left">
  <img src="/rooms/images/02_04.png" width="600">
</p>

Part 4：將事件上報給 SOC Team Lead——安全運營中心團隊負責人
<p align="left">
  <img src="/rooms/images/02_05.png" width="600">
</p>

Part 5：阻止惡意 IP 地址(143.110.250.149)訪問目標公司的權限
<p align="left">
  <img src="/rooms/images/02_06.png" width="600">
</p>

Part 6：獲得 Flag 🎉🎉
<p align="left">
  <img src="/rooms/images/02_07.png" width="600">
</p>

##### 🔐 答題：
1. What is the flag that you obtained by following along?
   
    您通過跟隨獲得的標誌是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{THREAT-BLOCKED}`

