# 【Git 學習筆記-基本指令】

# **§ Git 工具安裝 §**

- [Git For Windows](https://git-scm.com/)

# **§ Git 基本設定 §**

※ `git config --help` 完整指令說明

### Git 執行環境中，三個層級差異

- 系統層級
    - System-Level Configuration：整台電腦所有使用者

        ```go
        git config --system --list
        ```

        - 預設路徑：C:\Program Files\Git\etc\gitconfig

            ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled.png)

- 使用者層級
    - User-Level Configuration：當前登入的使用者

        ```go
        git config --global --list
        ```

        - 預設路徑：C:\Users\<使用者帳號>admin\.gitconfig

            ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%201.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%201.png)

        - 常用指令：
            - user區段下的name & email參數，初次使用Git一定要設定。

                ```go
                git config --global user.name "Eli"
                git config --global user.email "eli@uisco.com.tw"
                ```

            - Windows環境中，開啟 core.autocrlf選項，讓commit 的檔案沒有CR字元。

                ※純Windows開發環境，可以設定為False;跨平台建議設定為True

                ```go
                git config --global core.autocrlf true
                ```

            - 自動訂正打錯的參數

                ex:git statsu —> git status

                ```go
                git config --global help.autocorrect 1
                ```

- 儲存區層級
    - Repository-Level Configuration：

        ```go
        git config --list
        ```

        - 預設路徑：<Git儲存區>UISCO_Eli\.git\config

            ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%202.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%202.png)

### **Git 執行環境中，層級套用順序**

- **儲存區層級** (優先權最高) > **使用者層級** > **系統層級** (優先權最低) ****
- 刪除特定選項的值 (從設定檔中刪除)：

    ```go
    git config --unset user.email             (刪除**儲存區層級**的設定值)
    git config --global --unset user.email    (刪除**使用者層級**的設定值**)**
    ```

- 直接至檔案更改值：
    - **系統層級**預設路徑：C:\Program Files\Git\etc\gitconfig
    - **使用者層級**預設路徑：C:\Users\<使用者帳號>admin\.gitconfig
    - **儲存區層級**預設路徑：<Git儲存區>UISCO_Eli\.git\config

# **§ Git 版本控管工具(指令) §**

### 取得 **Git 軟體版本**

- 查看當前Git使用的版本。

    ```go
    git --version
    ```

### 建立 **Git 本地儲存區(Local Repositiry) (**初始化Git目錄**)**

- 所有儲存區檔案(repository files)都在存於【.git】目錄下。

    ```go
    git init
    ```

### 取得 **Git 工作目錄狀態**

- 取得當前版本控制狀態，檔案的新增、刪除、變更...ect。

    ```go
    git status
    ```

### 新增檔案使 Git 追蹤

- 將檔案加入追蹤但並未推送至 GitHub。

    ```go
    git add .               // 將所有Untracked files加入 Git清單
    git add <FILENAME.>     // 將指定檔案加入 Git清單
    ```

- 若新增一個檔案(aaa.txt)，執行 `git status`會得到以下畫面：

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%203.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%203.png)

- 接著執行 `git add.`後，得到以下畫面：

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%204.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%204.png)

### 提交變更使 **Git 送至 儲存區(Repository)**

- 當提交變更時，一定要寫下紀錄訊息。

    ```go
    git commit
    git commit -m "<版本記錄訊息>"
    ```

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%205.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%205.png)

### 查看**歷史紀錄**

- 當查詢紀錄時，重要欄位如下：

    ```go
    git log
    ```

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%206.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%206.png)

    - 【commit】：亂碼(SHA1 Hash)，每個版本唯一值。
    - 【Author】：此字提交之user.name & user.email
    - 【Date】：提交該版本之時間資訊
    - 【訊息】：提交該版本的`commit -m "紀錄訊息內容"`
- 詳細顯示新增的檔案、新增與刪除的行數...ect。

    ```go
    git log --stat
    ```

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%207.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%207.png)

- 簡略顯示每次版本更新之內容：

    ```go
    git log --pretty=oneline
    ```

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%208.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%208.png)

### 更新檔案

- 當加上 `-u` 參數時，將已經在追蹤的檔案有變更時再次提交追蹤。

    ```go
    git add -u
    ```

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%209.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%209.png)

### 刪除檔案

- 直接刪除

    先刪除檔案後，透過 `git add -u` 指令再將已追蹤的該檔案刪除。

    ```go
    rm <FILENAME>
    git add -u <FILENAME>
    ```

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2010.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2010.png)

- 利用 Git 指令刪除

    省去兩步驟將檔案刪除。

    ```go
    git rm <FILENAME>
    ```

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2011.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2011.png)

### 重置檔案狀態

- 取消該檔案追蹤。

    ```go
    git reset HEAD [<path\FILENAME>]
    ```

    註：【HEAD】代表目前版本庫中的最新版本，當執行 `git reset HEAD` 時，會重置檔案為HEAD版本時的狀態，所以HEAD之後的變更都會成為 **not staged** 或 **untracked**。但重置動作不會改變檔案內容。

### 復原檔案變更(Undo Changes)

- 當修改工作目錄中的檔案，若該檔案還為"**not staged**"狀態，則可以讓上一個版本的內容蓋掉這個檔案的內容。

    若已被標示為"**staged**"(透過 `git add .`)，必須先執行 `git reset HEAD` 才能回復為"**not stage**"狀態。

    ```go
    git checkout -- .
    git checkout --  <FILENAME>
    ```

    註：--為HEAD之縮寫。

### 清除未追蹤的檔案

- 自動清除未受追蹤的檔案。

    ```go
    git clean
    git clean -n   // 列出耀清空的檔案清單
    git clean -f   // 執行清除動作，將要清理的檔案逐一刪除 
    ```

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2012.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2012.png)

### 同時有檔案新增、檔案變更之控制

- 假設【變更 aaa.txt】且【新增 bbb.txt】，當執行 `git status` 時：

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2013.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2013.png)

    【not staged】：aaa.txt

    【Untracked】 ：bbb.txt

- 若想一次將【變更檔案】、【新增檔案】加入追蹤則使用 `git add .`

    兩個檔案皆呈現綠色字樣

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2014.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2014.png)

- 只想將【變更檔案】加入追蹤則使用 `git add -u`

    僅變更檔案呈現綠色字樣

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2015.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2015.png)

- 只想將【新增檔案】加入追蹤則使用 `git add bbb.txt`

    僅新增檔案呈現綠色字樣

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2016.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2016.png)

- 若想將剛剛所有加入追蹤之執行取消則使用 `gut reser HEAD`

    會顯示取消變動之項目並呈現紅色字樣

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2017.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2017.png)

- 若想將 bbb.txt 重置回Untracked狀態則使用 `git reset HEAD b.txt`

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2018.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2018.png)

- 若講將已aaa為名的所有檔案都重置則使用 `git reset HEAD aaa.*`

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2019.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2019.png)

- 若想取消aaa.txt所有變更之內容，回復到原本版本庫中之內容則使用 `git checkout --aaa.txt`

    註：檔案中新增的內容會一並移除

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2020.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2020.png)

---

### **總結上述內容**

- 【**staged**】：該檔案可以使用 `git commit` 會納入版本庫中
- 【**not staged**】：該檔案有變更但使用 `git commit` 不會納入版本庫中
- 【**untracked**】：該檔案尚未被追蹤，所以使用 `git commit` 也不會被納入
- `**git add .`** ：將所有檔案(新增或變更)標示，若使用 `git commit` 時會納入
- **`git reset HEAD`** ：取消所有檔案的標示
- **`git status`** ：檢查該工作目錄之檔案狀態
- **`git add -u .`** ：僅標示「變更」的檔案(曾被tracked過的)
- **`git commit`** ：將標示的檔案提交版本庫(需留下紀錄訊息)
- **`git log`** ：查看版本歷史紀錄
- **HEAD版本**之後的變更全部回復：`git reset HEAD` or `git checkout -- <FILENAME>` (差異見上文)

---

### 查看不同版本之間的變更比較

- 基本指令
    1. 比對 **工作目錄** 與 **尚未進入暫存區(unstaged)** 全部檔案差異

        ```go
        git diff
        ```

        ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2021.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2021.png)

    2. 比對 **工作目錄** 與 **已加入暫存區(staged)** 全部檔案差異

        註：若變更檔案以使用 `git add` 許加上 `--cached`，否則找無資料。

        ```go
        git diff --cached
        ```

        ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2022.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2022.png)

    3. 比對 **工作目錄** 與 **尚未進入暫存區** <filename>檔案差異

        ```go
        git diff <filename>
        ```

    4. 比對 **所在分支的<COMMIT-ID>** 與 **HEAD版** 差異

        ```go
        git diff <commit-id>
        ```

        ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2023.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2023.png)

    5. 比對 **兩版本之間(<commit-id>)** 差異

        ```go
        git diff <old commit-id> <new commit-id>
        ```

        ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2024.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2024.png)

    6. 比對 兩分支之間(<branches>) 差異 

        註：中間加入[..]避免檔案名稱跟分支名稱重複

        ```go
        git diff <branch 1>..<branch 2>
        ```

- 補充指令
    1. 比較 **版控中的倒數第二版**(**HEAD~1**/**HEAD^**) 與 **版控中的最新版(HEAD)** 差異

        **註**：HEAD代表最新版，HEAD~1代表最新版的前一版。

        ```go
        git diff HEAD~1..HEAD
        git diff HEAD^..HEAD
        ```

        ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2025.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2025.png)

    2. 檢視更新(簡略資訊)

        ```go
        git diff ---stat
        ```

        ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2026.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2026.png)

    3. 顯示 **更動檔案名稱列表** 於更新訊息後方

        ```go
        git diff --name-only
        ```

        ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2027.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2027.png)

    4. 顯示 **新增、刪除、變更的檔案列表**

        ```go
        git diff --name-status
        ```

        ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2028.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2028.png)

    5. 顯示 **檔案列表(依照檔案狀態)**

        ```go
        git diff --diff-filter= []
        A = added
        C = copied
        M = modified
        R = renamed
        T = changed
        D = delet
        ```

- 將差異以文件匯出
    - 將比對差異以【.txt】檔顯示，可配合補充指令。

        ```go
        git diff > *.txt
        ```

        ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2029.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2029.png)

    - 將 **<commit-id>** 與 **HEAD** 差異以【壓縮檔】輸出。

        ```go
        git archive --format=zip -output=*.zip HEAD $(git diff --name-only [commit-id] HEAD)
        ```

### 變更檔名

- 直接改名

    利用 `git status` 查詢時會有兩筆狀態改變，在使用 `git add .` 加入暫存區。

    若只有更改名稱沒有對內容進行變更 `git status` 則會顯示 `rename`。

    ```go
    mv <FILENAME> <新名稱>
    git add .
    ```

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2030.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2030.png)

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2031.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2031.png)

- 利用 Git 指令修改

    免去兩步驟的更名直接一步完成檔名變更

    ```go
    git mv <FILENAME> <新名稱>
    ```

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2032.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2032.png)

### 重新提交版本

- 當執行完`git commit`後發現遺漏檔案、紀錄訊息錯誤時，新增`--amend`參數可以重新提交一次版本

    ```go
    git commit --amend
    ```

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2033.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2033.png)

    ![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2034.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2034.png)

    **註**：版本數量、時間沒有變動，但commit 的內容作出了改變。

### 復原操作過程中的所有變更

- 在 Git 中所做的所有操作指令皆會留存於版本庫中，所有指令操作皆可復原

假設更動版本至上一版本(空心圓)

```go
git reset HEAD~1
```

![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2035.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2035.png)

利用 reflog 來查詢所有紀錄，找到要復原的版本後利用SHA-1復原。

```go
git reflog
git reset <SHA-1 Hast>
```

![%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2036.png](%E3%80%90Git%20%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E3%80%91%20797e69e596b247b19e28f1b4c6e2f5f4/Untitled%2036.png)

---

### ~~重置版本/復原版本(待整理)~~

[p.com/post/2013/08/18/Learning-Git-Part-1-Installation-Options-Tool-Usage-on-Local](https://blog.miniasp.com/post/2013/08/18/Learning-Git-Part-1-Installation-Options-Tool-Usage-on-Local)

[https://blog.miniasp.com/post/2013/11/03/Learning-Git-Part-2-Master-Git-in-30-days](https://blog.miniasp.com/post/2013/11/03/Learning-Git-Part-2-Master-Git-in-30-days)

[https://guides.github.com/activities/hello-world/](https://guides.github.com/activities/hello-world/)

[https://www.tpisoftware.com/tpu/articleDetails/1450](https://www.tpisoftware.com/tpu/articleDetails/1450)
