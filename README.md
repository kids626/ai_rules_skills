# AI Rules + Skills Pack (Traditional Chinese)

這個倉庫提供可重用的 AI 規則與 Skills，適合放在 GitHub 版本控管並跨專案重複使用。

## 內容

- Cursor Rules: `.cursor/rules/response-style.mdc`
- GitHub Copilot 規則: `.github/copilot-instructions.md`
- Skills:
  - `skills/explain-code/SKILL.md`
  - `skills/modify-code/SKILL.md`
  - `skills/logic-trace/SKILL.md`

## 使用方式

### 1) Cursor 專案規則
把 `.cursor/rules/response-style.mdc` 複製到你的專案同路徑。

### 2) GitHub Copilot 規則
把 `.github/copilot-instructions.md` 複製到你的專案同路徑。

### 3) Skills
`skills/` 目錄用來集中管理 Skill 文件（版本控管用）。
可依團隊流程同步到各開發者環境。

## 規則目標

1. 一律繁體中文
2. 涉及程式碼時要附程式碼位置
3. 需要修改程式時要說明加入位置並附程式碼
4. 逐行解釋需新手友善，補充隱含邏輯與特殊語法
5. 詢問邏輯時要附可追蹤的位置



## 常見問題
1. 工作區根目錄不一致（最常見）
Agent 的專案 skill 是掛在「你目前在 Cursor 開啟的那個資料夾」底下的 .cursor/skills/，不是整個 htdocs 自動合併。

若工作區是 c:\xampp\htdocs\pidi_admin → 會讀
pidi_admin\.cursor\skills\...（您放的位置才對）
若工作區是 c:\xampp\htdocs（上層）→ 專案 skill 應在
htdocs\.cursor\skills\...
放在 pidi_admin\.cursor\skills\ 時，這個工作區可能完全不會載入，設定頁也可能仍顯示空白。
請在 Cursor 看視窗標題或 File → Open Recent 確認目前開的是哪一層當 workspace。

2. 設定頁列出的是「另一種」Skill
這個 Skills 介面上的 「New Skill」，多半是透過 UI 建立的 skill 清單；不一定會把你在 repo 裡手寫的 SKILL.md 全部列成清單。
實務上仍可能在聊天用 / 或 @ 去叫出專案／個人 skill（依 Cursor 版本與設定而定）。

所以：畫面上是空的，不等於檔案沒生效；但若你預期「列表裡要看到三個」，可能要改用 UI 建立，或確認官方說明是否會同步顯示檔案型 skill。

3. 個人 skill 的路徑
若要所有專案都能用，習慣上是放在使用者目錄下的個人 skills（請勿放進內建的 skills-cursor 資料夾）。專案內則維持 .cursor/skills/<名稱>/SKILL.md。

建議您先確認一件事：目前 Cursor 開啟的工作區根目錄是 pidi_admin 還是 htdocs？若是 htdocs，把同一套 .cursor/skills 複製或連結到 htdocs\.cursor\skills\，或改以 pidi_admin 當唯一工作區開啟，行為才會一致。

若您補充「工作區路徑」與「Cursor 版本」，我可以更精準對應到您畫面上的狀況（我目前為 Ask 模式，無法代您搬檔或改設定；若要自動改目錄結構可改開 Agent 模式）