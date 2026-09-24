# 改寫規則與紅線

## 獨佔分配

- 每個 `案例/{類別}/caseNN` 只屬一個品牌；以 `Recycling/docs/case-allocation.md` 為準。
- 若 ledger 狀態為 `published` 於另一品牌，停止並回報衝突。
- ScrapBroHK 與 hkrecyclingco 同定位：靠不同 case、不同 slug／標題／query 差異化，不靠虛構服務差異。

## 允許改寫

Pipeline 模式優先讀 `case-brief.json`：下列地區與 query 改寫權只適用於 standalone。Pipeline 鎖定品牌、搜尋意圖、primary query、地區、場景與器材/SKU/數量；可調整語句與段落，但不能重新選題。標題不強制地區開頭。

- 地區側寫與客戶情境（可使用一般或已提供的客戶背景，不新增未獲授權的可識別 PII）
- 標題、`seoTitle`、`metaDescription`、primary／secondary query
- 難點與實用經驗的敘事角度（符合品牌：無償捐贈 vs 有價收購 vs 耗材 SKU）
- 內部連結改為該品牌真實路徑
- CTA 改為該品牌 WhatsApp／表單入口

## 不可改／不可發明

- 器材種類與數量（全文、表格、成果必須一致）
- 圖片可見的擺位、動作、包材、人數（以目視 webp 為準）
- prompt01／prompt02 場景連續性矛盾
- 碳減排數字、回收率、認證、法律結論（無供應來源時）
- 一律付款、一律免費、一律接單
- 打印耗材品牌：已用／空匣／舊機作為現行服務

## SEO 差異化檢查（同品牌批次）

產出前掃描該品牌已有 `title`、`seoTitle`、`district`＋主設備組合：

1. 標題不可只改一兩個字
2. primary query 不可完全相同
3. 同一地區＋同一主設備組合需換角度（原因、場地限制、資料處理）

## 發布（2026-09-15 擁有人決策）

- 中文可單獨上線
- 不再以 evidence／approval／雙語配對阻擋 build
- 仍須內容完整：標題、摘要、器材、流程、至少一張圖與 alt
- 對外仍遵守各品牌 `brand.md` 表述紅線

## 圖片

- Pipeline 用母層 `scripts/build-case-images.mjs` 匯出 `assets.json` 中已驗證的檔案，不再轉碼；standalone 舊案例保留原 WebP 路徑。
- 不把母層 PNG 或未選中的 angle-test／old 變體拷進品牌 repo
- cover 以 1200×630 為上限由清理後 before PNG 中心裁切；不足時沿用 manifest 實際尺寸與檔名，不放大。
