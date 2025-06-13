# Metasploit: Introduction

**🟥 Metasploit 簡介**

THM路徑：https://tryhackme.com/room/metasploitintro

---

>> #### Task 1：Metasploit 簡介

🔧 Metasploit Framework 簡介

🎯 用途：
- 滲透測試全流程支援（從偵察 → 利用 → 後滲透）
- 也能用於漏洞研究與 Exploit 開發

---

🧱 版本比較：

| 版本名稱                     | 特點                         |
| ------------------------ | -------------------------- |
| **Metasploit Pro**       | 商業版，有圖形化操作介面（GUI），支援自動化與管理 |
| **Metasploit Framework** | 開源版本、命令列操作，本課程以此為主         |

---

📦 主要組件：

| 元件名稱         | 說明                                                                     |
| ------------ | ---------------------------------------------------------------------- |
| `msfconsole` | 主要操作介面，命令列介面                                                           |
| **Modules**  | 各種模組，例如：exploit、scanner、payload 等                                      |
| **Tools**    | 獨立小工具，如：`msfvenom`、`pattern_create`、`pattern_offset`（後兩者用於 Exploit 開發） |

>> #### Task 2：Metasploit 的主要組件

💻 Metasploit 操作介面：

- 使用 `msfconsole` 開啟命令列操作介面
- 所有模組都可透過 `msfconsole` 互動呼叫

---

🧠 基本名詞釐清：

| 名稱                   | 說明                                |
|----------------------| --------------------------------- |
| **Vulnerability（漏洞）** | 目標系統中設計、邏輯或程式錯誤，如未授權存取、溢位等        |
| **Exploit（漏洞利用）**     | 利用漏洞來觸發異常行為的程式碼（可導致遠端執行等）         |
| **Payload（惡意負載）**    | 被植入到目標系統、用於執行惡意功能（如打開 shell、執行指令） |

---

🧱 Metasploit 模組分類：

🔹 1. **Auxiliary（輔助模組）**
- 功能：掃描器、爬蟲、fuzzer、sniffer 等
- 常見路徑：`/auxiliary/scanner/...`

<p align="left">
  <img src="/rooms/images/33_01.png" width="600">
</p>


🔹 2. **Exploits（漏洞利用模組）**
- 按平台分類（如 `Windows`, `Linux`, `Multi` 等）
- 每個 exploit 可搭配 payload 使用

<p align="left">
  <img src="/rooms/images/33_04.png" width="600">
</p>

🔹 3. **Payloads（惡意負載）**

- 四種子類型：

| 類型           | 說明                                       |
| ------------ | ---------------------------------------- |
| **Adapters** | 包裝 payload 成其他語言形式（如 PowerShell）         |
| **Singles**  | 單一自足 payload，不需下載其他模組（例如：add user）       |
| **Stagers**  | 用於先建立連線通道，再接收主 payload，適合隱藏或小型注入         |
| **Stages**   | 實際 payload 程式碼，由 stager 負責下載執行（功能完整、可擴展） |

 判斷技巧：

`shell_reverse_tcp`：單一 payload（inline）
`shell/reverse_tcp`：分段 payload（staged）


<p align="left">
  <img src="/rooms/images/33_06.png" width="600">
</p>


🔹 4. **Encoders（編碼器）**
- 將 payload 編碼，降低被防毒軟體辨識的機率
- 效果有限，因現代防毒多用行為偵測

<p align="left">
  <img src="/rooms/images/33_02.png" width="600">
</p>


🔹 5. **Evasion（防毒繞過模組）**
- 特別為繞過防毒與應用白名單設計（如 AppLocker、Defender)

<p align="left">
  <img src="/rooms/images/33_03.png" width="600">
</p>

🔹 6. **NOPs（無操作指令）**
- No OPeration
- 填充用，維持 payload 長度穩定（如 x86 架構中的 `0x90`）

<p align="left">
  <img src="/rooms/images/33_05.png" width="600">
</p>

🔹 7. **Post（滲透後模組）**
- 成功進入系統後使用，如帳號列舉、提權、收集系統資訊等
- 分平台分類（`Windows`、`Linux`、`Android`、`Osx`…）

<p align="left">
  <img src="/rooms/images/33_07.png" width="600">
</p>

---
- 查看模組分類與數量：

    `ls -l /opt/metasploit-framework/embedded/framework/modules/`

- 


>> #### Task 3：Msf 控制台

>> #### Task 4：使用模組

>> #### Task 5：總結