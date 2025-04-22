# What is Networking?  
**🌐 什麼是網路？**

THM路徑：https://tryhackme.com/room/whatisnetworking 

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
   
&nbsp;&nbsp;&nbsp;&nbsp; `Tim Berners-Lee`

> #### Task 3：識別網路上的設備

設備識別：IP 位址（可更改） MAC 位址（不可更改）

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

IPv4：最多約 42 億個位址，逐漸用完<br>
IPv6：可用位址達 340 兆兆兆（2¹²⁸），解決位址不足問題

</details>

<details>
<summary> MAC 位址（Media Access Control）唯一且固定</summary>
&nbsp;

- 類似「指紋」，出廠時寫死在網卡上，格式如：a4:c3:f0:85:ac:2d

<hr>
MAC 偽裝（MAC Spoofing）

- MAC 可被偽造，造成安全風險

- 若防火牆僅依 MAC 判斷是否放行，容易被冒用<br>

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

> #### Task 4：識別網路上的設備