# Traffic Analysis Essentials

**🟦 Traffic Analysis Essentials 要點**

THM路徑：https://tryhackme.com/room/trafficanalysisessentials

---

>> #### Task 1：介紹

Network Traffic Analysis（NTA）➜ **網路流量分析** 

- 主要任務：分析網路中的資料流量


- 目標：發現異常行為與潛在問題，例如：
  - 惡意連線
  - 資料外洩
  - 非授權存取

>> #### Task 2：網路安全和網路數據

🔐 網路安全（Network Security）重點概念：

- 核心關注點：
  - **驗證**（Authentication）
  - **授權**（Authorisation）

---

三層控制層級（Base Control Levels）：

| 層級 | 說明 |
|------|------|
| 🧱 物理控制（Physical） | 防止未經授權的實體接觸，如設備上鎖、線路安全 |
| 🛠️ 技術控制（Technical） | 控制資料訪問，如使用加密通道、驗證系統 |
| 📋 行政控制（Administrative） | 建立政策、權限分級、認證流程等 |

---
🧭 兩大主軸：**存取控制 & 威脅控制**

✅ 存取控制（Access Control）元素

| 元素                                              | 說明 |
|-------------------------------------------------|------|
| Firewall Protection                             | 管控網路流量，阻擋惡意連線與應用層威脅 |
| 網路存取控制 <br> Network Access Control (NAC)        | 驗證設備符合標準才允許連線 |
| 身份與存取管理<br>Identity and Access Management (IAM) | 管控人員與系統的存取權限 |
| 負載平衡 Load Balancing                             | 平衡資源負載，提升處理效率 |
| 網路分段 Segmentation                               | 分隔內外網、敏感系統與使用者權限 |
| 虛擬私人網路 VPN                                      | 建立加密通道，保護遠端存取安全 |
| Zero Trust Model                                | 永不信任，總是驗證；最小權限原則 |


⚠️ 威脅控制（Threat Control）元素

| 元素                                                                                       | 說明 |
|------------------------------------------------------------------------------------------|------|
| 入侵檢測和防禦 <br> Intrusion Detection and Prevention (IDS/IPS)                                | 偵測（IDS）或阻擋（IPS）異常網路行為 |
| 資料外洩防護 <br> Data Loss Prevention (DLP)                                                   | 檢查並阻止敏感資料傳輸 |
| 端點保護 <br>Endpoint Protection                                                             | 保護終端設備，整合多層防禦 |
| 雲端安全 <br>Cloud Security                                                                  | 防止雲端系統資料外洩（如加密、VPN） |
| 安全資訊和事件管理 <br>Security Information and Event Management (SIEM)                           | 整合日誌與事件資訊進行威脅分析 |
| 安全編排自動化和回應 <br>Security Orchestration Automation and Response (SOAR)                     | 自動化安全事件回應流程 |
| 網路流量分析和網路檢測和回應 <br>Network Traffic Analysis & Network Detection and Response (NTA & NDR） | 分析網路封包，識別潛在攻擊 |

---

🛠️ 常見網路安全營運流程

| 階段 | 說明 |
|------|------|
| 部署 | 安裝設備與軟體、初始化設定 |
| 配置 | 設定功能、權限與政策 |
| 管理 | 控制 NAT、VPN、策略調整 |
| 監控 | 系統與使用者活動監控、封包擷取 |
| 維護 | 更新、修補、憑證與授權管理 |

典型的 Network Security Management：
<p align="left">
  <img src="/rooms/images/23_01.png" width="600">
</p>

---

🤝 MSS（受託安全服務）

- 由第三方 MSSP 提供的外包安全服務，常見包含：

| 項目      | 說明                  |
| ------- | ------------------- |
| 🧪 滲透測試 | 模擬攻擊者行為，評估防禦能力      |
| 🩻 漏洞掃描 | 掃描環境漏洞與風險點          |
| 🚨 事件應變 | 快速識別、隔離、移除資安事件      |
| 📈 行為分析 | 建立使用者 / 系統行為模型，偵測異常 |



>> #### Task 3：流量分析

>> #### Task 4：結論