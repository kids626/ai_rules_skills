---
name: savepoint
description: >-
  Summarizes the current chat into three sections (initial question, guided
  steps, final outcome) and appends a reusable prompt block. Use when the user
  types savepoint, Savepoint, or asks to save a conversation checkpoint to
  CursorMemory for this project (pidi_admin).
---

# Savepoint（對話存檔）

## 何時使用

- 使用者訊息包含 **`savepoint`**（不分大小寫亦可），或明確說要「對話存檔／檢查點／整理這段對話」並指向 **`md文件檔/CursorMemory`**。

## 輸出格式（必須）

使用**繁體中文**，依序輸出：

1. **一開始是如何提出需求與問題的**（條列主要問題與 URL／檔案若已知）
2. **過程中是如何一步步引導、修正與優化的**（按時間或邏輯順序條列）
3. **最後是如何產出目前這個結果的**（現況：改了哪些層級－view／controller／model／component）

最後**一定要**附上一段「**可直接複製使用、能夠重現相同結果的提示詞**」（獨立程式碼塊），內容需足以讓另一個對話在相同技術棧下重做同款追查或實作。

## 風格與程式碼引用

- 若提及既有程式，請標出**可點擊行數**的程式碼引用（專案內路徑）。
- 簡潔為主；不要複製整份對話逐句貼上，改為**結構化摘要**。

## 寫入專案存檔（分支判斷）

當使用者要求存檔或打出 **savepoint** 且希望寫入檔案時，**先判斷是否引用既有 savepoint 的 `.md`**（例如：貼上完整路徑、`@md文件檔/CursorMemory/某檔.md`、或明確寫出 `savepoint_*.md`／`savepoint.md` 要接續同一份）。

### A. 有引用既有 savepoint 檔（接續同一份）

1. **只在被引用的那個檔案**內操作：於**檔尾追加**本次內容（建議新開一節，標題如 **`## 追加紀錄（YYYY-MM-DD）`** 或 **`### 主題簡述`**，內含日期／主題與三段摘要＋可複製提示詞）。
2. **不要**再新建另一份 **`savepoint_<日期>_<主題>.md`**，也不要複製整份舊檔另存新檔。

### B. 未引用既有檔（新開一筆存檔）

1. **新建一個檔案**（若檔名已存在則在檔名尾端加 `_2`、`_3`…），路徑與檔名格式為：
   - **`md文件檔/CursorMemory/savepoint_<日期>_<主題>.md`**
2. **`<日期>`**：**`YYYY-MM-DD`**（以使用者環境「今天」為準；若使用者指定日期則依指定）。
3. **`<主題>`**：一句簡短識別。**轉成檔名時**：空白改 **`_`**，移除或替換 **`\/:*?"<>|`** 等不合法字元；避免過長（建議約 20 字內或英文單字組合）。
4. 檔案內文須包含本 skill「輸出格式」之**完整三段＋可複製提示詞**；可於檔首加：`<!-- savepoint: 日期 / 主題 -->`。

## 參考範本

- 內文結構可沿用：`md文件檔/CursorMemory/savepoint.md`（若仍存在）。
- 分筆存檔：`md文件檔/CursorMemory/savepoint_*.md`，依檔名日期與主題檢索；**接續寫入時**以使用者指定的既有檔為準，依 **A** 規則追加。
