# AI Rules + Skills Pack（繁體中文）

可重複使用的 Cursor 規則與 Agent Skills，以 Git 版本控管，方便在多個專案共用。

## 目錄

- [倉庫結構](#倉庫結構)
- [內容清單](#內容清單)
- [使用方式](#使用方式)
  - [跨專案共用（符號連結）](#跨專案共用符號連結)
  - [規則目標](#規則目標)
- [常見問題](#常見問題)

## 倉庫結構

```text
ai_rules_skills/
├── .cursor/rules/              # Cursor 專案規則（*.mdc）
├── .github/                    # GitHub Copilot 說明
├── skills/                     # Skill 原始檔（依團隊流程套用到 Cursor／複製／連結）
│   ├── PassiveTrigger/         # 被動觸發（依對話情境）
│   ├── ActiveTrigger/          # 主動觸發（關鍵字、流程型技能）
│   ├── 被動技能PassiveTrigger/ # 與 PassiveTrigger 對應的中文分類目錄（內容可能重複，維護時擇一為準）
│   ├── 主動技能ActiveTrigger/  # 與 ActiveTrigger 對應的中文分類目錄
│   └── 連結使用skills_rules.md # Windows 下以 symlink 共用 rules／skills 的步驟說明
└── Prompt/                     # 提示詞與案例素材（可選）
```

**複製套用：** 將規則檔複製到目標專案的 `.cursor/rules/`；將各 Skill 依 [Cursor 官方文件](https://cursor.com/docs) 目前版本說明放到專案或使用者 skills 路徑（例如 `.cursor/skills/<名稱>/SKILL.md`，實際以當版 UI／文件為準）。

## 內容清單

### Cursor Rules

| 類型 | 路徑 |
|------|------|
| 回覆風格、繁中、**強制**可點擊程式碼引用 | `.cursor/rules/response-style.mdc` |
| `savesop` 關鍵字觸發存檔流程 | `.cursor/rules/savesop-trigger.mdc` |
| `save-code-review-sop` 關鍵字觸發程式碼審閱封存 | `.cursor/rules/save-code-review-sop-trigger.mdc` |

### GitHub Copilot

| 類型 | 路徑 |
|------|------|
| Copilot 說明 | `.github/copilot-instructions.md` |

### Skills（PassiveTrigger）

| 說明 | 路徑 |
|------|------|
| 逐行／新手解釋 | `skills/PassiveTrigger/explain-code/SKILL.md` |
| 修改程式 | `skills/PassiveTrigger/modify-code/SKILL.md` |
| 邏輯追蹤 | `skills/PassiveTrigger/logic-trace/SKILL.md` |
| 資料庫結構輔助 | `skills/PassiveTrigger/db-schema-helper/SKILL.md` |
| Google AdSense 修復流程 | `skills/PassiveTrigger/google-adsense-remediation/SKILL.md` |

### Skills（ActiveTrigger）

| 說明 | 路徑 |
|------|------|
| 對話流程摘要 SOP（搭配 `savesop-trigger`） | `skills/ActiveTrigger/save-template-sop/SKILL.md` |
| Savepoint／對話檢查點 | `skills/ActiveTrigger/savepoint/SKILL.md` |
| 程式碼審閱封存（搭配 `save-code-review-sop-trigger`） | `skills/ActiveTrigger/save-code-review-sop/SKILL.md` |
| 前端設計 | `skills/ActiveTrigger/網頁/frontend-design/SKILL.md` |
| 前端設計（中文分類路徑副本） | `skills/主動技能ActiveTrigger/網頁相關技能/frontend-design/SKILL.md` |

> 分類說明可另見 `skills/說明.txt`。若倉庫內另有 `skills/被動技能PassiveTrigger/`、`skills/主動技能ActiveTrigger/`，為中文路徑之對應副本，同步或 symlink 前請確認要以哪一側為「單一來源」避免分歧。

## 使用方式

### Cursor 專案規則

將 `.cursor/rules/` 內需要的 `.mdc` 複製到目標專案**相同相對路徑**。

- 使用 `savesop-trigger.mdc` 時，請一併維護 `skills/ActiveTrigger/save-template-sop/SKILL.md`（或目標專案中等價路徑），並依該 skill 建立 `md文件檔/local_notes/` 等輸出目錄。
- 使用 `save-code-review-sop-trigger.mdc` 時，請一併維護 `skills/ActiveTrigger/save-code-review-sop/SKILL.md` 與對應輸出目錄規則。

### GitHub Copilot

將 `.github/copilot-instructions.md` 複製到目標專案**相同相對路徑**。

### Skills

| 情境 | 做法 |
|------|------|
| 在本倉庫維護 | 使用 `skills/PassiveTrigger/<名稱>/` 或 `skills/ActiveTrigger/<名稱>/`（並決定是否仍保留中文資料夾副本） |
| 套用到其他專案 | 依 Cursor 當版文件，將 skill 放到專案或使用者 skills 目錄 |

再依團隊流程同步到各開發者環境。

### 跨專案共用（符號連結）

若希望**另一個專案**直接使用本倉庫的 `.cursor/rules` 或根目錄 `skills/`（單一來源、改一次多專案生效），可在 Windows 以 **PowerShell 建立目錄符號連結**。

完整步驟、範例指令與注意事項（含 **請以系統管理員身分執行 PowerShell**）請見：

**[`skills/連結使用skills_rules.md`](skills/連結使用skills_rules.md)**

### 規則目標

`response-style.mdc` 與 `copilot-instructions.md` 想讓助手行為一致為：

1. 繁體中文回覆
2. 談程式碼、邏輯、修改位置、逐行說明時，使用 **可點擊的程式碼引用**（`起行:迄行:檔案路徑`），並避免僅用無路徑的一般 fenced code 代表專案內程式
3. 要改程式時說明插入／修改處並附可點擊引用
4. 逐行解釋要新手友善，並補隱含邏輯與特殊語法
5. 問邏輯時附上可追溯的程式位置

## 常見問題

### 1）工作區根目錄與 Skill 載入（最常見）

工作區根目錄＝你在 Cursor **目前開啟的那一層資料夾**。系統會在這一層底下找 `.cursor/skills/`；**不會**把上層裡所有子專案自動合併成同一組設定。

| 目前開啟的工作區 | `.cursor/skills` 會從這裡讀 |
|------------------|---------------------------|
| `c:\xampp\htdocs\your_project` | `your_project\.cursor\skills\...` |
| `c:\xampp\htdocs`（上層） | `htdocs\.cursor\skills\...` |

若 Skill 在 `your_project\.cursor\skills\`，但你開的是 `htdocs`，可能**完全載入不到**、設定頁也可能空白。請用**視窗標題**或 **File → Open Recent** 確認根目錄。

### 2）設定頁的 Skill 列表是空的？

「New Skill」等列表多半對應 **UI 建立的** skill，**不一定**列出 repo 內每個 `SKILL.md`。聊天仍可能用 `/`、`@` 引用（依版本與設定）。**列表空白 ≠ 檔案無效**；若堅持要出現在列表，請查官方說明或改用 UI 建立。

### 3）個人 skill 與專案 skill 放哪？

| 範圍 | 建議 |
|------|------|
| 全專案共用 | 使用者目錄下的個人 skills（勿誤放內建 `skills-cursor`） |
| 單一專案 | `.cursor/skills/<名稱>/SKILL.md`（以當版 Cursor 為準） |

工作區根若是 `htdocs` 而非子專案，請把 `.cursor/skills` 放在 `htdocs\.cursor\skills\`，或改為**只開子專案資料夾**為工作區。  
他人協助排查時，可提供 **工作區完整路徑** 與 **Cursor 版本**。

### 4）Symlink 提交到 Git 會怎樣？

符號連結在不同 OS／clone 行為可能不同。團隊若需可重現流程，建議在 README 或 `連結使用skills_rules.md` 註明「本機建立連結」，或改用 submodule／複製策略。
