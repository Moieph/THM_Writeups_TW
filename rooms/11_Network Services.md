# Network Services

**🌐 網路服務**

THM路徑：https://tryhackme.com/room/networkservices

---

>> #### Task 1：建立聯繫

>> #### Task 2：瞭解 SMB

<details>
<summary><strong>伺服器訊息塊協定（SMB）</strong></summary>

- Server Message Block<br><strong>是一種用來在網路中分享資源的通訊協定</strong>

✅ 功能包括：
- 檔案共享（File Sharing）
- 印表機共享（Printer Sharing）
- 存取串列埠（Serial Port）
- 管道與 API 存取（Named Pipes / APIs）

---

SMB 讓「用戶端」能從遠端「像操作本機一樣」存取伺服器上的資源
</details>

<details>
<summary><strong>SMB 運作方式</strong></summary>

- SMB 是一種「**請求-回應協定**（Response-Request Protocol）」
- 用戶端（Client）和伺服器（Server）透過多次訊息互動建立連線
- 通訊協定底層可透過：
  - TCP/IP（最常見，含 NetBIOS over TCP/IP）
  - NetBEUI（較舊）
  - IPX/SPX（較罕見）

---

建立連線後，用戶端可以：

- 開啟遠端共享資料夾
- 閱讀 / 寫入檔案
- 操作共享印表機或資源
- 像使用自己電腦一樣操作伺服器資源（但是在網路上完成的！）

</details>


<details>
<summary><strong> 💻 誰在使用 SMB？</strong></summary>

| 作業系統 / 工具 | 說明 |
|----------------|------|
| **Windows**    | 從 Windows 95 開始即內建 SMB 支援 |
| **Samba**      | 開源實作，讓 Linux/Unix 也能支援 SMB 協定（可當成 SMB 伺服器） |

🧠 延伸知識

- SMB 也常見於內網滲透測試中，如利用漏洞進行：
    - SMB Relay 攻擊
    - 未授權存取共享資料夾
    - 利用弱密碼登入取得資料
- 知名漏洞：EternalBlue（MS17-010） 針對 SMB

##### 🔐 答題：
1. What does SMB stand for?  
   
   SMB 代表什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Server Message Block`

2. What type of protocol is SMB?
   
   SMB 是什麼類型的協定？
   
&nbsp;&nbsp;&nbsp;&nbsp; `response-request`

3. What protocol suite do clients use to connect to the server?    
   
   用戶端使用什麼協定套件連接到伺服器？
   
&nbsp;&nbsp;&nbsp;&nbsp; `TCP/IP`

4. What systems does Samba run on? 
   
   Samba 可以在哪些系統上運行？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Unix`

>> #### Task 3：枚舉 SMB

- `nmap` ：掃描網路開放的服務與主機

| 功能             | 指令                                      | 解說                             |
|------------------|-------------------------------------------|----------------------------------|
| 探測主機是否在線 | `nmap -sn 192.168.1.0/24`                 | 只 Ping 掃，不掃 port（-sn = --sP） |
| 快速掃描常見 port | `nmap <IP>`                               | 掃描 1000 個常見 port             |
| 全 Port 掃描     | `nmap -p- <IP>`                            | 掃 0~65535 所有 port              |
| 指定 Port        | `nmap -p 22,80,443 <IP>`                  | 只掃特定 port                     |
| 指定 Port        | `nmap -sV -p 21 <IP>`                     | 掃描特定 port 的版本              |


- `enum4linux` ：枚舉（列舉）Windows SMB 資訊

| 參數 | 功能說明 |
|------|----------|
| `-U` | 獲取使用者清單（User list） |
| `-M` | 獲取機器名稱清單（Machine list） |
| `-N` | 傾印名稱清單（Name list dump，與 `-U`、`-M` 不同） |
| `-S` | 獲取共享資源清單（Share list） |
| `-P` | 顯示密碼政策資訊（Password policy） |
| `-G` | 顯示群組與成員清單（Group + Members） |
| `-a` | 執行以上所有功能（全自動基本列舉） |


---

Question 1、2：對靶機執行`nmap`掃描，找到 3 個 Port 和 SMB 在哪個 Port 上運行

<p align="left">
  <img src="/rooms/images/11_01.png" width="600">
</p>

Question 3：對靶機執行`enum4linux`，枚舉靶機的 SMB 資訊，得到工作群組名稱
<p align="left">
  <img src="/rooms/images/11_02.png" width="600">
</p>

Question 4：在 NetBIOS Name Table 中，機器的名稱會出現在 `00`、`03`、`20` 

- `<00>`  Workstation Service（工作站服務名稱）<br>→ 通常代表主機名稱
- `<03>` Messenger Service（訊息傳遞）
- `<20>`  File Server Service（檔案分享服務）<br>→ 檔案伺服器名稱

<p align="left">
  <img src="/rooms/images/11_03.png" width="600">
</p>

Question 5：查看系統版本
<p align="left">
  <img src="/rooms/images/11_04.png" width="600">
</p>

Question 6：靶機允許匿名登錄 <br>
`username''`、`password''`

`//10.10.42.205/profiles Mapping: OK, Listing: OK`<br>
- 「Mapping」= 允許掛載（連線）到該 SMB 分享
- 「Listing」= 允許列出該分享資料夾的檔案與內容

<p align="left">
  <img src="/rooms/images/11_05.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/11_06.png" width="600">
</p>

##### 🔐 答題：
1. Conduct an nmap scan of your choosing, How many ports are open?
   
    執行您選擇的 nmap 掃描，打開了多少個埠？
   
&nbsp;&nbsp;&nbsp;&nbsp; `3`

2. What ports is SMB running on? Provide the ports in ascending order.
   
    SMB 在哪些埠上運行？按升序提供埠。
   
&nbsp;&nbsp;&nbsp;&nbsp; `139/445`

3. Let's get started with Enum4Linux, conduct a full basic enumeration. For starters, what is the workgroup name?    
   
    讓我們從 Enum4Linux 開始，進行一個完整的基本枚舉。工作群組名稱是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `WORKGROUP`

4. What comes up as the name of the machine? 
   
    機器的名稱是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `POLOSMB`

5. What operating system version is running?    
   
    運行的是什麼作系統版本 ？
   
&nbsp;&nbsp;&nbsp;&nbsp; `6.1`

6. What share sticks out as something we might want to investigate?    
   
    哪些分享資料夾值得我們調查？
   
&nbsp;&nbsp;&nbsp;&nbsp; `profiles`

>> #### Task 4：利用 SMB

`smbclient`： 連接 SMB 分享的命令列工具

`smbclient //[IP]/[SHARE] -User -Port`


>> #### Task 5：瞭解 Telnet

>> #### Task 6：枚舉 Telnet

>> #### Task 7：利用 Telnet

>> #### Task 8：瞭解 FTP

>> #### Task 9：枚舉 FTP

>> #### Task 11：利用 FTP


<!--**🐍 Pyhon 基礎** 







>> #### Task 2：Hello World

`print("想輸入的字符")` 

<p align="left">
  <img src="/rooms/images/09_01.png" width="600">
</p>

##### 🔐 答題：
1. On the code editor, print "Hello World". What is the flag?
   
   在代碼編輯器上，列印 「Hello World」。旗子是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{PRINT_STATEMENTS}`

>> #### Task 3：數學運算符

| 算法名稱     | 語法   | 範例說明              |
|--------------|--------|-----------------------|
| 加法         | `+`    | 1 + 1 = 2             |
| 減法         | `-`    | 5 - 1 = 4             |
| 乘法         | `*`    | 10 * 10 = 100         |
| 除法         | `/`    | 10 / 2 = 5            |
| 餘數（取餘） | `%`    | 10 % 2 = 0            |
| 次方（指數） | `**`   | 5**2 = 25（5 的平方） |

---
| 比較意思         | 語法 |
|------------------|------|
| 大於             | `>`  |
| 小於             | `<`  |
| 等於             | `==` |
| 不等於           | `!=` |
| 大於或等於       | `>=` |
| 小於或等於       | `<=` |

<p align="left">
  <img src="/rooms/images/09_02.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/09_03.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/09_04.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/09_05.png" width="600">
</p>

##### 🔐 答題：
1. In the code editor, print the result of 21 + 43. What is the flag?
   
   在代碼編輯器中，列印 21 + 43 的結果。旗子是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{ADDITI0N}`

2. Print the result of 142 - 52. What is the flag?
   
   列印 142 - 52 的結果。旗子是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{SUBTRCT}`

3. Print the result of 10 * 342. What is the flag?
   
   列印 10 * 342 的結果。旗子是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{MULTIPLICATION_PYTHON}`

4. Print the result of 5 squared. What is the flag?
   
   列印 5 平方的結果。旗子是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{EXP0N3NT_POWER}`

>> #### Task 4：變數與資料型別


變數 = 幫資料取個名字！
你可以把變數想成「資料的盒子」，你給它一個名字，放進你想記住的東西。


- 📦 例子：

  - name = "Moieph"       （把字串 "Moieph" 放進 name 這個變數裡）<br>
  - age = 28           （把數字 28 放進 age 裡）<br>
  - is_hungry = True   （把布林值 True 放進 is_hungry 裡）<br>


---

📚 資料型別簡易筆記：

- **String（字串）**  
  就是文字！像名字、書名、任何一段話。必須加引號！  
  例如： `"Hello"`、`'Python'`、`"123"`（雖然是數字，但因為有引號，還是字串）


- **Integer（整數）**  
  純數字，沒有小數點。拿來計算次數或年齡都可以。  
  例如： `10`、`-5`、`0`


- **Float（浮點數）**  
  小數點數字，能表示比較精細的數值。  
  例如： `3.14`、`0.5`、`-100.01`


- **Boolean（布林值）**  
  只有兩種結果：「True（真）」或「False（假）」，常用來做判斷。  
  例如： `True`、`False`


- **List（串列）**  
  像一個袋子可以裝很多東西，而且順序會被記住。可以裝數字、字串、甚至其他 list！  
  例如： `[1, 2, 3]`、`["apple", "banana"]`、`[True, 3.14, "yes"]`

| String        | Float | Integer | Boolean | List          |
|---------------|-------|---------|---------|---------------|
| "Star Wars"    | 9.8   | 13      | True    | ["Alice", "Bob" ] |
| "Matrix"       | 8.5   | 23      | False   | ["Charlie"]     |
| "Indiana Jones" | 6.1   | 3       | False   | ["Daniel", "Evie"] |


<p align="left">
  <img src="/rooms/images/09_06.png" width="600">
</p>

##### 🔐 答題：
3. On another new line, print out the value of height. What is the flag that appears?
   
   在另一行新行中，列印出 height 的值。出現的旗子是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{VARIABL3S}`

>> #### Task 5：邏輯運算符及布林值

| Logical Operation 邏輯運算         | Operator 運算子 | Example 例子           |
|--------------------------------|-------------|----------------------|
|  等於                 | `==`        | if x == 5   |
|  小於                   | `<`         | if x < 5   |
|  小於或等於    | `<=`        | if x <= 5  |
|  大於                | `>=`        | if x > 5   |
|  大於或等於 | `>=`        | if x >= 5   |

---

| Boolean Operation 布林運算說                               | Operator 算子 | Example 例                                                              |
|-------------------------------------------------------|----------------|-------------------------------------------------------------------------|
| 兩個條件都要為 true         | AND            | if x >= 5 AND x <= 100 <br>如果 x 是介於 5 和 100 之間，則回傳 TRUE      |
| 其中一個條件為 true 即可 | OR             | if x == 1 OR x == 10 <br>如果 x 為 1 或 10，則回傳 TRUE                 |
| 條件相反                        | NOT            | if NOT y <br>如果 y 為 False，則回傳 TRUE                              |

>> #### Task 6：IF 語句

🔹 `if`：如果…就…
<pre>age = 18

if age >= 18:
    print("你是成年人")  </pre>

👉 如果條件成立，就執行縮排內的程式。

---

🔹 elif：否則如果…就…

<pre>score = 85

if score >= 90:
    print("優等")
elif score >= 60:
    print("及格")</pre>

👉 elif 是 「否則如果」，可接續判斷其他條件。

---

🔹else：以上都不符合時…

<pre>score = 50

if score >= 90:
    print("優等")
elif score >= 60:
    print("及格")
else:
    print("不及格")</pre>

👉 else 不用寫條件，當上面條件都不成立時執行。

---
- if → 如果成立，就做
- elif → 再檢查下一個可能
- else → 都不是，就做這個

---
請寫一段程式，根據以下條件計算顧客的總金額：

- 如果購物金額超過 100 元，則免運費  
- 如果低於 100 元，則每公斤運費為 1.2 元
- 最後請印出 總金額（含運費）

<p align="left">
  <img src="/rooms/images/09_07.png" width="600">
</p>

將 customer_basket_cost 改成 101 ： 

<p align="left">
  <img src="/rooms/images/09_08.png" width="600">
</p>


##### 🔐 答題：
2. Once you've written the application in the code editor's shipping.py tab, a flag will appear, which is the answer to this question.
   
   在代碼編輯器的 shipping.py 選項卡中編寫應用程式後，將出現一個旗子，這是這個問題的答案。
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{IF_STATEMENT_SHOPPING}`

3. In shipping.py, on line 15 (when using the Code Editor's Hint), change the customer_basket_cost variable to 101 and re-run your code. You will get a flag (if the total cost is correct based on your code); the flag is the answer to this question.

    在 shipping.py 中的第 15 行（使用代碼編輯器提示時），將 customer_basket_cost 變數更改為 101 並重新執行代碼。您將收到一個旗子（如果根據您的代碼，總成本是正確的）FLAG 是這個問題的答案。

&nbsp;&nbsp;&nbsp;&nbsp; `THM{MY_FIRST_APP}`


>> #### Task 7：Loops 迴圈

1. `while` 迴圈：當條件為 True 就會一直跑（直到變 False）

<pre>i = 1
while i <= 10:
    print(i)
    i = i + 1</pre>

2. `for...in` 迴圈（跑清單）
<pre>websites = ["facebook.com", "google.com", "amazon.com"]
for site in websites:
    print(site)</pre>

3. `for...in range()` 迴圈（跑固定次數）
<pre>for i in range(5):
    print(i)</pre>
👉 從 0 開始跑到 4（不包含 5），共跑 5 次。

---

逐一輸出數字 0 - 50： 

<p align="left">
  <img src="/rooms/images/09_09.png" width="600">
</p>

##### 🔐 答題：
1. On the code editor, click back on the "script.py" tab and code a loop that outputs every number from 0 to 50.
   
   在代碼編輯器上，按兩下「script.py」專案並編寫一個循環，輸出從 0 到 50 的每個數。
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{L00PS_WHILE_FOR}`

>> #### Task 8：函數介紹

`def `：定義函式（function）的關鍵字，函式是 一組可重複使用的程式碼

<pre>def greet(name):  # name 是參數
    print("你好" + {name})

greet("Ben")
greet("Tom")</pre>

---

<pre>def calcCost(item):
     if(item == "sweets"):
          return 3.99
     elif (item == "oranges"):
          return 1.99
     else:
          return 0.99

spent = 10
spent = spent + calcCost("sweets")
print("You have spent:" + str(spent))</pre>

---

請建立一個名為 bitcoinToUSD 的函式，接收兩個參數：
擁有的比特幣數量（bitcoin_amount） 、每顆比特幣的美元價格（bitcoin_value_usd）

- 函式要回傳你目前比特幣的總價值（美元）
- 使用函式來計算比特幣總價值
- 如果低於 30,000 美元，請印出提醒訊息

<p align="left">
  <img src="/rooms/images/09_10.png" width="600">
</p>

<p align="left">
  <img src="/rooms/images/09_11.png" width="600">
</p>

##### 🔐 答題：
1. Once you've written the bitcoinToUSD function, use it to calculate the value of your Bitcoin in USD, and then create an if statement to determine if the value falls below $30,000; if it does, output a message to alert you (via a print statement).
   
   編寫 bitcoinToUSD 函數後，使用它來計算比特幣的美元價值，然後創建一個 if 語句來確定該值是否低於 30,000 美元;如果是這樣，則輸出一條消息以提醒您（通過 print 語句）。

&nbsp;&nbsp;&nbsp;&nbsp; `THM{BITC0IN_INVESTOR}`

>> #### Task 9：檔案處理
`with open(路徑,'w',encoding="utf-8")as file:`<br>
`'w'` → 寫入模式（write mode）<br>
預設` encoding="utf-8"` → 能處理中文或特殊字元

---
`file.write(內容) `： 將 text 變數的內容寫入檔案

<pre># 寫入檔案

location = "/Users/moieph/Desktop/AAA.txt"
text = ("哈哈是我啦")

# write

with open(location,'w') as file:
    file.write(text) </pre>

| 模式   | 說明                             |
|--------|----------------------------------|
| `"w"`  | 寫入模式，如果檔案存在，**清空內容再寫入** |
| `"a"`  | **追加模式**，寫入時不會覆蓋原內容         |
| `"w+"` | 讀寫模式，先清空再寫入，可讀取內容         |
| `"a+"` | 讀寫追加模式，不清空，可讀取內容          |
| `"wb"` | **寫入二進位檔案**（二進位）               |

---
`file.read()` ：讀取檔案內容

<pre>str = "/Users/moieph/Desktop/text.txt"
with open(str) as file:
    print(file.read())</pre>

<p align="left">
  <img src="/rooms/images/09_12.png" width="600">
</p>

##### 🔐 答題：
1. In the code editor, write Python code to read the flag.txt file. What is the flag in this file?
   
   在代碼編輯器中，編寫 Python 代碼以讀取 flag.txt 檔。此檔中的標誌是什麼？

&nbsp;&nbsp;&nbsp;&nbsp; `THM{F1LE_R3AD}`

>> #### Task 10：匯入

Library（函式庫）：就是別人寫好的功能集合，我們可以直接拿來用，不用自己從頭寫。

- 匯入方式：用 import 關鍵字引入，例如：
<pre>import datetime
current_time = datetime.datetime.now()
print(current_time)</pre>

- 語法格式為：<br>
library_name.function_name()
（先叫出庫，再叫出裡面的功能）

---
常見的實用函式庫：
1. requests：發送 HTTP 請求
2. scapy：封包製作、封包分析
3. pwntools	：CTF / 漏洞利用開發常用工具庫