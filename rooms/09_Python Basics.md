# Python Basics
**🐍 Pyhon 基礎** 

THM路徑：https://tryhackme.com/room/pythonbasics

---

>> #### Task 1：簡介

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

  - name = "Moe"       （把字串 "Moe" 放進 name 這個變數裡）<br>
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

location = "/Users/moe/Desktop/AAA.txt"
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

<pre>str = "/Users/moe/Desktop/text.txt"
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