---
name: db-schema-helper
description: 查詢本專案資料庫結構與資料表關聯，權威來源為專案根目錄 skills-db-schema-helpers 下的 SQL dump
---

# DB Schema Helper（本專案）

## 目標
當需求涉及資料庫、資料表、欄位、索引、關聯時，優先使用「專案根目錄的 `skills-db-schema-helpers/`」下的 SQL dump 作為權威來源；若根目錄不存在才改用「從你正在詢問的檔案路徑往上層搜尋到的 `skills-db-schema-helpers/`」。避免只依 Model 猜欄位。

## 權威來源
- 資料庫結構以「自動定位到的 `skills-db-schema-helpers/`」內的 SQL dump（`*.sql`）`CREATE TABLE` 定義為準。
- 自動定位規則（很重要）：
  - 先檢查「專案根目錄」是否存在 `skills-db-schema-helpers/`：
    - 若存在：直接使用它作為本次權威 schema 目錄（不再往上層尋找）。
    - 若不存在：才進入下一步。
  - 以使用者「正在詢問/指定的檔案路徑」作為起點（例如 Controller / View / Model 的檔案）。
  - 從該檔案所在目錄開始，逐層往上層目錄搜尋是否存在 `skills-db-schema-helpers/`。
  - 找到的第一個（最近的）`skills-db-schema-helpers/` 視為本次權威 schema 目錄。
- 檔名不限定 `pidi_new.sql`，需先挑選本次使用的權威 SQL 並在回答中註明檔案路徑。
- 若與 Yii Model 不一致，先以本次權威 SQL 為主，並明確註記差異。

## 必做規則
1. 先用「自動定位規則」找到本次權威 `skills-db-schema-helpers/` 目錄，再在該目錄找 `*.sql`，決定本次權威 SQL 後再搜尋目標表名，找到對應 `CREATE TABLE` 區塊。
2. 回答時至少交代：
   - 表名
   - 相關欄位（型別 / 是否可為 NULL / 預設值）
   - 索引或主鍵（若有）
3. 涉及表關聯時：
   - 先看 `*_id` 欄位與欄位命名
   - 再到專案中搜尋同欄位在哪些表/Model/Controller 被使用
4. 不要只靠 `protected/models/*.php` 推論資料庫實際欄位。
5. 若使用者說明「正式機 DB 已變更但尚未回寫 SQL」，以使用者描述為準，並註明可能與權威 SQL 不同。

## 建議查詢流程
1. 先檢查「專案根目錄」是否存在 `skills-db-schema-helpers/`。
2. 若根目錄不存在：取得使用者正在詢問的檔案路徑（例如 `protected/controllers/...`），從該檔案所在目錄往上層搜尋最近的 `skills-db-schema-helpers/`。
3. 在定位到的 `skills-db-schema-helpers/` 目錄找 `*.sql` 候選檔。
4. 挑選本次權威 SQL（建議優先：完整 `CREATE TABLE` 較多、檔案較新、名稱較接近專案/DB）。
5. 在權威 SQL 搜尋表名（例如 `company_info`），擷取該表 `CREATE TABLE` 的欄位與索引。
6. 到 `protected/models` 找 `tableName()` 交叉確認。
7. 到 `protected/controllers`、`protected/views` 搜尋欄位/Model 名稱，確認實際使用情境（查詢、篩選、JOIN、顯示）。
8. 輸出結論時附上檔案位置與重點片段，並註明本次權威 SQL 路徑。

## 回答格式（建議）
- 結論先行（1~3 句）
- 本次權威 SQL 路徑
- 表結構重點（欄位/型別/索引）
- 程式使用位置（Controller / Model / View）
- 風險與差異（若 SQL 與 Model 不一致）

## 常見陷阱
- Model 有屬性不代表資料表一定有該欄位。
- dump 常無 foreign key，不能因此判斷「無關聯」。
- 搜尋條件在 `search()` 或 criteria 的 JOIN 可能引用其他表欄位，需回到 SQL 驗證存在性。
- 同目錄可能有多份 SQL，回答前要先聲明本次採用哪一份。