# Handoff — CR Flow: Suggest Plan Screen

## Màn hình được review
**"CR Optimization Proposal"** — màn hình AI phân tích product page và đề xuất danh sách thay đổi giúp cải thiện Conversion Rate. Layout split: panel trái (danh sách change items) + panel phải (preview product page).

---

## UX Issues đã identify

**Data errors cần fix ngay:**
- AOV hiển thị `1.4%` thay vì $ value
- Issues count `11` nhưng math chỉ ra `5` (3+1+1)
- Conversion Score `42` không có thang đo

**Structural issues:**
- WHAT TO DO đang viết cho AI executor, không phải cho human reviewer → user đọc không hiểu
- Jargon dày đặc: USP, Above the fold, Trust signals, Copy — seller trình độ thấp không hiểu
- Tags "First impression / Offer clarity / Trust signals" ở header không rõ là interactive hay label
- Add new item (empty card) không có template/placeholder
- Delete không có confirm, không có undo

---

## User Profile đã xác định
- Seller ecommerce kỹ năng web builder thấp
- Lười đọc — chủ yếu scan
- Cần hiểu đủ để tự tin click Apply, không cần hiểu technical detail

---

## Solution đã thống nhất

### 1. Tách 2 layer content trong mỗi card
- **CURRENT SITUATION** → giữ nguyên format, viết cho user
- **WHAT TO DO** → đổi thành **WHAT WILL CHANGE** — viết benefit/outcome cho user review
- Implementation detail (instructions cho AI) là internal data, không hiển thị

### 2. Bold rule cho AI gen content
- **CURRENT SITUATION bold** = triệu chứng cụ thể, quan sát được trên page (không bold hệ quả sau →)
- **WHAT WILL CHANGE bold** = tên element + trạng thái mới sau khi apply (không bold benefit abstract)
- Kiểm tra: che hết text thường, chỉ đọc bold → vẫn hiểu vấn đề và điều gì thay đổi

### 3. Card titles rewrite — ngôn ngữ seller
| Before | After |
|--------|-------|
| Clean Up Product Gallery | Fix Your Product Photos |
| Add USP Hook + Benefit Summary | Give Buyers a Reason to Buy |
| Simplify the Buy Buttons Area | Make Your Buy Button Stand Out |
| Add Trust Badges | Show Buyers They Can Trust You |
| Rewrite Description Copy | Make Your Description Easy to Read |

---

## Cards đã rewrite (Cards 1–5)

### Card 1 — Fix Your Product Photos
**CURRENT SITUATION**
**First image is a before/after with promotional badges** → looks like an ad, not a real product.

**WHAT WILL CHANGE**
- **First image** becomes a **clean product shot on white background** → buyers see the real product immediately
- **Before/after images** move to **position #5+** — kept, just placed where they belong
- All **thumbnails** share the **same square ratio and padding** → gallery looks consistent and professional

---

### Card 2 — Give Buyers a Reason to Buy
**CURRENT SITUATION**
**Title and buy area show no result or benefit** → buyers don't understand the product's value before scrolling down.

**WHAT WILL CHANGE**
- **Product title** includes a **specific result** — e.g. *"...Clears Oil & Tightens Pores"*
- **A hook sentence** appears **directly below the title** → buyers know why to buy in under 3 seconds
- **3 benefit bullets** placed **above the Add to Cart button** → buyers decide faster without reading the full description

---

### Card 3 — Make Your Buy Button Stand Out
**CURRENT SITUATION**
**Buy area has multiple buttons with no size or contrast hierarchy** → buyers hesitate and leave at the moment of purchase.

**WHAT WILL CHANGE**
- **Buy Now** becomes the **largest, highest-contrast button** → buyers know exactly what to tap
- **Bundle offers** move **below the main buttons** — still visible but no longer competing for attention
- **Only one buy button** remains **per page section** → cleaner, less distraction

---

### Card 4 — Show Buyers They Can Trust You
**CURRENT SITUATION**
**No trust signals near the buy button** → buyers lose confidence at the exact moment of decision.

**WHAT WILL CHANGE**
- **An icon row** appears **directly below Buy Now**: *30-day returns · Secure checkout · Tracked shipping*
- **A summary line** added **near the price**: *"Free shipping | 30-day returns"* → buyers see it instantly without searching
- **Money-back badge** only added **if you actually have that policy** — don't add if it isn't real

---

### Card 5 — Make Your Description Easy to Read
**CURRENT SITUATION**
**Description is one dense paragraph block with no structure** → buyers skip it and miss the key benefits.

**WHAT WILL CHANGE**
- **First paragraph** leads with **the key result in one sentence** → buyers know what the product does before reading further
- **Long paragraphs** break into **short blocks of 2–3 sentences** → easy to scan, not overwhelming
- **Small section headers** divide the content: *How it works · How to use · Who it's for*

---

## High/Medium/Low Badge

- Hiện tại giải quyết được "cái này có quan trọng không" nhưng chưa đủ để user tự tin quyết định apply
- **Đề xuất thêm +% CR per item** — nhưng không thể dùng số tuyệt đối vì thiếu evidence
- **Kết luận:** Phase 1 dùng benchmark framing *"Stores that fixed this typically saw +X–Y%"*, Phase 2 build first-party data từ platform
- High/Medium/Low có thể chuyển sang encode **effort** (Quick fix / Standard / Custom) thay vì priority

---

## Preview Highlight Rules

**Rule cơ bản:** 1 card = 1 vùng highlight duy nhất trên preview

**Existing element** → solid highlight
**New element chưa tồn tại** → ghost block dashed border + "NEW" badge, inject đúng vị trí theo implement flow order

**Ghost states:** ẩn khi collapsed, subtle khi hover, prominent khi expanded, biến thành real element sau Apply

**Mapping đã xác định:**
| Card | Vùng highlight | Type |
|------|---------------|------|
| Fix Your Product Photos | Gallery zone (hero + thumbnails) | Solid |
| Give Buyers a Reason to Buy | Title & description zone (title → above CTA) | Solid |
| Make Your Buy Button Stand Out | Buy area zone (price + CTA + bundles) | Solid |
| Show Buyers They Can Trust You | Ghost block ngay dưới ADD TO CART | Ghost |
| Make Your Description Easy to Read | Product description zone + auto-scroll | Solid |

**Implement flow order** (dùng để xác định vị trí ghost block):
```
Announcement bar → Header → Title & Short description → Pricing display
→ Trust badges → Policy → Product gallery → Product Details
→ Q&A → UGC images → Review section → Footer
```

---

## Còn open / chưa xử lý
- **FAQ card (Card 6):** bug nghiêm trọng — content placeholder sai product (câu hỏi về battery/Sony camera cho skincare product)
- **Badge redesign:** effort thay vì priority chưa được finalize
- **+% CR feature:** cần user research / A/B test để validate trước khi pitch PM

---

## Session 2 — Summary Section & CR Uplift Rules

### Summary Section — Redesign đã thống nhất

**Bỏ AOV card** — không có data đo lường AOV trong scope CR optimization.

**3 cards mới:**

| Card | Nội dung |
|------|----------|
| CONVERSION RATE | Current CR + "↑ Est. up to X% if fixed" (green, nhỏ) |
| CONVERSION SCORE | Score lớn + progress bar + benchmark label "Avg store: 65 · Good: 70+" |
| ISSUES FOUND | Chỉ hiển thị số issue, bỏ phần high/medium/low breakdown |

**Tags "First impression / Offer clarity / Trust signals":**
- Đổi từ pill border (trông như button) → colored dot + plain text
- Không interactive, không hover — là label thuần túy

**Hierarchy fix:** "X HIGH" ở Issues card phải là focal point tạo urgency, không phải Score number.

---

### CR Uplift — Lookup Table Per-Item (Phase 1)

Nguồn: CRO industry benchmark (Baymard, ConversionXL, IRP Commerce).
Framing bắt buộc: *"Stores that fixed this typically saw..."* — không dùng "You will get".

| Change Item | CR Uplift Midpoint |
|-------------|-------------------|
| Fix Your Product Photos | +0.3% |
| Give Buyers a Reason to Buy | +0.5% |
| Make Your Buy Button Stand Out | +0.3% |
| Show Buyers They Can Trust You | +0.4% |
| Make Your Description Easy to Read | +0.2% |
| Add new FAQ | +0.2% |

Midpoint = (low + high) ÷ 2. Hardcode Phase 1, replace bằng first-party data ở Phase 2.

---

### CR Uplift — Cách tính tổng (Summary card)

```
Est CR = Current CR + Σ(midpoints của tất cả items)
Không có cap — trust the benchmarks
```

Ví dụ seller CR = 1.4%:
```
1.4% + (0.3 + 0.5 + 0.3 + 0.4 + 0.2 + 0.2) = 1.4% + 1.9% = est. 3.3%
Display: "1.4% → est. 3.3%"
```

**Không dùng multiplicative compounding** — benchmark là absolute uplift đo cô lập,
không phải relative multiplier. Additive đơn giản hơn và đủ defensible cho Phase 1.

---

### Display Format — Per-Item CR Uplift

**Không hiển thị relative lift** (ví dụ "+21% CR") vì:
- Relative lift phụ thuộc current CR của từng seller → không hardcode được
- Seller đọc "+57% CR" có thể hiểu nhầm là cộng thẳng 57pp vào 1.4% → misread hợp lý

**Hai options đã thống nhất:**
- **Option A** (nếu không có traffic data): hiển thị resulting CR — `"est. 1.7% CR after this fix"`
- **Option B** (nếu có traffic data): đổi sang orders language — `"+3 more buyers per 100 visitors"`

Format summary vẫn giữ: `"1.4% → est. 3.3%"` — không hiển thị relative lift ở summary.

---

### Research Keywords — Tìm citation cho benchmark numbers

Khi cần validate con số với PM/stakeholder, tìm theo keywords:

| Category | Keywords |
|---|---|
| Gallery | "product image quality conversion rate study" |
| Value prop | "above the fold conversion rate impact" |
| CTA | "single CTA vs multiple CTA conversion" |
| Trust signals | "trust badges conversion rate study" |
| Description | "product description format conversion" |
| FAQ | "FAQ section conversion rate ecommerce" |

Sources tier 1: Baymard Institute, Nielsen Norman Group, CXL (cxl.com/blog)
Sources tier 2: VWO case studies, Optimizely Insights, Google Think with Google

**Khi đọc research:** phần lớn báo cáo relative lift (%). Convert về absolute: `absolute = baseline_CR × relative_lift%`

---

### AI Execution State — Animation Spec

Màn hình sau khi user confirm apply changes. Layout giữ nguyên split panel.

**Left panel — 3 states per item:**

| State | Visual |
|---|---|
| Pending | Gray circle outline, text muted, no animation |
| Processing | Purple-cyan gradient spinner, card có purple left border + pulse glow, label "AI is working..." |
| Done | Green checkmark với scale-in pop animation, card có green left border |

**Preview space — per-element animation, 3 phases:**

- **Phase 1 — Scanning (500ms):** Purple outline glow + horizontal light beam sweep top-to-bottom trên element
- **Phase 2 — Generating:** Element replaced bằng AI skeleton state — purple shimmer (không dùng gray), text zones dùng typewriter streaming effect, floating chip `[◉ Fixing product photos...]`
- **Phase 3 — Reveal (400ms):** New content fade in với purple flash → scale 0.98→1.0

Global overlay: thin animated purple→cyan→purple gradient border quanh preview frame.

**AI color palette:** Primary `#7C3AED`, Cyan `#06B6D4`, Light purple `#EDE9FE`, Done green `#16A34A`
