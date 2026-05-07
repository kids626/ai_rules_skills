# AI Rules + Skills Pack（繁體中文）

可重複使用的 Cursor 規則與 Agent Skills，適合以 GitHub 版本控管並在多個專案間共用。

## 倉庫結構

```text
ai_rules_skills/
├── .cursor/rules/          # Cursor 專案規則
├── .github/                # GitHub Copilot 說明
└── skills/                 # Skill 文件（版本控管用）
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

將 `skills/` 內容依團隊流程同步至各環境。**專案中**慣例路徑為：`.cursor/skills/<skill 名稱>/SKILL.md`（請以 Cursor 目前版本說明為準）。

### 規則想達成的行為

1. 一律以繁體中文回覆  
2. 涉及程式碼時附上程式碼位置與可引用片段  
3. 若要改程式，說明插入／修改位置並附程式碼  
4. 逐行解釋須對新手友善，並補上隱含邏輯與特殊語法  
5. 詢問邏輯時附上可對應的程式位置  

---

## 常見問題（FAQ）

### 1）工作區根目錄與載入位置不一致（最常見）

Agent 會以「目前在 Cursor **開啟的那一層資料夾**」當工作區根目錄來找 `.cursor/skills/`，**不會**自動把整個 `htdocs` 底下所有子專案合併成同一組設定。

| 你開的工作區範例 | Skill 會從這裡讀 |
|------------------|------------------|
| `c:\xampp\htdocs\your_project` | `your_project\.cursor\skills\...` |
| `c:\xampp\htdocs`（上層資料夾） | `htdocs\.cursor\skills\...` |

若 Skill 放在子專案 `your_project\.cursor\skills\`，但你實際開的是上層 `htdocs`，該 Skill **可能完全不會載入**；設定頁也可能看似空白。**請依「視窗標題」或 File → Open Recent** 確認目前到底以哪一層當 workspace。

### 2）設定頁面上的 Skill 列表

介面上的「New Skill」等列表，多半是透過 UI 建立的清單，**不一定**會把 repo 裡手寫的每個 `SKILL.md` 都列進去。實務上仍可能在聊天中用 `/`、`@` 等方式引用（依 Cursor 版本與設定而定）。

結論：**畫面上是空的，不代表檔案沒作用**；若你預期「列表一定要有某幾項」，請對照該版本的官方說明，或改用 UI 建立並確認是否會同步顯示。

### 3）個人 skill 建議放哪？

- **全專案共用**：放在使用者目錄下的個人 skills（請勿誤放進內建的 `skills-cursor` 資料夾）。  
- **單一專案**：維持 `.cursor/skills/<名稱>/SKILL.md`。

建議先釐清：**目前 Cursor 開啟的工作區根目錄是子專案還是 `htdocs`？** 若是 `htdocs`，請把同一套 `.cursor/skills` 放到 `htdocs\.cursor\skills\`，或改為**只以子專案資料夾**當唯一工作區開啟，行為才會一致。

若你提供「工作區完整路徑」與「Cursor 版本」，可以進一步對照你畫面上的狀況。
