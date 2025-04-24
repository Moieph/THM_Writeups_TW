# Linux Fundamentals Part 1 

**🐧 Linux 基礎知識 部分 1**

THM路徑：https://tryhackme.com/room/linuxfundamentalspart1

官方影片：https://youtu.be/kPylihJRG70?si=q3Q65tuVHhAq_FGL

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