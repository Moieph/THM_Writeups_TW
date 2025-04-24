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
   
   在代碼編輯器上，列印 「Hello World」。標誌是什麼？
   
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
   
   在代碼編輯器中，列印 21 + 43 的結果。標誌是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{ADDITI0N}`

2. Print the result of 142 - 52. What is the flag?
   
   列印 142 - 52 的結果。標誌是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{SUBTRCT}`

3. Print the result of 10 * 342. What is the flag?
   
   列印 10 * 342 的結果。標誌是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{MULTIPLICATION_PYTHON}`

4. Print the result of 5 squared. What is the flag?
   
   列印 5 平方的結果。標誌是什麼？
   
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
   
   在另一行新行中，列印出 height 的值。出現的標誌是什麼？
   
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
   
   在代碼編輯器的 shipping.py 選項卡中編寫應用程式後，將出現一個標誌，這是這個問題的答案。
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{IF_STATEMENT_SHOPPING}`

3. In shipping.py, on line 15 (when using the Code Editor's Hint), change the customer_basket_cost variable to 101 and re-run your code. You will get a flag (if the total cost is correct based on your code); the flag is the answer to this question.

    在 shipping.py 中的第 15 行（使用代碼編輯器提示時），將 customer_basket_cost 變數更改為 101 並重新執行代碼。您將收到一個標誌（如果根據您的代碼，總成本是正確的）;FLAG 是這個問題的答案。

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
   
   在代碼編輯器上，按兩下「script.py」選項卡並編寫一個循環，輸出從 0 到 50 的每個數。
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{L00PS_WHILE_FOR}`

>> #### Task 8：功能介紹

>> #### Task 9：檔案處理

>> #### Task 10：匯入


<!--**🐧 Linux 基礎知識 部分 1**

- THM路徑：https://tryhackme.com/room/linuxfundamentalspart1

- 官方影片：https://youtu.be/42u_2e6eNF4?si=5G3x-KfvIMHzU84a

---

>> #### Task 1：介紹

>> #### Task 2：Linux 的背景知識

🐧 Linux 發行版（Flavours）

- 「Linux」不是單一系統，而是統稱一系列 基於 **UNIX** 的作業系統。<br>
- 因為是 **開源**，所以可以根據用途發展出不同版本（大小、功能不一）。

---

常見發行版：

- **Ubuntu、Debian**：用途廣泛，可當伺服器也可當桌面系統  
- 📁 **Ubuntu Server 只需 512MB RAM 就能跑！**

##### 🔐 答題：
1. Research: What year was the first release of a Linux operating system?
   
   研究：Linux 作系統的首次發佈是哪一年？
   
&nbsp;&nbsp;&nbsp;&nbsp; `1991`

>> #### Task 3：與您的第一台 Linux 電腦互動（瀏覽器內）

>> #### Task 4：運行您的前幾個命令

- 基礎指令：

| 指令    | 說明                                     |
|---------|------------------------------------------|
| `echo`  | 輸出你指定的文字（例如：`echo Hello`）   |
| `whoami`| 顯示你目前登入的使用者名稱                |

如果字串中有一個或多個空格，則應使用雙引號將其引起來，例如： `echo "Hello Friend!"`。

##### 🔐 答題：
1. If we wanted to output the text "TryHackMe", what would our command be?
   
   如果我們想輸出文本 「TryHackMe」，我們的命令會是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `echo TryHackMe`

2. What is the username of who you're logged in as on your deployed Linux machine?
   
   您在部署的 Linux 電腦上登錄的使用者的使用者名是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `tryhackme`

>> #### Task 5：與檔案系統交互！

| 指令     | 全名（Full Name）         | 中文說明                                    |
|----------|----------------------------|---------------------------------------------|
| `ls`     | **listing**                | 列出目前目錄下的檔案與資料夾               |
| `cd`     | **change directory**       | 切換目錄（例如： `cd /home/user`）         |
| `cat`    | **concatenate**            | 查看檔案內容、串接檔案內容                  |
| `pwd`    | **print working directory**| 顯示目前所在的路徑位置                      |

<p align="left">
  <img src="/rooms/images/08_01.png" width="600">
</p>

##### 🔐 答題：
1. On the Linux machine that you deploy, how many folders are there?
   
   在您部署的 Linux 電腦上，有多少個資料夾？
   
&nbsp;&nbsp;&nbsp;&nbsp; `4`

2. Which directory contains a file? 
   
   哪個目錄包含檔？
   
&nbsp;&nbsp;&nbsp;&nbsp; `folder4`

3. What is the contents of this file?
   
   這個文件的內容是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `Hello World`

4. Use the cd command to navigate to this file and find out the new current working directory. What is the path?
   
   使用 cd 命令導航到此檔案並找出新的當前工作目錄。路徑是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `/home/tryhackme/folder4`

>> #### Task 6：搜尋檔案
> 
| 指令 | 功能說明 | 常用情境 |
|------|---------|----------|
| `find` | 找檔案（依名稱、類型等） | 找某個檔案藏在哪裡 |
| `grep` | 找內容（看誰含有某關鍵字） | 搜某段文字在哪個檔案裡出現了 |


`find . -name "*.txt"` <br>在目前資料夾 (.) 下，找出所有 .txt 結尾的檔案

`find / -name "*.txt"` <br>在根目錄 (/) 下，找出所有 .txt 結尾的檔案

---

`grep "password" config.txt` <br> 在 config.txt 裡找出包含「password」的那幾行

---

wc 計算：

| 指令範例 | 功能 |
|---------|------|
| `wc -l file.txt` | 只顯示行數 (line) |
| `wc -w file.txt` | 只顯示字數 (word) |
| `wc -c file.txt` | 只顯示位元組 (byte 數) |
| `wc -m file.txt` | 顯示字元數 (character)<br>👉 特別適合中文或 UTF-8 |

<p align="left">
  <img src="/rooms/images/08_02.png" width="600">
</p>

##### 🔐 答題：
1. Use grep on "access.log" to find the flag that has a prefix of "THM". What is the flag? Note: The "access.log" file is located in the "/home/tryhackme/" directory.
   
   對 「access.log」 使用 grep 可查找前綴為 「THM」 的標誌。標誌是什麼？ 注意：“access.log” 檔案位於 “/home/tryhackme/” 目錄中。
   
&nbsp;&nbsp;&nbsp;&nbsp; `THM{ACCESS}`

>> #### Task 7：Shell 運算符簡介
> 
| 運算符 | 功能說明                           | 備註                           |
|--------|------------------------------------|--------------------------------|
| `&`    | 在背景執行指令                     | 可同時做其他事                 |
| `&&`   | 串接多個指令，**前一個成功才執行下一個** | 具「依序且條件成立才執行」的效果 |
| `>`    | 輸出導向（覆蓋檔案內容）           | 建立或覆寫檔案                 |
| `>>`   | 輸出導向（追加內容至檔案末端）     | 不會覆蓋，只會往後加內容       |

`echo "hello" > greet.txt` <br>建立 greet.txt 並寫入 "hello"（若已有檔案會整個覆蓋）

`echo "world" >> greet.txt` <br>把 "world" 加到檔案 greet.txt 的末尾

##### 🔐 答題：
1. If we wanted to run a command in the background, what operator would we want to use?
   
   如果我們想在後台運行命令，我們想使用什麼運算符？
   
&nbsp;&nbsp;&nbsp;&nbsp; `&`

2. If I wanted to replace the contents of a file named "passwords" with the word "password123", what would my command be?
   
   如果我想用單詞 「password123」 替換名為 「passwords」 的文件的內容，我的命令是什麼？
   
&nbsp;&nbsp;&nbsp;&nbsp; `echo password123 > passwords`

3. Now if I wanted to add "tryhackme" to this file named "passwords" but also keep "passwords123", what would my command be
   
   現在，如果我想將 「tryhackme」 添加到名為 「passwords」 的檔中，但同時保留 「passwords123」，我的命令會是什麼
   
&nbsp;&nbsp;&nbsp;&nbsp; `echo tryhackme >> passwords`