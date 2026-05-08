# CR Flow — Handoff Document

---

## Product Context

**CR Flow** là tính năng trong AI-powered eCommerce page builder. User chọn một product page → AI analyze → đưa ra plan gồm các suggested changes để cải thiện Conversion Rate (CR).

Màn hình đang thiết kế: **CR Optimization Plan screen**
- LEFT PANEL (60%): Danh sách suggested changes, grouped by category
- RIGHT PANEL (40%): Live product page preview (sticky)

---

## Screen Structure

### Top of left panel
**Summary section** — hiển thị trước danh sách changes. Mục đích: user hiểu tình trạng page trong < 5 giây, đủ tự tin scroll xuống xem change items.

### Categories (theo thứ tự cố định)
Layout → Reusable elements → Above the fold → Buy area → Social proof → Product information

### Known Elements trên product page (vocabulary cố định, 12 elements)
Announcement bar · Header · Title & Short description · Pricing display · Trust badges · Policy · Q&A · Footer · Product gallery · Product details · UGC images · Review section with UGC

### Card Structure (mỗi suggested change)
- Title
- Description gồm 2 section: **CURRENT SITUATION** + **WHAT TO DO**

---

## Summary Section

### Vấn đề đã identify

**🔴 P0 — Misleading / mất tin tưởng**

| # | Vấn đề | Heuristic vi phạm |
|---|---|---|
| 1 | CR Score 42 hiển thị màu **xanh lá** — green = tốt, nhưng 42/100 là thấp → user không cảm nhận được urgency | #2 Match System & Real World |
| 2 | CR Score không có scale — 42/100? 42/50? Không có baseline, không biết tốt hay xấu | #1 Visibility of Status |
| 3 | Issues Found 11 không có severity — bao nhiêu critical? User không biết nên lo mức nào | #6 Recognition > Recall |

**🟡 P1 — Cản trở scan nhanh**

| # | Vấn đề |
|---|---|
| 4 | Conversion 1.4% không có benchmark (avg eCommerce ~2–3%) và không có "potential after fix" |
| 5 | AOV $49.99 không kết nối với action nào — raw data, không phải insight |
| 6 | Summary text chôn 3 điểm vấn đề trong paragraph — không scannable |
| 7 | Không có directional cue sau khi đọc xong Summary |

---

### Solutions đã chốt

#### CR Score
- Gauge bar thay vì số đơn thuần: track + fill % + label **Poor / Fair / Good / Great**
- Semantic color theo value (không bao giờ dùng green cho score thấp):
  - 0–40: red `#DC2626`
  - 41–60: amber `#D97706`
  - 61–80: blue `#2563EB`
  - 81–100: green `#16A34A`
- Label: "Conversion Score" (không dùng "CR Score" — jargon)

#### Summary text
- Bỏ paragraph chôn vùi → dùng pattern:
  ```
  "Your page loses buyers at 3 key points:"
  [First impression]  [Offer clarity]  [Trust signals]   ← chips màu red-tinted
  "Fixing these before the CTA area will have the highest impact."
  ```
- Directional cue cuối block: `↓  11 changes suggested — starting from High impact`

#### Metric row (3 blocks)

| Block | Value | Context layer cần thêm |
|---|---|---|
| CONVERSION | 1.4% | Benchmark: "Avg. eCommerce: 2–3%" + Potential: "↑ Up to 2.8% if fixed" (green) |
| AOV | $49.99 | Kết nối action: "Upsell opportunity in 2 changes" |
| ISSUES FOUND | 11 | Severity: `🔴 3 critical · 🟡 5 medium · ⚪ 3 low` + left border red 3px |

**Nguyên tắc:** Mỗi số phải là **insight**, không phải raw data. User nhìn vào phải biết phải cảm thấy gì và làm gì tiếp.

---

## Các vấn đề UX đã identify

### P0
1. Plan ↔ Preview bị tách rời — user không biết plan item tương ứng với vùng nào trên page
2. Wall of text — description quá nhiều text, user skip, không hiểu, không tự tin click Apply
3. Selection state vô hình — có "Apply selected" nhưng không rõ checkbox

### P1
4. Không có priority/impact ranking
5. Inconsistent labels trong description
6. User không biết có thể edit content trên card
7. CR Score không có context

---

## Solutions đã chốt

### Solution 1 — Plan ↔ Preview Visual Link

**Interaction:**
- **Hover card** → preview element tương ứng nhận blue outline 2px + label tag + auto-scroll tới element
- **Click card** → selected state + persistent highlight (outline đậm hơn, không mất khi bỏ hover)
- **Hover category header** → highlight tất cả elements thuộc category đó trên preview

**Mapping card → preview element:**
Mỗi change item link tới 1–3 elements từ vocabulary 12 elements cố định.
Vì vocabulary cố định, preview luôn biết zone nào dù element có tồn tại hay không.

**Xử lý element chưa tồn tại (INSERT):**
- Ghost zone: dashed outline + faded background + label "(not yet added)"
- Dot overlay: hollow style + icon "+" thay vì solid dot

**3 states của highlight:**

| State | Trigger | Preview |
|---|---|---|
| Idle | Không hover | Không highlight |
| Hover | Hover card | Blue outline 2px + label + scroll |
| Selected | Click card | Outline đậm 3px + persistent |

---

### Solution 2 — Giảm Cognitive Load (Text)

**Giữ nguyên layout:** Title + Description (gray area với CURRENT SITUATION + WHAT TO DO).
Không thêm button, không thêm expand, không đổi cấu trúc layout.

**Quy tắc rewriting content:**

**CURRENT SITUATION:**
- 1 câu duy nhất, ≤ 100 ký tự
- Bold phrase = tên element + vấn đề cụ thể (3–6 từ, nằm nửa đầu câu)
- Dùng → cho cause-effect
- Pattern: `[Element] **[core problem]** → [user consequence]`

**WHAT TO DO:**
- 3–5 bullets, không hơn
- Mỗi bullet ≤ 70 ký tự
- Bắt đầu bằng **bold action verb**: Thay / Thêm / Xóa / Di chuyển / Đồng bộ / Viết lại / Bỏ
- Dùng → cho replacement/result
- Dùng #1, #2, #3 thay vì "first", "second"
- Sort theo impact descending

**Symbols thay prose:**
- `→` = trở thành / thay bằng
- `+` = thêm mới
- `−` = loại bỏ
- `#1, #2` = vị trí thứ tự

**Kết quả:** ~800 ký tự → ~230 ký tự. Scan time: 25–30s → 5–7s.

---

### Solution 3 — Edit Affordance

Cơ chế: **Click-to-edit inline** (pattern Notion/Linear). Không có "edit mode" riêng.

**3 states của field:**
- **Idle:** text bình thường, không border
- **Hover:** background nhạt + cursor text + icon ✏️ mờ + dotted underline
- **Editing:** focus ring + character counter + hint "Enter to save · Esc to cancel"

**Editable fields:**
- Title: click → single-line input
- Description (gray area): click → textarea toàn block

---

## Card Types

### AI-generated card
- Có impact badge (🔴 High / 🟡 Medium / ⚪ Low)
- Description có CURRENT SITUATION + WHAT TO DO (format rewriting rules ở trên)
- Linked tới 1–3 elements → có highlight trên preview

### User-added card
- Không có location data → không có preview highlight
- Description = free text, show thẳng (không expand)
- Icon ✏️ thay category icon để phân biệt

**Một layout duy nhất cho cả 2 loại.** Các feature nâng cao (highlight, location) chỉ render khi data tồn tại.

---

## AI Content Generation Schema

```json
{
  "title": "string (≤8 words, action-oriented, no jargon)",
  "impact": "high | medium | low",
  "affectedElements": ["array, 1–3 items, from fixed 12-element list"],
  "currentSituation": {
    "text": "string (≤100 chars, 1 sentence, use →)",
    "boldPhrase": "string (3–6 words, must appear verbatim in text, = element + problem)"
  },
  "whatToDo": [
    {
      "verb": "string (1 action word only)",
      "detail": "string (≤70 chars, continues sentence after verb, use →)"
    }
  ]
}
```

**Validation rules — reject và regenerate nếu:**
- title > 8 words
- currentSituation.text > 100 chars hoặc > 1 sentence
- boldPhrase không xuất hiện verbatim trong text
- boldPhrase mô tả consequence thay vì root cause
- bất kỳ detail > 70 chars
- whatToDo có < 3 hoặc > 5 items
- verb nhiều hơn 1 từ
- title topic ≠ whatToDo topic → split thành 2 cards riêng

---

## Validated Examples

### Example 1
```json
{
  "title": "Clarify offers in announcement bar and pricing area",
  "impact": "high",
  "affectedElements": ["Announcement bar", "Pricing display"],
  "currentSituation": {
    "text": "Announcement bar and pricing area show no offer or discount → shopper doesn't know about promotions on first visit.",
    "boldPhrase": "pricing area show no offer or discount"
  },
  "whatToDo": [
    { "verb": "Replace", "detail": "announcement bar text → show active offer or deadline" },
    { "verb": "Add", "detail": "discount line near price → visible before scrolling" },
    { "verb": "Add", "detail": "urgency micro-copy near Buy Now → 'Offer ends today'" }
  ]
}
```

### Example 2
```json
{
  "title": "Clean up product gallery sequence",
  "impact": "medium",
  "affectedElements": ["Product gallery"],
  "currentSituation": {
    "text": "First gallery image is before/after with promotional badges → product looks like an ad, not a product.",
    "boldPhrase": "first gallery image is before/after with promotional badges"
  },
  "whatToDo": [
    { "verb": "Set", "detail": "image #1 → clean product shot, white background, no text or stickers" },
    { "verb": "Add", "detail": "images #2–4 → texture close-up, in-hand scale, lifestyle application" },
    { "verb": "Move", "detail": "before/after images → position #5+, never first" },
    { "verb": "Remove", "detail": "sale stickers + text overlays from all product photos" },
    { "verb": "Sync", "detail": "thumbnail crops → same square ratio, same padding" }
  ]
}
```

### Example 3
```json
{
  "title": "Add USP Hook + Benefit Summary",
  "impact": "high",
  "affectedElements": ["Title & Short description", "Pricing display"],
  "currentSituation": {
    "text": "Title and buy area show no benefit or result → user doesn't understand product value before scrolling.",
    "boldPhrase": "show no benefit or result"
  },
  "whatToDo": [
    { "verb": "Rewrite", "detail": "title → include result, e.g. '...Clears Oil & Tightens Pores'" },
    { "verb": "Add", "detail": "1 hook sentence below title → value in under 15 words" },
    { "verb": "Add", "detail": "3 benefit bullets above Add to Cart → pore cleanse, oil control, 10-min routine" },
    { "verb": "Write", "detail": "as live text → never embed text inside product images" }
  ]
}
```

---

## Key Decisions & Rationale

| Decision | Rationale |
|---|---|
| Giữ nguyên layout (title + description) | User đã quen, không cần học lại. Fix text, không fix structure |
| Không thêm expand button | Description ngắn sau khi rewrite → không cần ẩn content |
| Bold via JSON field, không dùng markdown | AI tự quyết markdown → inconsistent. Schema field → render chính xác 100% |
| 1 card layout cho cả AI và user-added | Đơn giản hóa mental model. Feature nâng cao tự ẩn khi thiếu data |
| Ghost zone cho INSERT changes | Element vocabulary cố định → luôn biết zone dù element chưa tồn tại |
| Split card khi title ≠ content | Tránh mislead user, giữ 1 card = 1 clear action |

---

## Open Questions

1. **Sticky bottom bar:** "Apply Selected Changes X/11" — checkbox mechanism chưa spec rõ (default all checked?)
2. **Impact badge:** v1 dùng High/Medium/Low. Nguồn data từ industry benchmark hay chỉ AI estimate?
3. **User-added card:** Khi user muốn link tới element — có "Link to element" button không?
4. **Category "Layout":** Không map tới element cụ thể nào — highlight toàn trang hay từng element bị ảnh hưởng?

---

*Last updated: 2026-05-08 — Added Summary section analysis & solutions*
