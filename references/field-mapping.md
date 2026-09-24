# Field mapping：母層 storyline → 五品牌 collection

Pipeline 附加欄位：五品牌皆寫 `primaryQuery`（brief.primary_query）及 `sourceCase`（brief.source），以便追蹤選題。圖片欄位從 assets.json 的 primary 取值；以下 1200px 檔名只為舊版示例，不是生成保證。地區／意圖／器材以 locked brief 為準。

## 所有品牌的發布頁正文合約（必須完整保留）

把母層 `storyline.md` 改寫成任何品牌 collection 時，詳情頁必須按以下次序呈現全部語義區塊。標題可配合品牌語氣微調，但不得因版面精簡、collection 格式或品牌模板而刪走區塊：

1. 案例摘要／情境
2. 器材資料表
3. 客戶要求及難點（必須是獨立、可見的段落）
4. 實際處理流程
5. 人手、時間及本案交易安排
6. 資料處理及設備去向
7. 可量度成果
8. 實用經驗
9. 現場圖片及準確 alt
10. 問答（v4 為 3-6 個 locked answer targets；exact question 作 H3，首段直接回答）
11. 相關服務及案例（案例連向 locked pillar／相關內容，並在每個指定 inbound source 加入具情境 anchor 回鏈案例 canonical URL）
12. 查詢 CTA

Markdown 品牌用 `##`／`###` 正文呈現；JSON 或結構化 collection 用對應欄位並由詳情頁 renderer 顯示。若現有 schema／template 缺少欄位，先擴充 schema 和 renderer，不能把內容塞入摘要或直接省略。`回收證據` 仍按 case type 及母層 storyline 決定是否保留，不屬每案強制區塊。

## 共用來源欄位（`storyline.md`）

| 來源 | 說明 |
| --- | --- |
| `case_id` / `url` 末段 | 建議 `caseId`／slug |
| `title` / `seo_title` / `meta_description` | 標題與 SEO；可按品牌改寫 |
| `service_area` / `venue` / `client_profile` / `recycling_reason` | 地區、場地、客戶側寫、原因 |
| 器材資料表 | 設備、品牌型號、數量、狀況 |
| 人手、時間及交易安排 | 個案交易結果（不可升格為承諾） |
| 資料處理及設備去向 | 去向／捐贈／再用 |
| 可量度成果 / 常見問題 | outcomes / FAQ |
| `image01.webp` / `image02.webp` | before / handling |

## ScrapBroHK（`src/content/cases/{caseId}.zh.md`）

```yaml
caseId: slug
locale: zh-Hant-HK
status: published
title: ...
summary: ...
seoTitle: ...          # optional but recommended
metaDescription: ...
publishedAt: YYYY-MM-DD
sector: 公司|學校|家居
district: 地區
equipment:
  - label: 主機
    quantity: 6
image: /cases/{caseId}/{caseId}-cover-1200x630.webp
imageAlt: ...
images:
  before: /cases/{caseId}/{caseId}-before-1200.webp
  beforeAlt: ...
  handling: /cases/{caseId}/{caseId}-handling-1200.webp
  handlingAlt: ...
```

Body：摘要、器材表、難點、流程、交易、去向、成果、FAQ、相關連結、CTA。

## hkrecyclingco（`src/content/cases/{caseId}.zh.md`）

```yaml
caseId: slug
locale: zh-Hant
published: true
title: ...
summary: ...
seoTitle: ...
metaDescription: ...
publishedAt: YYYY-MM-DD
updatedAt: YYYY-MM-DD
serviceArea: 地區
clientType: 公司|學校|家居|機構
equipment:
  - name: 主機
    quantity: 6
outcomes:
  - ...
evidenceNote: 匿名回收節錄
image: /cases/{caseId}/{caseId}-cover-1200x630.webp
imageAlt: ...
```

Body 必須存在並由詳情頁 render（表格＋FAQ）。

## green-hong-kong（`src/content/donationCases/{caseId}.zh.md`）

```yaml
caseId: slug
lang: zh
status: published
title: ...
summary: ...
seoTitle: ...
metaDescription: ...
publishedAt: YYYY-MM-DD
equipment:
  - category: 主機
    quantity: 6
    outcome: 再捐贈|下游分類|現場核對後處理
images:
  - src: /cases/{caseId}/{caseId}-before-1200.webp
    alt: ...
  - src: /cases/{caseId}/{caseId}-handling-1200.webp
    alt: ...
```

## green-printer（`src/content/inventory-cases/{caseId}.zh.json`）

```json
{
  "caseId": "slug",
  "locale": "zh-Hant-HK",
  "status": "published",
  "title": "...",
  "summary": "...",
  "seoTitle": "...",
  "metaDescription": "...",
  "situation": "...",
  "inventory": [{ "item": "HP 206A ...", "quantity": "2盒", "condition": "未開封原裝" }],
  "process": ["..."],
  "result": "...",
  "evidenceNote": "...",
  "publishedDate": "YYYY-MM-DD",
  "image": "/cases/{caseId}/{caseId}-cover-1200x630.webp",
  "imageAlt": "...",
  "images": {
    "before": "/cases/{caseId}/{caseId}-before-1200.webp",
    "beforeAlt": "...",
    "handling": "/cases/{caseId}/{caseId}-handling-1200.webp",
    "handlingAlt": "..."
  },
  "faq": [{ "question": "...", "answer": "..." }]
}
```

`condition` 必須符合現行收貨：全新、未開封、原裝。

JSON 的 `faq.question`／`answer` 等字串由模板當純文字輸出；從 storyline 搬入時移除 Markdown 標題前綴（例如 `### `），不要把 Markdown 語法顯示在公開頁。逐項檢查實際渲染。

## ReLight（`src/content/cases/{caseId}.md`）

`caseId`、`caseType`、`primaryQuery`、`secondaryQueries`、`district`、`sourceCase` 及結構化 `inventory` 全部由 locked brief 對應。新 narrative cases 使用 `editorial`，不顯示「代表性匿名情境」提示，亦不要求逐宗證據段落；正文可按 locked storyline 描述完成結果。歷史 `representative` 頁保留原有 hub／詳情提示與示範方案寫法。
