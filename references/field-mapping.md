# Field mapping：母層 storyline → 四品牌 collection

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
evidenceNote: 匿名交收節錄
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
