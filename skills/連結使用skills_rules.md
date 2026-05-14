================================================================================
連結使用：將本專案（ai_rules_skills）的 Cursor rules／skills 共用給其他專案
================================================================================

一、用途說明
-----------
若希望「另一個專案（以下稱 B 專案）」直接使用本 repo 已維護好的內容，可在 B 專案
內建立「符號連結（Symbolic Link）」，讓 B 的 .cursor\rules 或 skills 資料夾
指向本專案實體路徑。之後只須在本專案改檔，B 專案會一併看到相同內容。

適用對象：
  - .cursor\rules\（*.mdc 專案規則）
  - 本 repo 根目錄下的 skills\（各 SKILL.md 等）

注意：Cursor 不支援「填遠端 URL 自動載入」；跨專案共用須靠複製、Git submodule、
或本文件示範的 symlink／junction。


二、執行前準備（Windows）
------------------------
1. 權限（Windows）
   - 本文件內所有 `New-Item -ItemType SymbolicLink` **建議一律以「系統管理員身分」**
     開啟 PowerShell（開始選單搜尋 PowerShell → 右鍵 → **以系統管理員身分執行**）
     後再貼上指令，較可避免「拒絕存取」。
   - 若仍失敗，可再擇一處理：
     a) 維持管理員 PowerShell 重試；或
     b) 開啟 Windows「開發人員模式」：
        設定 → 隱私權與安全性 → 開發人員專用 → 開發人員模式。

2. B 專案目錄
   - B 專案根目錄下須先有 .cursor 資料夾（若無請自行建立）。
   - 若 B 專案已存在「要改成連結的同名資料夾」，請先備份後刪除該資料夾，
     否則 New-Item 無法在同一路徑建立連結。

3. 路徑請依實際環境修改
   - 本文件中的 pidi_admin 僅為範例；換其他專案時請改 B 的路徑變數。


三、共用 Cursor rules（.cursor\rules）
--------------------------------------
變數說明：
  $A_Rules = 本專案（來源）的 rules 資料夾
  $B_Rules = B 專案內要出現的 rules 路徑（將成為連結，勿保留舊的同名資料夾）

在 **以系統管理員身分執行的 PowerShell** 中執行（可依需要只改 $B_Rules 為你的 B 專案路徑）：

$A_Rules = "C:\xampp\htdocs\ai_rules_skills\.cursor\rules"
$B_Rules = "C:\xampp\htdocs\pidi_admin\.cursor\rules"

New-Item -ItemType SymbolicLink -Path $B_Rules -Target $A_Rules

成功後，於 B 專案用 Cursor 開啟工作區時，應會讀取與本專案相同的規則檔。

驗證（選做）：
  Get-Item $B_Rules | Select-Object FullName, LinkType, Target


四、共用本 repo 的 skills 資料夾
--------------------------------

> **Windows 必讀**：以下建立 **`skills` 目錄符號連結** 的步驟，請在 **以系統管理員身分執行的 PowerShell** 中操作（與「二、1」相同）。未提升權限時常出現「拒絕存取」。

若希望 B 專案根目錄下的 `skills` 也指向本專案（整包共用），流程與「三」相同：
先確認 B 專案沒有「要保留的」同名 `skills` 資料夾，**備份後刪除**，再於**管理員 PowerShell** 貼上執行。

**【範例】整包 `skills` 連到本專案（路徑請依你的 B 專案修改 `$B_Skills`）**

```powershell

$A_Skills = "C:\xampp\htdocs\ai_rules_skills\skills"
$B_Skills = "C:\xampp\htdocs\pidi_admin\skills"

New-Item -ItemType SymbolicLink -Path $B_Skills -Target $A_Skills
```

說明：skills 內路徑若寫死「專案根目錄下的 md文件檔」等，B 專案目錄結構不同時
可能需另調整 skill 內文或改為複製部分檔案，而非整包連結。


五、若符號連結無法建立（改用目錄 Junction）
------------------------------------------
僅適用「整個資料夾」、且多為本機相同磁碟。以 cmd 執行（先刪除 B 端舊資料夾）：

cmd /c mklink /J "C:\xampp\htdocs\pidi_admin\.cursor\rules" "C:\xampp\htdocs\ai_rules_skills\.cursor\rules"


六、維護與版本控制注意
----------------------
1. 若本專案（來源）路徑搬移或更名，B 端的連結會失效，需刪除舊連結後重建。
2. 將 symlink 提交進 Git 時，團隊成員在不同 OS 上可能行為不同；若需可重現
   的流程，可改在 README 註明「本機建立連結」或改用 Git submodule。
3. B 專案若需「自己的一份」規則，請勿對整包 rules 做連結，改為複製單一 .mdc
   或只連結特定檔案。


七、相關檔案位置（本專案）
------------------------
  規則：  ai_rules_skills\.cursor\rules\
  技能：  ai_rules_skills\skills\

（本文件路徑：skills\連結使用skills_rules.md）


