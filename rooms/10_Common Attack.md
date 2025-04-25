# Common Attack

**🔍 常見攻擊**

THM路徑：https://tryhackme.com/room/commonattacks

---

>> #### Task 1：介紹

>> #### Task 2：社交工程

🧩 社交工程**多層次攻擊**

1. 取得初步資訊：從社群媒體挖資料（生日、寵物名、常去的店等）。

2. 假冒電話／公司：冒充電信客服、銀行人員，藉此拿到進一步個資。

3. 層層推進（Snowball Effect）：從小資訊一步步滾到帳號、信用卡、甚至人生控制權。
---
🧨 **常見的社交工程手法**

| 手法 | 說明 |
|------|------|
| 💡假冒客服打電話 | 騙客服交出你的帳號 / 重設密碼 |
| 💾散佈 USB | 在停車場丟 USB，誘人插入電腦，內含惡意程式 |
| 🪛假充電線 | 公共場所放置惡意「充電線」，實際可安裝後門或鍵盤記錄器 |
| 🧑‍💼冒充公司內部人員 | 藉由話術、信任、語氣騙取內部人員協助取得系統存取 |

---

🛡️ 如何**防範**社交工程？

1. 雙重驗證要開啟 → 設定難猜的安全問題（或故意填錯的答案）。

2. 陌生 USB 不插入→ 別將來路不明的 USB 插進任何你在意的設備裡。

3. 驗證身份 → 陌生來電自稱客服，請用官方網站上的電話號碼回撥確認。

4. 不要告訴任何人密碼 → 沒有 legit 的公司人員會向你索取帳密。

##### 🔐 答題：
2. What was the original target of Stuxnet?
   
   Stuxnet 的最初目標是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `The Iran Nuclear Programme`


>> #### Task 3：社交工程：網路釣魚（Phishing）
_攻擊者透過 Email、簡訊（SMS）、語音（電話） 等方式，引導你點擊惡意連結_<br>

目的通常是：盜取帳號密碼、信用卡、銀行資料 → 安裝惡意程式，進入你裝置或公司內網

---

| 類型               | 說明 |
|--------------------|------|
| **General Phishing** | 大量發送，無特定目標，內容常有明顯錯誤，如假冒 Amazon、銀行通知等 |
| **Spearphishing**   | 有針對性，對特定公司或人設計，內容更逼真、較難辨識 |
| **Whaling**         | 專針對高層主管（CEO、CFO 等），手法精緻、社工精準、破壞力大 |

---

🪤 常見釣魚手法

1. 假冒知名品牌（Amazon、銀行、快遞…）
2. 製作「假登入頁面」騙你輸入帳密
3. 使用像真的網址（例：royalmai1.co.uk）替代正確網址（royalmail.co.uk）
4. 偽造寄件者 Email 地址，看起來像 legit 的帳號（實際為 Gmail）
5. 在 Email 內用超連結文字遮蔽真正網址（滑鼠移過去才能看到）

---

🛡️ 如何**防範 Phishing**？

| 建議行為                           | 說明 |
|------------------------------------|------|
| 刪除不明郵件，不點不開             | 如果來路不明、語氣奇怪、附加檔案 → 立刻刪除 |
| 不要點 Email 裡的超連結             | 寧可自己手動開網站，確認網址拼字正確 |
| 不要插不明的附件或裝置             | 包含 USB、CD、壓縮檔等，尤其是陌生人或未預期寄來的 |
| 使用「一次性信箱」處理公開活動註冊 | 避免你的主信箱被加入垃圾信名單 |
| 電腦與防毒軟體保持更新             | 有些釣魚網頁會試圖植入木馬或鍵盤記錄器 |
| 若不小心中招，馬上改密碼、通知 IT 或客服 | 越快行動，越有機會阻止進一步損害 |

<p align="left">
  <img src="/rooms/images/10_01.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/10_02.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/10_03.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/10_04.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/10_05.png" width="600">
</p>

##### 🔐 答題：
2. The static site will display a series of emails and text messages. You will be asked to identify which of these messages are genuine and which are phishing attempts. Once you have successfully identified all of the messages you will be presented with a flag to enter, here.
   
   靜態網站將顯示一系列電子郵件和簡訊。您將被要求識別這些郵件中哪些是真實的，哪些是網路釣魚企圖。成功識別所有消息后，您將看到一個旗子供您輸入，請在此處。
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{I_CAUGHT_ALL_THE_PHISH}`

>> #### Task 4：惡意軟體和勒索軟體

- **Malware（惡意軟體）**<br>
  - 是指任何設計來替攻擊者執行惡意行為的軟體<br>
  - 常見行為包含：盜資料、損壞系統、執行任意指令、建立遠端操控（C2）

- **Ransomware（勒索軟體）**
  - 會大量感染裝置，加密所有資料
  - 通常會要求你在限時內付款（通常是加密貨幣）
  - 恢復與否，全看駭客「心情」

🔥 著名案例：WannaCry 勒索病毒

---

🚚 常見**傳播方式**（Delivery Methods）

| 方法                     | 說明                                               |
|--------------------------|----------------------------------------------------|
| 社交工程 / 鉤魚郵件      | 寄 Word/Excel 附檔，內含「巨集（macro）」病毒       |
| 執行檔（`.exe`、`.bat`、`.ps1`） | 一點就中，利用人類好奇心                             |
| 網站漏洞攻擊             | 利用網站伺服器弱點滲透公司內網                      |
| 插入惡意 USB             | 將 USB 掉在辦公室或公開場合引誘人插入              |

---

🛡️ 如何**防範** Malware / Ransomware？

| 防範措施                             | 說明                                                                 |
|--------------------------------------|----------------------------------------------------------------------|
| ✅ 隨時更新系統與軟體                | 修補安全漏洞最基本也是最關鍵的動作                                   |
| 🚫 不點擊可疑連結或檔案              | 特別是 Email 附檔或未預期的「啟用內容」按鈕                          |
| 🛠️ 不插不明 USB 裝置                | 發現陌生 USB、記憶卡 → 直接交給 IT 或警察                            |
| 📀 定期備份資料！                    | 有備份就不怕被勒索！                                                 |
| 🧱 保持防毒軟體啟用並更新至最新版     | 最後一道防線                                                         |
| 🕵️‍♀️ 中毒時：別急著關機、別付款     | 拔網路 → 聯繫 IT 或警方 → 不要破壞現場痕跡                          |

##### 🔐 答題：
1. What currency did the Wannacry attackers request payment in?
   
   Wannacry 攻擊者要求以什麼貨幣付款？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Bitcoin`

>> #### Task 5：密碼和身份驗證

- 強密碼：
   - 傳統：複雜性導向
   - 現代：使用長句（Passphrase）
  -  理想：隨機產生 + 密碼管理工具

- 弱密碼：複雜度低 + 共用密碼

---
**密碼外洩（Exposed Passwords）:**<br>

如果網站遭駭、資料庫被公開，可能出現：

| 狀況類型       | 說明                                                                 |
|----------------|----------------------------------------------------------------------|
| ✅ 安全雜湊儲存 | 攻擊者只能看到加密過的密碼（安全度取決於密碼強度）                    |
| ❌ 明文或可解密 | 使用者帳密完全外流，可被攻擊者用來登入甚至販售                        |

---
**密碼攻擊類型（Password Attacks）：**<br>

🖥 **Local Attacks（本地破解）**：

   1. 前提：已拿到一份帳號+密碼雜湊值（如從資料庫竊取）。
   2. 使用字典檔或暴力破解工具（如 hashcat、John the Ripper）。
   3. 變體攻擊（Hybrid）＝ 字典 + 變化組合（加數字、符號、大小寫轉換）。

🌐 **Remote Attacks（遠端攻擊）**：

| 類型                 | 說明                                                             |
|----------------------|------------------------------------------------------------------|
| Brute-force          | 針對已知帳號一個一個嘗試密碼                                      |
| Credential Stuffing  | 用外洩帳密試各大平台，尤其是重複使用的帳密                         |

---
利用密碼清單暴力破解（已知哈希值）：

<p align="left">
  <img src="/rooms/images/10_06.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/10_07.png" width="600">
</p>

##### 🔐 答題：
3. What is the password?
   
   密碼是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `TryHackMe123!`

>> #### Task 6：多重身份驗證和密碼管理員）

<details>
<summary><strong>Multi-Factor Authentication（MFA）</strong></summary>

&nbsp;&nbsp;&nbsp;&nbsp;_登入帳號時，需要「超過一項」驗證方式才能成功_<br>

| 類型             | 說明                                     |
|------------------|------------------------------------------|
| 第一因素 你知道的 | 密碼                                     |
| 第二因素 你有的   | 驗證碼（如手機簡訊、App 產生的 TOTP）   |
| 第三因素 你是誰   | 生物特徵（如指紋、臉部辨識）             |

---

⏱ 常見的第二因素：TOTP（Time-based One Time Password）
- 形式： App 顯示一組 6 位數字，每 30 秒刷新
- 工具 App：Google Authenticator、Authy
- 安全性遠高於簡訊驗證（SMS 易攔截、轉移）

📌 **建議：** 看到 MFA 選項就開！就算被盜密碼，也需要實體驗證器才能登入

</details>

<details>
<summary><strong>Password Managers</strong></summary>

&nbsp;&nbsp;&nbsp;&nbsp;_幫你「產生、儲存、填入」強密碼，只要記住一組主密碼就好_<br>


| 功能項目                    | 說明                                         |
|-----------------------------|----------------------------------------------|
| 密碼保險庫（Vault）         | 加密儲存密碼，可在本地或雲端跨裝置使用        |
| 自動填寫                    | 登入網站或 App 時，自動幫你填入帳密           |
| 密碼產生器                  | 一鍵產生長且隨機的強密碼                     |
| 主密碼 / 生物辨識登入       | 用主密碼或指紋登入保險庫，管理所有帳密        |

---

🧰 常見工具：

- Bitwarden（免費＋開源）
- 1Password（付費，設計佳）
- LastPass（主流品牌）
- KeePass（離線儲存，偏技術取向）

建議選擇：**具跨平台、自動填寫、開源或好口碑**

##### 🔐 答題：
3. Where you have the option, which should you use as a second authentication factor between SMS based TOTPs or Authenticator App based TOTPs (SMS or App)?
   
   如果可以選擇，您應該使用哪個作為基於 SMS 的 TOTP 或基於 Authenticator 應用程式的 TOTP（SMS 或應用程式）之間的第二個身份驗證因素？
   
&nbsp;&nbsp;&nbsp;&nbsp; `App`

</details>

>> #### Task 7：公共網路安全

🧨 為什麼**公共 WiFi**危險？
  1. 很多攻擊者會假冒 WiFi（釣魚熱點）吸引連線
  2. 攻擊者可以攔截你所有未加密的流量 → Man-in-the-Middle 攻擊
  3. 若網站沒用 HTTPS，你輸入的帳密、資料都可能被偷
  4. 即使是正常 WiFi，只要你連進去，你的設備也可能暴露在其他使用者面前（被掃描、攻擊）

🚨對策：

- 避免使用不受信任的 WiFi：<br>
使用手機熱點（Hotspot） 、 私人網路

- 使用 VPN（Virtual Private Network）：<br>
    ✅ VPN 功能：<br>
   1. 加密你所有的網路流量
   2. 就算被攔截，駭客也只能看到亂碼
   3. 可自建（較進階）或使用商業 VPN（例如：ProtonVPN、Mullvad）

   ⚠️ 小心免費 VPN：<br>
   1. 可能自己就是資料販子，反而不安全

- 檢查網站是否使用加密（HTTPS / TLS）：<br>
    ✅ 檢查方法：
   1. 看網址前面是否有 🔒 鎖頭
   2. 代表該網站啟用了 TLS 加密（傳輸加密）
   
   ⚠️ 注意事項：
   1. 有鎖頭 ≠ 網站安全，只是代表連線被加密

    ❌ 若出現：
    1. 鎖頭有叉叉 / 驚嘆號
    2. 瀏覽器跳出「安全憑證錯誤」警告都代表可能有問題，不要輸入任何資料！

---
🔐 **安全使用**公共網路的守則：

| 行為                                | 說明                               |
|-------------------------------------|------------------------------------|
| ✅ 使用手機熱點                     | 最安全                             |
| ✅ 開啟 VPN 後再連 WiFi             | 可防止攔截                         |
| ✅ 確認網站有 HTTPS 加密            | 確保資料傳輸加密                   |
| ❌ 在 HTTP 網站輸入密碼 / 信用卡資料 | 等於自動送給駭客                   |
| ❌ 忽略 TLS 憑證錯誤強行進入網站     | 可能是有人在竄改連線，**立即離開** |

---

傳輸資料時開啟 VPN、HTTPS 保護資料：

<p align="left">
  <img src="/rooms/images/10_08.png" width="600">
</p>

>> #### Task 8：備份



>> #### Task 9：更新和補丁

>> #### Task 10：結論
