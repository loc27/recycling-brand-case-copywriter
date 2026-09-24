---
name: recycling-brand-case-copywriter
description: Adapt one Hong Kong recycling case from the shared Recycling/案例 pool into a single brand's published case page—rewriting copy for that brand's brand.md and copywriter.md SEO targets, copying webp images into the brand repo, and writing collection content with readable tables. Use when assigning or editing brand-specific case studies for ScrapBroHK, hkrecyclingco, green-hong-kong, green-printer-consumables-recycling, or ReLight; not for generating new scene images or creating brand-neutral storylines only.
---

# Recycling Brand Case Copywriter

Turn one source case into one brand-owned published case. Each source case is exclusive to one brand (see the allocation ledger).

## Required inputs

- Brand key: `ScrapBroHK` | `hkrecyclingco` | `green-hong-kong` | `green-printer-consumables-recycling` | `ReLight`
- Source path under `Recycling/案例/{類別}/caseNN/`
- Optional: override `caseId` only if ledger already lists it

If brand or source path is missing, ask one short question.

Pipeline mode: both are resolved by canonical `case-brief.json`. Read it before writing and do not ask again. Preserve brand, district, intent, primary_query, models/SKUs, quantities, typed answer targets and topic cluster; rewrite expression only. The parent pipeline invocation supplies batch and deployment scope. Do not add permission questions for actions already authorized by that invocation.

## Before writing

1. Confirm git root and remote belong to the target brand only.
2. Read, in order:
   - Brand `docs/ssot/brand.md`
   - Brand `docs/ssot/copywriter.md`
   - Parent `Recycling/docs/case-allocation.md` — verify this source is assigned to this brand and not already published elsewhere
   - Source `prompt01.md`, `prompt02.md`, `storyline.md`
3. Open and visually inspect `image01.webp` and `image02.webp`. Claims must match visible equipment and handling.
4. Read [references/field-mapping.md](references/field-mapping.md) and [references/rewrite-rules.md](references/rewrite-rules.md).

## Execution

1. Resolve `caseId` from the ledger slug (preferred) or storyline `url` final segment.
2. Run the Recycling parent's `scripts/build-case-images.mjs` with explicit source and target brand `public/cases` paths. Pipeline cases export verified derivatives from `assets.json` without re-encoding; copy actual filenames/sizes, never assume 1200px exists. Do not commit source PNGs from the parent pool.
3. Rewrite storyline into the brand collection format. Read and obey the cross-brand published-body contract in [references/field-mapping.md](references/field-mapping.md): every brand must preserve all required semantic sections from the storyline, including a distinct customer requirements/challenges section; a compact brand layout is not permission to omit one.
   - ScrapBroHK / hkrecyclingco / green-hong-kong / ReLight → Markdown + frontmatter
   - green-printer → JSON
4. Apply brand voice and red lines from `copywriter.md`. Standalone mode permits editorial query/district framing; pipeline mode preserves the locked brief and adds `primaryQuery` and `sourceCase` metadata. District need not lead the title. Keep equipment/models/counts and visible facts consistent; do not claim occluded inventory is all visible.
5. Build a readable equipment table and FAQ in body or structured fields. Confirm the rendered detail page exposes every required body section in the prescribed order; when a collection is JSON or field-driven, extend its schema/template instead of silently dropping unsupported sections.
6. Set Chinese-only publish fields per loosened gates (`status: published` or `published: true`). Do not require English pair for first ship.
7. Run brand validator (if any) and `npm run build`. Fix errors before finishing.
8. Pipeline mode writes `brand-review.json`, checkpoints `brand`, and returns to the orchestrator for build/browser/deployment verification. Only its `published` checkpoint updates the ledger after actual live verification. Standalone mode updates ledger within current task authorization and never calls a local build a live publication.

## Semantic review checklist

- Inventory counts match table, summary, outcomes, and visible images
- Published body preserves the full cross-brand structure in `field-mapping.md`; `客戶要求及難點` remains a distinct rendered section
- No payment/donation universal promises; case fees stay case-specific
- Printer brand: only 全新／未開封／原裝 as current acceptance
- ReLight editorial cases: no anonymous-scenario disclosure or per-case evidence gate; narrate the locked storyline and result while keeping service promises case-specific
- ReLight historical representative cases: preserve their visible disclosure and bounded preparation wording
- Internal links resolve on that brand site
- Title / primary query not duplicated within the same brand's existing cases
- Hub lists a card; detail page has its own URL and meta

## Boundaries

- Do not assign the same source case to a second brand
- Do not edit other brands in the same turn unless the user explicitly batch-requests
- Do not change DNS, Cloudflare bindings, or production deploy unless separately authorized
- Do not use `$recycling-case-generator` image generation here; reuse existing webp
- Do not push or open PRs unless the user asks
