# Red Team Engagements

**🟥 紅隊參與**

THM路徑：https://tryhackme.com/room/redteamengagements

---

>> #### Task 1：介紹

📌 常見的紅隊演練類型（Types of Engagements）

| 類型                      | 說明                                 |
| ----------------------- | ---------------------------------- |
| **Tabletop Exercises**  | 桌面模擬，針對特定威脅場景進行策略討論與決策演練（無實際攻擊）    |
| **Adversary Emulation** | 模擬特定攻擊者（如 APT）完整的 TTPs，測試組織偵測與回應能力 |
| **Physical Assessment** | 針對實體環境進行評估，如社交工程、門禁入侵、實體資產存取測試     |


>> #### Task 2：定義範圍和目標

📘 **Red Team Engagement**：目標設定與範疇界定

---

🎯 **清晰的客戶目標（Client Objectives）**
- 客戶目標是整個紅隊行動的基石。
- 目標應由 **紅隊與客戶雙方共同討論**，確保理解一致、期待一致。
- 若無具體目標，整場 Engagement 將 **缺乏結構與規劃**，容易失控或無效。


🧩 客戶目標的功能：
- 設定行動的主軸與節奏
- 奠定文件撰寫與規劃基礎
- 影響後續的 **規則制定（Rules of Engagement） 與 範疇定義（Scope）**

---

⚔️ Engagement 形式分類

| 分類                          | 說明                                          |
| --------------------------- | ------------------------------------------- |
| 一般滲透測試（Penetration Test）    | 著重於測試內部/網路系統弱點，通常較廣泛、不特定對象，使用通用 TTPs。       |
| 特定對手模擬（Adversary Emulation） | 根據客戶所屬產業（如金融業）模擬特定 APT（如 APT38）行為，目標與技術更聚焦。 |

📌 選擇哪種形式，需依照「客戶目標」與資源決定。

---

🧾 Engagement 範疇（Scope）

- **Scope 是「你能做／不能做」的範圍**，應由 **客戶設定**，紅隊僅可建議或提出爭議。


常見條款範例：

````
- 不得進行資料外洩行為（No exfiltration of data）
- 不可觸碰正式環境伺服器（Production servers are off-limits）
- 子網段 10.0.3.8/18 為不可攻擊目標（Out of Scope）
- 子網段 10.0.0.8/20 為可測試目標（In Scope）
- 不可造成任何系統停機（No system downtime）
- 嚴禁外洩任何 PII 資料（PII exfiltration prohibited）
````

---

🔍  紅隊角度的分析要點

- **動態解讀客戶目標與範疇**，思考若你是攻擊者該如何規劃行動。
- 即便只有目標與範疇，也要能根據這些資訊推導出自己的 **Engagement Plan 行動計畫草案**。
- 若 Scope 不合理，也可由紅隊提出協商建議。

---

🧠 總結流程圖：

````
1️⃣ 客戶目標（Client Objectives）
     ↓
2️⃣ Engagement 類型判定（PT / Emulation）
     ↓
3️⃣ 紅隊策略與資源規劃
     ↓
4️⃣ 客戶設定範疇（Scope）
     ↓
5️⃣ 撰寫 Engagement Plan（行動計畫書）
````
---
閱讀題旨並依序作答

<p align="left">
  <img src="/rooms/images/29_01.png" width="600">
</p>

---

##### 🔐 答題：
2. What CIDR range is permitted to be attacked?
   
   允許攻擊的 CIDR 範圍是多少？    
   
&nbsp;&nbsp;&nbsp;&nbsp; `10.0.4.0/22`

3. Is the use of white cards permitted? (Y/N)
   
   允許使用白卡嗎？（是/否）    
   
&nbsp;&nbsp;&nbsp;&nbsp; `Y`

4. Are you permitted to access "*.bethechange.xyz?" (Y/N)
   
   您是否允許訪問 「*.bethechange.xyz？（是/否）
   
&nbsp;&nbsp;&nbsp;&nbsp; `N`

>> #### Task 3：交戰規則

📄 **紅隊演練規則文件**（Rules of Engagement，RoE）

- RoE 是一份 **具有法律效力的正式文件**，明確記錄紅隊與客戶雙方的行動範圍與權責。
- 通常為第一份進入規劃階段的正式文件。
- 涵蓋：**客戶目標、行動範圍、技術限制、責任分工、聯絡窗口、雙方授權**。
- 通常會搭配 **外部合約或 NDA（保密協議）** 使用。

---

📑 RoE 標準章節結構（依 redteam.guide 整理）

| 區塊名稱                                                    | 說明                                    |
| ------------------------------------------------------- | ------------------------------------- |
| **Executive Summary**（執行摘要）                             | 概要說明文件內容與授權範圍。                        |
| **Purpose**（目的）                                         | 定義 RoE 文件存在的理由。                       |
| **References**（參考標準）                                    | 如 HIPAA、ISO 27001 等引用依據。              |
| **Scope**（範疇）                                           | 明確記錄可攻擊與不可攻擊的範圍（如 IP、系統、時段）。          |
| **Definitions**（術語定義）                                   | 解釋文件中會用到的專業術語。                        |
| **Rules of Engagement & Support Agreement**（雙方義務與支持條款）  | 定義雙方技術與行政責任，例如：資源協助、事前溝通流程等。          |
| **Provisions**（補充條款）                                    | 增補或例外事項，如臨時許可、特定通道白名單等。               |
| **Requirements, Restrictions & Authority**（紅隊要求與限制）     | 紅隊操作的具體授權與操作限制（例如不得使用 DoS、不可破壞資料）。    |
| **Ground Rules**（基本限制規則）                                | 明確限制紅隊互動方式，如社工不能打擾實體工作人員。             |
| **Resolution of Issues / Points of Contact**（聯絡窗口與問題處理） | 所有關鍵聯絡人與問題升級機制（客戶聯絡人 / 紅隊指揮官 / 白隊裁判）。 |
| **Authorization**（授權聲明）                                 | 客戶明確授權紅隊執行該 engagement 的聲明。           |
| **Approval**（雙方簽署）                                      | 客戶與紅隊雙方正式簽署同意，具有法律效力。                 |
| **Appendix**（附錄）                                        | 附加補充資訊、圖表、背景資料等。                      |

---

📌 注意事項
- RoE 不是完整行動規劃，而是 **法律框架與合作條件**。
- 真正的技術細節與階段任務會在後續的 **Engagement Plan（行動計畫書）** 中補充。
- 需確保所有條文都具備明確性與可執行性，避免產生解釋歧義。

>> #### Task 4：活動策劃

>> #### Task 5：參與文件

>> #### Task 6：運營概念

>> #### Task 7：資源計劃

>> #### Task 8：運營計劃

>> #### Task 9：任務計劃

>> #### Task 10：結論