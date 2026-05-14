先請ai執行換路徑
prompt:"來源 C:\xampp\htdocs\ai_rules_skills，目標 C:\xampp\htdocs，要 rules + 逐 skill 連到 .cursor\skills，skill 清單跟現有 md 一樣。"

# Windows 置入專案連結指令（PowerShell）

| 項目 | 路徑 |
|------|------|
| **來源（本倉庫）** | `C:\xampp\htdocs\ai_rules_skills` |
| **目標（工作區根）** | `C:\xampp\htdocs`（以 Cursor 開啟 `htdocs` 為根時會讀此層的 `.cursor`） |
| **Rules 連結位置** | `C:\xampp\htdocs\.cursor\rules` → 來源 `.cursor\rules` |
| **Skills 連結位置** | `C:\xampp\htdocs\.cursor\skills\<名稱>` → 來源各 skill 資料夾 |

**執行前提**

1. 使用 **以系統管理員身分執行的 PowerShell**。
2. 若目標路徑已存在**同名且為一般資料夾**（非連結），請先**備份後刪除**，再執行 `New-Item`，否則會失敗。
3. 建立各 skill 的符號連結前，**父目錄** `C:\xampp\htdocs\.cursor\skills` 必須存在；整段腳本開頭會先建立。

**一次可整段貼上執行**（建立目錄 → rules → 逐 skill；skill 清單與舊版 md 相同）。

```powershell
# 建立父目錄（已存在則略過）
New-Item -ItemType Directory -Force -Path "C:\xampp\htdocs\.cursor"
New-Item -ItemType Directory -Force -Path "C:\xampp\htdocs\.cursor\skills"

# rules
$A_Rules = "C:\xampp\htdocs\ai_rules_skills\.cursor\rules"; $B_Rules = "C:\xampp\htdocs\.cursor\rules"; New-Item -ItemType SymbolicLink -Path $B_Rules -Target $A_Rules

# 主動技能 ActiveTrigger（逐 skill → .cursor\skills）
$A_Skills = "C:\xampp\htdocs\ai_rules_skills\skills\主動技能ActiveTrigger\save-code-review-sop"; $B_Skills = "C:\xampp\htdocs\.cursor\skills\save-code-review-sop"; New-Item -ItemType SymbolicLink -Path $B_Skills -Target $A_Skills
$A_Skills = "C:\xampp\htdocs\ai_rules_skills\skills\主動技能ActiveTrigger\save-template-sop"; $B_Skills = "C:\xampp\htdocs\.cursor\skills\save-template-sop"; New-Item -ItemType SymbolicLink -Path $B_Skills -Target $A_Skills
$A_Skills = "C:\xampp\htdocs\ai_rules_skills\skills\主動技能ActiveTrigger\savepoint"; $B_Skills = "C:\xampp\htdocs\.cursor\skills\savepoint"; New-Item -ItemType SymbolicLink -Path $B_Skills -Target $A_Skills

# 被動技能 PassiveTrigger
$A_Skills = "C:\xampp\htdocs\ai_rules_skills\skills\被動技能PassiveTrigger\db-schema-helper"; $B_Skills = "C:\xampp\htdocs\.cursor\skills\db-schema-helper"; New-Item -ItemType SymbolicLink -Path $B_Skills -Target $A_Skills
$A_Skills = "C:\xampp\htdocs\ai_rules_skills\skills\被動技能PassiveTrigger\explain-code"; $B_Skills = "C:\xampp\htdocs\.cursor\skills\explain-code"; New-Item -ItemType SymbolicLink -Path $B_Skills -Target $A_Skills
$A_Skills = "C:\xampp\htdocs\ai_rules_skills\skills\被動技能PassiveTrigger\modify-code"; $B_Skills = "C:\xampp\htdocs\.cursor\skills\modify-code"; New-Item -ItemType SymbolicLink -Path $B_Skills -Target $A_Skills
$A_Skills = "C:\xampp\htdocs\ai_rules_skills\skills\被動技能PassiveTrigger\logic-trace"; $B_Skills = "C:\xampp\htdocs\.cursor\skills\logic-trace"; New-Item -ItemType SymbolicLink -Path $B_Skills -Target $A_Skills

# 選用 — 被動技能 PassiveTrigger
$A_Skills = "C:\xampp\htdocs\ai_rules_skills\skills\被動技能PassiveTrigger\google-adsense-remediation"; $B_Skills = "C:\xampp\htdocs\.cursor\skills\google-adsense-remediation"; New-Item -ItemType SymbolicLink -Path $B_Skills -Target $A_Skills
```

---

## 分號版（與舊檔相同風格，可單行複製）

**請先**執行過上面區塊中的兩行 `New-Item -ItemType Directory -Force ...`（或確認 `.cursor\skills` 已存在），且 **`.cursor\rules` 與各 skill 名稱下不可先存在同名一般資料夾**。

