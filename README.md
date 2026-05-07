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
