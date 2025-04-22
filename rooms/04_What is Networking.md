# What is Networking?  
**什麼是網路？**

THM路徑：https://tryhackme.com/room/whatisnetworking <br>
官方影片：https://youtu.be/42u_2e6eNF4?si=5G3x-KfvIMHzU84a
> #### Task 1：什麼是網路？
##### 🔐 答題：
1. What is the key term for devices that are connected together?
   
    連接在一起的設備的關鍵術語是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Network`

> #### Task 2：什麼是互聯網？

**互聯網（Internet）是一個由許多小型網路（Private Network）組成的公用網路（Public Network）**

##### 🔐 答題：
1. Who invented the World Wide Web?
   
   誰發明全球資訊網？
   
&nbsp;&nbsp;&nbsp;&nbsp; `
Tim Berners-Lee `
> #### Task 3：識別網路上的設備

設備識別：IP 位址（Ｏ更改）、 MAC 位址（Ｘ更改）

為了能在網路中通訊，設備必須能被辨識，就像人有名字與指紋一樣。

<details>
<summary> IP （Internet Protocol）位址：</summary>
&nbsp;
<p align="left">
  <img src="/rooms/images/04_01.png" width="600">
</p>

1. 類似「名字」，可更改
2. 每台設備在網路中都有一組 IP 位址 

- 分為：
  - 私人 IP：在內部網路中使用，如 192.168.x.x
  - 公共 IP：與外部網路通訊時使用，由 ISP 分配
    - 公共 IP 可共用（如多台設備透過一個路由器上網）
<hr>
IPv4 vs IPv6：

IPv4：最多約 42 億個位址，逐漸用完<br>
IPv6：可用位址達 340 兆兆兆（2¹²⁸），解決位址不足問題

</details>

> #### Task 4：事件響應人員（Incident responder）
&nbsp;&nbsp;&nbsp;&nbsp;_負責應對資安事件，制定計劃、即時反應、降低損害，守護公司資料與聲譽_ <br>

- 主要職責：
1. 制定可執行的事件回應計劃
2. 落實安全最佳實務、即時支援事件處理 
3. 撰寫事件報告、吸取教訓，強化未來防禦

- 關鍵指標：
  - MTTD（偵測時間）
  - MTTA（確認時間）
  - MTTR（恢復時間）

> #### Task 5：數位取證審查員（Digital Forensics Examiner）
&nbsp;&nbsp;&nbsp;&nbsp;_透過數位證據揭露真相。可應用於執法或企業資安領域_ <br>

- 主要職責：
1. 遵循法律程序收集數位證據 
2. 分析證據，找出與事件相關的線索 
3. 紀錄發現並撰寫報告

> #### Task 6：惡意軟體分析師（Malware Analyst）
&nbsp;&nbsp;&nbsp;&nbsp;_負責分析可疑程式，找出其行為與功能，有時也稱為「逆向工程師」_<br>

- 主要職責：
1. 執行靜態分析，逆向工程惡意程式碼
2. 在沙箱中觀察程式行為，進行動態分析
3. 撰寫分析報告，紀錄所有發現

📌 需具備彙編語言、C 語言等低階程式能力。

> #### Task 7：滲透測試員（Penetration Tester）
&nbsp;&nbsp;&nbsp;&nbsp;_透過模擬駭客攻擊測試系統安全，找出漏洞並協助企業修補_<br>

- 主要職責：
1. 測試系統、網路與網路應用的安全性 
2. 執行安全評估與政策審查 
3. 撰寫報告，提出防禦建議

> #### Task 8：紅隊成員（Red Teamer）
&nbsp;&nbsp;&nbsp;&nbsp;_模擬真實攻擊者行為，測試組織的偵測與回應能力，進行深入持續 性攻擊評估_<br>

- 主要職責：
1. 假扮攻擊者，挖掘漏洞、維持存取權限、避開偵測
2. 測試組織的安全防禦與事件回應流程
3. 撰寫報告，提供可行建議以提升真實攻擊防禦力