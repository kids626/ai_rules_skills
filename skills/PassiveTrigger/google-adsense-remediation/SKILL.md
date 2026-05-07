---
name: google-adsense-remediation
description: Generate and execute a remediation checklist for Google AdSense rejection due to low-value content. Use when the user mentions AdSense rejection, low value content, thin content, or asks for AdSense approval improvements.
disable-model-invocation: true
---

# Google AdSense 退件整改（缺乏價值內容）

## 目標
在網站送審 Google AdSense 前，建立可執行的整改清單，降低「缺乏價值內容（Low value content）」退件風險。

## 官方依據
- 審核說明：https://support.google.com/adsense/answer/9335564?hl=zh_TW
- 最低內容規定：https://support.google.com/adsense/answer/9335564#minimum_content_requirements
- 內容與使用者體驗：https://support.google.com/adsense/answer/10015918
- 薄內容（thin content）：https://support.google.com/webmasters/answer/9044175#thin-content
- Search Spam 政策：https://support.google.com/adsense/answer/1348737

## 使用時機
- 使用者收到 AdSense 退件通知，原因是「缺乏價值內容」。
- 使用者準備首次申請 AdSense，想先做內容與站點品質體檢。
- 使用者詢問如何提高 AdSense 審核通過率。

## 輸出格式
回覆時使用以下結構：
1. 現況診斷（高風險 / 中風險 / 低風險）
2. 立即修正（1-3 天）
3. 中期修正（1-2 週）
4. 送審前檢查清單
5. 建議重送時機

## 整改流程
複製這份清單並逐項打勾：

```markdown
AdSense Low Value Content 整改進度
- [ ] 盤點全站內容頁面數量與品質
- [ ] 移除或改寫薄內容頁
- [ ] 補齊關鍵信任頁面（About / Contact / Privacy）
- [ ] 提升內文深度與原創性（非模板拼湊）
- [ ] 改善版面可讀性與導覽結構
- [ ] 檢查是否有政策風險（Spam / 誤導 / 堆砌）
- [ ] 完成送審前 QA 並安排重送
```

### Step 1：內容盤點
- 先列出可被索引的內容頁（文章、產品頁、落地頁）。
- 標註每頁的字數、主題完整度、是否有明確使用者價值。
- 若內容重複、過短、僅為關鍵字拼貼，標記為高風險。

### Step 2：薄內容整改
- 合併主題重複頁面，避免多頁稀釋資訊。
- 將過短頁面擴寫為可解決使用者問題的完整內容。
- 補齊範例、步驟、比較、FAQ，提升實用性與停留價值。

### Step 3：信任與體驗補強
- 確認站內可清楚找到：`About`、`Contact`、`Privacy Policy`。
- 導覽列與內部連結要能幫助使用者找到下一步內容。
- 行動版可讀性、載入速度、廣告密度需維持可用體驗。

### Step 4：政策風險檢查
- 避免自動生成且未經人工校正的低品質內容。
- 避免誤導性標題、關鍵字堆砌、幾乎無資訊價值頁面。
- 內容需與使用者意圖一致，不做欺騙式導流。

### Step 5：送審前 QA
- 抽查至少 10 個重點頁，確認品質一致。
- 確認重要頁面可正常開啟，無大量 404/空白頁。
- 檢查 robots/noindex 設定，避免誤封鎖關鍵內容。

## 回覆原則
- 優先提供「可立即執行」的修正項，不只講原則。
- 每項建議都要說明「為何影響 AdSense 審核」。
- 若資訊不足，先要求必要資料（站點類型、內容量、近期改版、退件訊息截圖文字）。

## 資訊不足時先詢問
至少先蒐集：
1. 站點 URL 與主要內容類型
2. 已上線內容頁數與更新頻率
3. 近期是否大量新增模板頁或 AI 產文
4. 最近一次退件時間與退件訊息原文

## 延伸參考
- 進階檢核與執行細節請見 [reference.md](reference.md)

