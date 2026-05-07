# AI Rules + Skills Pack（繁體中文）

可重複使用的 Cursor 規則與 Agent Skills，適合以 Git 版本控管並在多個專案間共用。

## 目錄

- [倉庫結構](#倉庫結構)
- [內容清單](#內容清單)
- [使用方式](#使用方式)
- [常見問題](#常見問題)

## 倉庫結構

```text
ai_rules_skills/
├── .cursor/rules/          # Cursor 專案規則
├── .github/                # GitHub Copilot 說明
└── skills/                 # Skill 原始檔（見下方「套用到專案」）
```

## 內容清單

| 類型 | 路徑 |
|------|------|
| Cursor Rules | `.cursor/rules/response-style.mdc` |
| GitHub Copilot | `.github/copilot-instructions.md` |
| Skill：逐行／新手解釋 | `skills/explain-code/SKILL.md` |
| Skill：修改程式 | `skills/modify-code/SKILL.md` |
| Skill：邏輯追蹤 | `skills/logic-trace/SKILL.md` |

## 使用方式

### Cursor 專案規則

將 `.cursor/rules/response-style.mdc` 複製到目標專案的相同相對路徑。

### GitHub Copilot

將 `.github/copilot-instructions.md` 複製到目標專案的相同相對路徑。

### Skills

- **本倉庫**：`skills/<名稱>/SKILL.md` 當作「原始檔」維護即可。
- **套用到其他專案**：每個子資料夾對應 Cursor 慣例路徑 `.cursor/skills/<名稱>/SKILL.md`（細節以 Cursor 當前版本文件為準）。
- 依團隊流程同步到各開發者環境即可。

### 規則想達成的行為

1. 一律以繁體中文回覆
2. 涉及程式碼時附上程式碼位置與可引用片段
3. 若要改程式，說明插入／修改位置並附程式碼
4. 逐行解釋須對新手友善，並補上隱含邏輯與特殊語法
5. 詢問邏輯時附上可對應的程式位置

---

## 常見問題

### 1）工作區根目錄與載入位置不一致（最常見）

Cursor／Agent 只會把「目前開啟的那一層資料夾」當工作區根目錄，並在該根目錄下找 `.cursor/skills/`；**不會**把上層目錄內所有子專案自動合併成同一組設定。

| 目前開啟的工作區 | `.cursor/skills` 預期位置 |
|------------------|-------------------------|
| `c:\xampp\htdocs\your_project` | `your_project\.cursor\skills\...` |
| `c:\xampp\htdocs`（上層） | `htdocs\.cursor\skills\...` |

Skill 若在 `your_project\.cursor\skills\`，但你實際開的是 `htdocs`，則可能**完全載入不到**，設定頁也可能看似空白。請用**視窗標題**或 **File → Open Recent** 確認 workspace 根目錄是哪一層。

### 2）設定頁上的 Skill 列表為何是空的？

介面中的「New Skill」等列表，多半對應 **UI 建立的** skill；**不一定**會列出 repo 內手寫的每個 `SKILL.md`。聊天中仍可能用 `/`、`@` 等方式引用（依版本與設定而定）。

**畫面上是空的，不代表檔案沒生效**；若需要「列表一定要出現」，請對照官方說明或改用 UI 建立並確認同步方式。

### 3）個人 skill 與專案 skill 放哪？

| 範圍 | 建議 |
|------|------|
| 全專案共用 | 使用者目錄下的個人 skills（勿誤放內建 `skills-cursor`） |
| 單一專案 | `.cursor/skills/<名稱>/SKILL.md` |

先釐清：工作區根是「子專案」還是「`htdocs` 上層」？若是 `htdocs`，請把同一套 `.cursor/skills` 放在 `htdocs\.cursor\skills\`，或改為**只開子專案資料夾**為工作區，行為才會一致。

需要他人協助排查時，可提供 **工作區完整路徑** 與 **Cursor 版本**。
