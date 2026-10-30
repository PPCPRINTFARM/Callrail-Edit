# Phoenix Phase Converters — SEO Repair Plan & Timeline

**Domain:** phoenixphaseconverters.com
**Prepared:** 2026-10-30
**Approach:** Gradual, lowest-risk fixes first. No more than one major change category per week to isolate impact and avoid ranking volatility.

---

## Current Site Health Snapshot

| Metric | Value |
|---|---|
| Site Health Score | 85% |
| Errors | 19 |
| Warnings | 300 |
| Organic Traffic | ~8,400/mo |
| Authority Score | 30 |
| AI Visibility | 20 (Semrush) / 65% (UberSuggest) |
| Duplicate Titles | ~2,000 pages |
| Duplicate Descriptions | ~2,000 pages |
| Missing H1 Tags | 178 pages |
| Broken Links | 19 |

---

## Phase 1 — Quick Wins (Week 1-2)

*Zero ranking risk. These fix crawl errors and remove dead weight.*

### 1.1 Remove Motor Product Pages
- **Status:** COMPLETE
- 59 standalone motor products set to DRAFT
- 12 Phase Converter Idler Motors kept ACTIVE (core product)
- 61 URL redirects created (301 → `/collections/rotary-phase-converters`)
- `/pages/electric-motors` and `/collections/electric-motors` redirected

### 1.2 Fix 19 Broken Links
- **Risk:** None — fixing broken links only helps
- **Time:** 1-2 hours

| Pattern | Count | Fix |
|---|---|---|
| `hub.phoenixphaseconverters.com/autostart.html` | 13 pages | Update link to current AutoStart product page or remove dead subdomain reference |
| Missing PDF datasheets on CDN | 3 links | Re-upload PDFs to Shopify Files or CDN, update hrefs |
| Other 404s | 3 links | Audit and fix or redirect individually |

**How to execute:**
1. In Shopify Admin → Online Store → Pages, search each affected product page
2. Find the broken `hub.phoenixphaseconverters.com/autostart.html` link in the description
3. Replace with the correct URL (likely `/collections/digital-phase-converters-w-autostart`)
4. For missing PDFs: upload to Settings → Files, copy the new CDN URL, update links

### 1.3 Clean Up Empty Collections
- **Risk:** None
- Archive or hide these empty motor-related collections:
  - PM DC Electric Motor (0 products)
  - Definite Purpose Electric Motors (0 products)
  - General Purpose Electric Motors (0 products)
  - Electric Chain Hoists (0 products)
- Create redirects from their URLs to `/collections/rotary-phase-converters`

---

## Phase 2 — Theme-Level Fix (Week 3)

*Single change, massive impact. Fix once, fixes 178 pages.*

### 2.1 Add Missing H1 Tags (178 Pages)
- **Risk:** Low — adding proper heading structure improves SEO
- **Time:** 30 minutes (one theme file edit)
- **Root cause:** Shopify theme template doesn't output page/product titles as `<h1>` tags

**How to execute:**
1. Shopify Admin → Online Store → Themes → Edit Code
2. Open `templates/page.liquid` (or the relevant section file)
3. Find the page title output and wrap it in `<h1>` tags
4. Repeat for `templates/product.liquid` and `templates/collection.liquid` if needed
5. Preview before publishing — verify the H1 appears correctly on a few pages

**Verification:** Run a site crawl after 48 hours to confirm all 178 pages now have H1 tags.

---

## Phase 3 — Spanish Content & hreflang (Week 4-5)

*Addresses ~50% of all duplicate content. This is the single biggest duplicate content fix.*

### 3.1 Add hreflang Tags
- **Risk:** Low-medium — tells Google these are language variants, not duplicates
- **Impact:** Resolves ~2,000 duplicate title/description issues in one move

**Root cause:** Spanish `/es/` mirror pages copy English meta tags verbatim. Google sees identical titles/descriptions on two URLs and flags them as duplicates.

**How to execute:**
1. Add hreflang tags to the `<head>` of every page:
```html
<link rel="alternate" hreflang="en" href="https://phoenixphaseconverters.com/PAGE" />
<link rel="alternate" hreflang="es" href="https://phoenixphaseconverters.com/es/PAGE" />
<link rel="alternate" hreflang="x-default" href="https://phoenixphaseconverters.com/PAGE" />
```
2. This goes in the theme's `layout/theme.liquid` file
3. Use Shopify's `request.locale` and `request.path` to generate dynamically

### 3.2 Localize Spanish Meta Titles & Descriptions
- **Risk:** Low — only affects `/es/` pages
- **Time:** Can be done gradually over weeks 4-5
- Translate the top 50 highest-traffic Spanish pages first
- Use consistent title format: `[Producto] | Phoenix Phase Converters`

**Priority order for translation:**
1. Homepage (`/es/`)
2. Collection pages (`/es/collections/...`)
3. Top 20 product pages by traffic
4. Blog posts (lowest priority — most visitors read English)

---

## Phase 4 — Blog Meta Descriptions (Week 6-7)

*Fixes ~218 blog pages sharing one generic meta description.*

### 4.1 Unique Blog Post Descriptions
- **Risk:** Low — meta descriptions don't directly affect rankings, but improve CTR
- **Time:** ~5-10 minutes per post, batch in groups of 30/week

**How to execute:**
1. Shopify Admin → Blog Posts → Edit each post
2. Scroll to "Search engine listing" section
3. Write a unique 150-160 character description summarizing that specific post
4. Save

**Priority order:**
1. Blog posts with highest organic traffic (check Google Search Console)
2. Blog posts ranking on page 1-2 for target keywords
3. Motor wiring diagram posts (these drive significant traffic — keep them)
4. Remaining posts

**Template for descriptions:**
> Learn [topic] for [application]. [Key takeaway]. Expert guide from Phoenix Phase Converters.

---

## Phase 5 — Product Page Meta Optimization (Week 8-10)

*Addresses remaining duplicate titles across product pages.*

### 5.1 Unique Product Titles & Descriptions
- **Risk:** Medium — changing titles on ranking pages can temporarily affect rankings
- **Batch size:** 20-30 products per week maximum
- **Monitor:** Google Search Console for any ranking drops after each batch

**Title format:**
```
[HP] [Type] Phase Converter - [Voltage] | Phoenix Phase Converters
```
Example: `20HP Rotary Phase Converter - 230V | Phoenix Phase Converters`

**Description format (150-160 chars):**
```
Shop the [HP] [Type] from Phoenix Phase Converters. [Key feature]. [Warranty/shipping detail]. Call for expert sizing help.
```

**Batch order (safest first):**
1. Week 8: Products with zero organic traffic (no risk)
2. Week 9: Products with low traffic (< 10 visits/month)
3. Week 10: Higher-traffic products (proceed carefully, monitor daily)

### 5.2 Transformer Page Differentiation
- 31 transformer products likely share similar meta
- Differentiate by: voltage, kVA rating, application (CNC, HVAC, welding)

---

## Phase 6 — AEO & Content Strategy (Week 11-16)

*Longer-term play to improve AI visibility from 20% toward 60%+.*

### 6.1 Current AI Visibility Gap

| AI Engine | Phoenix | American Rotary (Competitor) |
|---|---|---|
| Overall | 65% | 97.5% |
| Gemini | 90% | — |
| ChatGPT | 50% | — |
| AI Overviews | — | — |

### 6.2 Target Prompts to Optimize For
Focus content on prompts where Phoenix is weak or absent:
- "What size phase converter do I need?"
- "Rotary vs digital phase converter"
- "How to wire a phase converter"
- "Best phase converter for CNC machines"
- "Phase converter for farm/agricultural use"
- "Single phase to three phase conversion options"

### 6.3 Content Calendar

| Week | Blog Post Topic | Target Prompt |
|---|---|---|
| 11 | Phase Converter Sizing Guide (comprehensive) | "What size phase converter do I need?" |
| 12 | Rotary vs Digital: Complete Comparison | "Rotary vs digital phase converter" |
| 13 | Phase Converters for CNC Machines | "Best phase converter for CNC" |
| 14 | Agricultural Phase Converter Guide | "Phase converter for farm use" |
| 15 | Wiring Guide: Single Phase to Three Phase | "How to wire a phase converter" |
| 16 | FAQ Page: 25 Most Asked Questions | Multiple long-tail prompts |

### 6.4 Structured Data (Schema Markup)
- Add `Product` schema to all product pages (price, availability, reviews)
- Add `FAQPage` schema to FAQ content
- Add `HowTo` schema to wiring/installation guides
- Add `Organization` schema to homepage

---

## Phase 7 — Competitor Tracking & Citation Building (Ongoing)

### 7.1 Track Competitors in Brand Monitoring
- American Rotary (97.5% AI visibility — primary target)
- Phase-A-Matic
- Kay Industries

### 7.2 Citation Gap Strategy
- Identify directories/publications where competitors appear but Phoenix doesn't
- Target: industrial directories, equipment review sites, trade publications
- Goal: close the 451 → 600+ citation gap over 3 months

---

## Monitoring Schedule

| Frequency | Action |
|---|---|
| Daily (Week 1-4) | Check Google Search Console for crawl errors, indexing issues |
| Weekly | Run UberSuggest site audit, compare health score |
| Bi-weekly | Check keyword rankings for top 20 terms |
| Monthly | Full AI visibility check, citation count, traffic comparison |

## Rollback Protocol

If any phase causes a ranking drop > 10% for key terms:
1. **Stop** all changes immediately
2. **Revert** the most recent batch of changes
3. **Wait** 2 weeks for rankings to stabilize
4. **Analyze** which specific change caused the drop
5. **Resume** with smaller batches or adjusted approach

---

## Summary Timeline

```
Week 1-2   [======] Phase 1: Quick wins (broken links, cleanup) ............. DONE (motors)
Week 3     [===]    Phase 2: H1 tag fix (theme edit) ........................ LOW RISK
Week 4-5   [======] Phase 3: hreflang + Spanish meta ........................ LOW RISK
Week 6-7   [======] Phase 4: Blog meta descriptions ......................... LOW RISK
Week 8-10  [=========] Phase 5: Product meta optimization ................... MEDIUM RISK
Week 11-16 [==================] Phase 6: AEO content strategy ............... NEW CONTENT
Ongoing    [>>>>>>>>>>>>>>>>>>>>] Phase 7: Citations & monitoring ........... ONGOING
```

**Estimated completion:** 16 weeks for all phases
**Expected outcome:** Site health 85% → 95%+, AI visibility 20% → 50%+, duplicate issues reduced by 90%+
