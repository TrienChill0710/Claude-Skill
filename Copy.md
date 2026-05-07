# CR Flow — Conversation Log

---

## Turn 1 — User

**Context:**
Sau khi user chọn dùng AI để analyze một product page bất kỳ thì AI sẽ phân tích và đưa ra plan để giúp cải thiện CR cho product page đó
- Đây là màn detail plan mục đích là user sẽ xem chi tiết các phân tích vấn đề hiện tại mà giao diện của product page đang gặp phải và từ đó AI đề xuất các thay đổi. User sẽ xem đánh giá, có thể sửa đổi thêm theo ý và click apply change khi đó AI sẽ thực thi vào giao diện để có kết quả tối ưu CR hơn

**Spec màn hình:**
1. Hiển thị mục Summary bao gồm: Summary text, Conversion rate, AOV, Issue found, CR score
2. Hiển thị các mục Suggested changes theo Category: Layout, Reusable elements, Above the fold, Buy area, Social proof, Product information
3. Mỗi suggested change gồm: Title, Current situation, What to do
4. User có thể Tạo thêm hoặc Sửa Change item
5. Ở dưới cùng có button "Apply selected changes" — floatable khi scroll

**Yêu cầu:** Đọc CLAUDE.md và dùng các skill để đánh giá UI hiện tại, sau đó đưa ra các solution cải thiện UX. Insight: User rất lười đọc text, cần hiểu issue ở đâu và solution như thế nào trước khi quyết định.

---

## Turn 1 — Assistant

### Đánh giá UI hiện tại — màn CR Optimization Proposal

Áp dụng **Judge UI** + **Don't Make Me Think** + **Hick's Law** + **10 Heuristics**

**Bước 1 — Context & Mental Model**

Task của user: Review plan AI gen → quyết định change nào áp dụng → click Apply.

User cần gì để tự tin click Apply?
1. Hiểu vấn đề ở ĐÂU trên page (visual location)
2. Hiểu sẽ thay đổi thành cái gì (before/after)
3. Hiểu tại sao change này quan trọng (impact)

User ưu tiên **sự tự tin > tốc độ** — nhưng lười đọc → cần visual nhanh, không phải text dài.

---

**Bước 2 — Vấn đề chính**

🔴 **P0 — Không đạt mức Usable**

| # | Vấn đề | Heuristic vi phạm |
|---|---|---|
| 1 | Plan ↔ Preview bị tách rời — không có visual link | #6 Recognition vs Recall |
| 2 | Wall of text — Mỗi block có 5-7 bullet dày đặc | DMMT #1 |
| 3 | Selection state vô hình — Button "Apply selected" nhưng không thấy checkbox | #1 Visibility of Status |
| 4 | Issues found = 11 nhưng count change item ≠ 11 | #4 Consistency |

🟡 **P1 — Cản trở quyết định**

| # | Vấn đề |
|---|---|
| 5 | Không có priority/impact ranking — tất cả change trông equal |
| 6 | Inconsistent labels — "PHẢI LÀM GÌ" vs "CÁCH THỰC HIỆN" vs "TÌNH TRẠNG HIỆN TẠI" |
| 7 | Affordance edit ẩn — Title không lộ là editable |
| 8 | Category headings nhỏ/mờ — không tạo orientation rõ |
| 9 | CR Score 42 — không có context (42/100? tốt hay xấu?) |

---

**Bước 3 — Solution đề xuất**

**Giải pháp 1: Visual link Plan ↔ Preview (impact cao nhất)**
Mỗi change item có một chấm số overlay trực tiếp lên vị trí tương ứng trên product preview. Hover block trái → highlight vùng phải + scroll preview tới đó.

**Giải pháp 2: Card scannable thay wall of text**
```
┌─────────────────────────────────────────┐
│ ☑ [Icon] TITLE — ngắn, action-oriented │
│ +X% CR uplift est.    [Edit] [Delete]  │
├─────────────────────────────────────────┤
│  ❌ Hiện tại:  1 dòng tóm tắt vấn đề    │
│  ✅ Đổi thành: 1 dòng tóm tắt giải pháp │
│  ▼ Xem chi tiết (collapse mặc định)    │
└─────────────────────────────────────────┘
```

**Giải pháp 3: Selection rõ ràng + impact rollup**
- Mỗi block có checkbox đầu (default checked)
- Sticky bottom bar: "Apply 8 / 11 changes — Est. CR: 42 → 58"

**Giải pháp 4: Group có hierarchy, không equal**
- Category header: `▼ ABOVE THE FOLD · 3 changes · High impact`
- Sort theo impact descending
- Top 3 change có badge "Recommended"

**Giải pháp 5: Polish nhỏ**
- Đồng nhất label: "Current situation" / "What to do"
- Title editable: hover hiện icon ✏️
- CR score 42: thêm gauge/scale + context
- Fix mismatch issue count

**Ưu tiên implement:**
| Giai đoạn | Việc cần làm |
|---|---|
| Sprint 1 (must) | GP1 (visual link) + GP3 (selection + impact rollup) |
| Sprint 2 | GP2 (card scannable + before/after) |
| Sprint 3 | GP4 + GP5 |

---

## Turn 2 — User

Với giải pháp 2 hãy cho tôi ví dụ thực tế bạn sẽ thay đổi với ví dụ:
- Title: Củng cố Khung Đề nghị + Tính Cấp bách
- TÌNH TRẠNG HIỆN TẠI: Thanh thông báo ở trên cùng chỉ hiển thị "Thời gian hoàn trả 30 ngày." Người mua không thấy bất kỳ thông tin nào về ưu đãi hay giảm giá khi họ lần đầu truy cập vào trang. Khu vực giá không đề cập đến ưu đãi — người mua không biết có chương trình khuyến mãi trừ khi họ đã đọc kỹ giá.
- PHẢI LÀM GÌ: 5 bullet về product images — clean hero shot, sequence, remove badges, consistent thumbnails

---

## Turn 2 — Assistant

### Áp dụng Giải pháp 2 — Ví dụ thực tế

**Phát hiện vấn đề nội dung:**
Title "Củng cố Khung Đề nghị + Tính Cấp bách" không khớp với content (nói về product images). Title nên tách thành 2 change items riêng.

**Card redesign (collapsed):**
```
┌──────────────────────────────────────────────────────────────────┐
│ ☑  🖼️  Dọn lại bộ ảnh sản phẩm theo công thức   ⚡ +8% CR  ✏️🗑   │
│       hook → texture → scale → in-use                             │
├──────────────────────────────────────────────────────────────────┤
│  ❌  Hiện tại: Ảnh #1 đang là before/after có nhãn giảm giá       │
│  ✅  Sau: Sequence kể chuyện 5 ảnh, bỏ hết nhãn quảng cáo        │
│  📍  Ảnh hưởng tới: Product Gallery (5 ảnh thumbnail)  ↗ Xem    │
│  ▾ Xem 5 bước chi tiết                                           │
└──────────────────────────────────────────────────────────────────┘
```

**Card khi expand (bảng cấu trúc):**
```
Vị trí    Loại ảnh                    Trạng thái
#1        Product shot, nền trắng     Cần thay (đang là before/after)
#2        Close-up kết cấu            Cần thêm
#3        Cầm trên tay (scale)        Cần thêm
#4        Đang dùng sản phẩm          Cần thêm
#5+       Before/after comparison     Di chuyển từ #1 sang
```

**So sánh trước/sau:**
| Metric | Trước | Sau |
|---|---|---|
| Ký tự hiển thị ban đầu | ~580 | ~140 |
| Thời gian scan để hiểu | ~25-30s | ~5s |
| Visual link tới preview | Không | 📍 Xem trên trang |
| Selection state | Vô hình | ☑ rõ ràng |
| Impact ranking | Không | Badge +X% CR |

**Quy tắc rewrite content cho prompt AI:**
1. Title ≤ 8 từ, dạng action verb
2. Current situation = 1 câu, ≤ 20 từ
3. What-to-do summary = 1 câu, ≤ 25 từ
4. Detail steps có cấu trúc table/numbered
5. Gen kèm: estimated CR uplift (%), affected element location
6. Validate: title phải khớp với what-to-do — nếu lệch thì split thành 2 items

---

## Turn 3 — User

Về impact ranking dựa vào đâu để đưa ra con số này?

---

## Turn 3 — Assistant

### Impact Ranking — Cơ sở và Đề xuất

Số `+8% CR` ở ví dụ là placeholder demo UI, không có cơ sở. Hiển thị số giả = dark pattern.

**4 hướng để có con số:**

**Hướng 1 — Industry benchmark database:**
| Loại change | Range uplift | Nguồn |
|---|---|---|
| Thêm urgency/scarcity element | +2-9% | Baymard, ConvertKit |
| Cải thiện product photo (hero shot sạch) | +5-12% | Baymard #213 |
| Đơn giản hóa CTA / 1 primary action | +10-30% | Nielsen Norman, GoodUI |
| Thêm trust badge cạnh CTA | +1-15% | Baymard checkout study |

**Hướng 2 — Tiered impact (không số, chỉ level):**
- 🔴 High impact
- 🟡 Medium impact
- ⚪ Low impact

**Hướng 3 — ICE/PIE scoring:** Impact + Confidence + Ease → tổng hợp score /10

**Hướng 4 — Real data từ platform** (cần tích lũy N stores qua thời gian)

**Đề xuất roadmap:**
| Giai đoạn | Hiển thị gì |
|---|---|
| v1 (launch) | 🔴 High / 🟡 Medium / ⚪ Low |
| v1.5 | Range từ industry research + tooltip nguồn |
| v2 | "Based on N stores" với data thật |

**Cảnh báo fake precision:**
- `+8.2% CR` per change là dark pattern
- Cộng dồn impact (6 changes × +8% ≠ +48% CR) — toán không đúng vì impact không additive
- Thà `High impact` đủ tốt còn hơn `+8.2%` sai

---

## Turn 4 — User

Tối ưu tương tự với phần này về solution 2:
- Title: Thêm USP Hook + Tóm tắt Lợi ích
- CÁCH THỰC HIỆN: Cập nhật tiêu đề sản phẩm để bao gồm kết quả, thêm 1 câu hook ngắn, thêm 3 điểm lợi ích ở trên nút Thêm vào Giỏ hàng, viết dưới dạng live text (không nhúng vào ảnh)

---

## Turn 4 — Assistant

### Áp dụng Giải pháp 2 — Ví dụ thứ 2

**Phát hiện vấn đề content:**
- Block này chỉ có "CÁCH THỰC HIỆN" — thiếu hẳn phần "TÌNH TRẠNG HIỆN TẠI"
- Title "Thêm USP Hook + Tóm tắt Lợi ích" dùng jargon (USP, hook)
- Prompt AI phải **enforce schema cố định** cho mọi change item

**Card redesign (collapsed):**
```
┌──────────────────────────────────────────────────────────────────┐
│ ☑  💬  Show 3 lợi ích cụ thể trước khi user click  🔴 High  ✏️🗑 │
│       Bổ sung hook + benefit bullets quanh khu mua hàng           │
├──────────────────────────────────────────────────────────────────┤
│  ❌  Hiện tại: Khu mua hàng chỉ có title + price + CTA, user     │
│               phải scroll mới hiểu sản phẩm làm gì cho da        │
│  ✅  Sau: Title rõ kết quả + 1 hook + 3 benefit ✓ ngay trên CTA  │
│  📍  Ảnh hưởng: Title · Dưới title · Trên Add to Cart  ↗ Xem    │
│  ▾ Xem 3 thay đổi cụ thể                                        │
└──────────────────────────────────────────────────────────────────┘
```

**Card khi expand (numbered list):**
```
① TITLE
  Hiện tại  →  Green Tea Clay Mask - deep pore cleanse, oil control & hydration | 40g
  Đổi thành →  Green Tea Clay Mask Stick — Cleanses Oil & Minimizes Pores
  Why: ngắn hơn, đặt kết quả lên trước, bỏ "| 40g" thừa

② DƯỚI TITLE (chèn mới)
  Hiện tại  →  ⊘ Trống
  Đổi thành →  "Giúp làm sạch bụi bẩn trong lỗ chân lông, giảm dầu thừa và để lại làn da mịn màng trong 10 phút"
  Why: 1 câu hook giải thích value trước khi user scroll

③ TRÊN ADD TO CART (chèn mới)
  Hiện tại  →  ⊘ Trống
  Đổi thành →  ✓ Làm sạch sâu lỗ chân lông
               ✓ Kiểm soát dầu
               ✓ Quy trình dễ dàng trong 10 phút
  Why: 3 benefit bullet ngay trước CTA → giảm do dự ở thời điểm quyết định

⚠️ Viết text trực tiếp (live text), KHÔNG nhúng vào hình ảnh
   Lý do: SEO + screen reader + dễ edit / A/B test
```

**Pattern chung cho mọi card — schema thống nhất:**
```
COLLAPSED: ☑ Title (≤8 từ) + Subtitle + Impact level + ❌/✅ 1 dòng + 📍 locations + toggle
EXPANDED:
  - Nhiều vị trí → Bảng (Vị trí · Hiện tại · Đổi thành)
  - Có sequence → Numbered ①②③
  - Quy tắc chung → Section ⚠️ riêng
  - Mỗi mục có Why: 1 dòng
```

**Prompt AI cần enforce:**
1. `currentSituation` ≤ 25 từ
2. `afterApply` ≤ 25 từ
3. `affectedLocations` (array)
4. Title: action verb, ≤ 8 từ, không jargon
5. Impact: chỉ high/medium/low, không gen %
6. Validation: title phải khớp detail steps

---

## Turn 5 — User

Theo spec user sẽ có thể edit được toàn bộ nội dung theo format card cũ như title, description bao gồm current state và what to do. Vậy với solution mới này match phần edit như thế nào?

---

## Turn 5 — Assistant

### Edit affordance trong card design mới

**Nguyên tắc:** Click-to-edit inline (kiểu Notion/Linear/Figma). Mọi text nhìn thấy = sửa được. Không có "edit mode" riêng.

**Map field editable:**
| Field | Edit type | Constraint |
|---|---|---|
| Title | Single-line input | ≤ 80 ký tự |
| Subtitle | Single-line input | ≤ 120 ký tự |
| ❌ Current situation | Textarea (auto-grow) | ≤ 200 ký tự |
| ✅ After applying | Textarea (auto-grow) | ≤ 200 ký tự |
| Detail step text | Textarea per cell | Tự do |
| Why line | Single-line input | ≤ 100 ký tự |
| Impact level 🔴🟡⚪ | Dropdown | Read-only ở v1 |
| 📍 Affected locations | Read-only | Structural |

**3 states của field:**

State 1 — Idle: Text bình thường, không border
State 2 — Hover: Background nhạt (#F5F5F5) + cursor text + icon ✏️ mờ + dotted underline
State 3 — Editing:
```
┌─────────────────────────────────────────────────┐
│ Text đang edit▌                                  │
└─────────────────────────────────────────────────┘
Esc để huỷ · Enter để lưu              42 / 200
```

**Edit ở vùng đặc biệt:**

Bảng (block 1 — gallery): mỗi cell click-edit độc lập. "Trạng thái" → dropdown.
Numbered (block 2 — USP): mỗi step có 3 sub-field (Hiện tại / Đổi thành / Why) đều click-edit.

**Add / Remove sub-items:**
- Hover row → icon 🗑 xuất hiện phải
- Cuối list → "+ Thêm benefit / bước"

**Edge cases:**
- Card collapsed + click field → chỉ field đó edit, KHÔNG auto-expand
- User edit summary ≠ trigger AI re-gen detail steps
- Field trống không hợp lệ → khôi phục nội dung cũ + tooltip cảnh báo
- Edit ≠ unselect checkbox — 2 hành động độc lập

**Đề xuất bỏ icon ✏️ ở header card** — redundant với inline edit. Giữ lại chỉ 🗑.

**Mental model cuối cùng:** "Mọi chữ click được = sửa được" — quen từ Notion, Linear, GitHub issue title.

---

## Turn 6 — User

Hiện tại cơ chế sẽ là AI đọc phần what to do/những việc cần làm sau đó thực thi. Nếu giờ đổi format như concept 2 liệu có xảy ra vấn đề không?
Thêm nữa sau khi click xem chi tiết việc giải thích từng phần có hiện tại như thế nào và đổi thành như thế nào tốt dễ hiểu nhưng đặt câu hỏi ngược lại làm vậy lại thành rất nhiều text mà con người rất lười đọc text vậy thì có phải lại vẫn gặp vấn đề cũ không?

---

## Turn 6 — Assistant

### Câu 1: AI execution có vấn đề không?

**Không — thực ra chính xác hơn nếu làm đúng.**

Cần tách 2 layer:
- **DISPLAY LAYER** (cho user): Title, subtitle, ❌/✅, diff view, why
- **DATA LAYER** (cho AI execute): steps[], implementFlow per step, executionPayload structured

**JSON schema cho AI tiêu thụ:**
```json
{
  "id": "ch_002",
  "category": "above_the_fold",
  "impact": "high",
  "display": {
    "title": "Show 3 lợi ích cụ thể trước khi user click",
    "currentSummary": "Khu mua hàng chỉ có title + price + CTA...",
    "afterSummary": "Title rõ kết quả + 1 hook + 3 benefit ✓..."
  },
  "steps": [
    {
      "id": "step_1",
      "implementFlow": "title_short_description",
      "location": "product_title",
      "operation": "replace",
      "currentValue": "Green Tea Clay Mask - deep pore cleanse...",
      "newValue": "Green Tea Clay Mask Stick — Cleanses Oil & Minimizes Pores"
    },
    {
      "id": "step_2",
      "implementFlow": "title_short_description",
      "location": "below_title",
      "operation": "insert",
      "currentValue": null,
      "newValue": "Giúp làm sạch bụi bẩn trong lỗ chân lông..."
    },
    {
      "id": "step_3",
      "implementFlow": "pricing_display",
      "location": "above_add_to_cart",
      "operation": "insert",
      "newValue": ["Làm sạch sâu lỗ chân lông", "Kiểm soát dầu", "Quy trình dễ dàng trong 10 phút"]
    }
  ]
}
```

**Vì sao format này CẢI THIỆN AI execution:**
| Trước (parse bullet text) | Sau (structured steps) |
|---|---|
| AI phải đoán vị trí nào trên page | `location` field nói rõ |
| AI phải đoán operation | `operation` field nói rõ |
| implementFlow ở card-level → 1 pipeline | Per-step → route chính xác |
| User edit text → AI parse lại, có thể sai | User edit field cụ thể → AI execute đúng |
| 1 block có 3 vị trí → nhồi vào 1 pipeline | 3 step → 3 pipeline khác nhau |

---

### Câu 2: Detail view vẫn nhiều text — vẫn problem cũ?

**Đúng. Giải pháp: Diff view kiểu GitHub thay text description.**

**Đề xuất detail view mới:**
```
┌────────────────────────────────────────────────────────────┐
│  📌 Product title                              ⓘ Vì sao?  │
│  ─  Green Tea Clay Mask - deep pore cleanse,              │
│     oil control & hydration | 40g                          │
│  +  Green Tea Clay Mask Stick — Cleanses Oil              │
│     & Minimizes Pores                                      │
│                                                            │
│  📌 Dưới title  (mới)                          ⓘ Vì sao?  │
│  +  "Giúp làm sạch bụi bẩn trong lỗ chân lông..."         │
│                                                            │
│  📌 Trên Add to Cart  (mới)                    ⓘ Vì sao?  │
│  +  ✓ Làm sạch sâu lỗ chân lông                           │
│  +  ✓ Kiểm soát dầu                                       │
│  +  ✓ Quy trình dễ dàng trong 10 phút                     │
└────────────────────────────────────────────────────────────┘
```

- `─` đỏ (struck-through) = text cũ bị thay
- `+` xanh = text mới
- Why: on-demand qua tooltip ⓘ
- "(mới)" badge = insert chưa tồn tại trước đây

**So sánh khối lượng đọc:**
| | Visible text |
|---|---|
| Card detail format cũ (bullet) | ~580 ký tự |
| Card detail Hiện tại/Đổi thành/Why | ~620 ký tự |
| **Card detail diff view** | **~340 ký tự** |

**Tăng cấp: Visual preview side-by-side** — wireframe mini HIỆN TẠI vs SAU KHI ÁP DỤNG

**Tăng cấp tối đa: Click 📍 → highlight + animate trên preview chính** — khử luôn detail view

**3 layer giảm dần text:**
| Layer | Cách hiển thị | Dành cho |
|---|---|---|
| Card collapsed (default) | ❌/✅ 1 dòng + 📍 link | 80% user |
| Click 📍 / toggle preview | Highlight + after-state render | 15% user |
| Expand ▾ Xem chi tiết | Diff view kiểu Git + Why ⓘ on-demand | 5% user |

**Đề xuất build:**
| Phase | Build gì |
|---|---|
| v1 | Card collapsed + diff view text-based |
| v1.5 | Toggle "Current / After" trên preview + click 📍 highlight |
| v2 | Wireframe mini side-by-side trong detail |

---

## Turn 7 — User

Pipeline bạn nhắc đến là gì? Diff view? Text diff? Pattern diff?

---

## Turn 7 — Assistant

### Pipeline là gì?

Khi AI "Apply" một change, mỗi loại thay đổi cần một quy trình xử lý khác nhau:

```
Change: Sửa title          →  Pipeline Title & Description
Change: Sửa gallery ảnh    →  Pipeline Product Gallery
Change: Thêm Q&A           →  Pipeline Q&A Block
Change: Sửa announcement   →  Pipeline Announcement Bar
```

Mỗi pipeline = 1 bộ prompt + logic riêng để AI biết chỉnh đúng vùng trên trang.

### Diff view là gì?

Cách hiển thị sự thay đổi — cái gì mất, cái gì thêm — bằng mắt không cần đọc giải thích. Pattern từ GitHub, Google Docs:

```
─  Green Tea Clay Mask - deep pore cleanse, oil control | 40g
+  Green Tea Clay Mask Stick — Cleanses Oil & Minimizes Pores
```

- `─` màu đỏ = text cũ bị thay
- `+` màu xanh = text mới

Thay vì viết "Hiện tại X, đổi thành Y vì lý do Z" — user đọc 3 dòng hiểu ngay bằng mắt.

---

## Turn 8 — User

Tôi nghĩ phương án Đề xuất detail view mới — Diff view kiểu GitHub này oke. Hãy giúp tôi viết 1 prompt về phương án này với ví dụ hiện tại để tôi đưa cho AI gen UI giúp trực quan về solution 2 kết hợp diff view. Nhớ thêm phần interaction liên quan đến edit title và description bao gồm các phần có thể edit được.

---

## Turn 8 — Assistant

### Prompt cho AI gen UI

````
Design a UI component for a "CR Optimization Plan" screen inside an AI-powered eCommerce page builder.

---

## SCREEN CONTEXT

Split layout:
- LEFT PANEL (60%): Plan panel — scrollable list of AI-suggested changes
- RIGHT PANEL (40%): Live product page preview — sticky

At the top of the left panel: Summary section with CR Score (42/100), Conversion Rate (1.4%), AOV ($49.99), Issues Found (11), and a 1-paragraph summary text.

Below summary: Change items grouped by category labels (ABOVE THE FOLD, KHU VỰC MUA HÀNG, BẰNG CHỨNG XÃ HỘI, THÔNG TIN SẢN PHẨM).

At the bottom: Sticky floating bar with "Apply Selected Changes" CTA button, showing count of selected items.

---

## CORE COMPONENT: CHANGE ITEM CARD

Each card has 3 states: Collapsed (default), Expanded (diff view), Editing.

---

### STATE 1 — COLLAPSED (default)

Design specs:
- Checkbox [✓] on far left — checked by default
- Category icon (💬 for copy/text, 🖼️ for image, 🛒 for buy area)
- Title: 600 weight, 15px
- Subtitle below title: 400 weight, 13px, muted color
- Impact badge: pill shape — 🔴 High (red), 🟡 Medium (yellow), ⚪ Low (gray) — top right
- Delete icon 🗑 far right, only visible on card hover
- ❌ row: light red-tinted text, 1 line max, 13px
- ✅ row: light green-tinted text, 1 line max, 13px
- 📍 row: gray 12px, inline tag-style chips for locations, small link "↗ Xem trên trang"
- Expand toggle: "▾ Xem N thay đổi cụ thể" — ghost button
- Card border: 1px solid #E5E7EB, radius 8px, white background
- Unchecked state: card gets 40% opacity

---

### STATE 2 — EXPANDED (diff view)

Clicking the expand toggle reveals diff section:

- `─` prefix + red background (#FFF1F0), red text (#CF1322), strikethrough — removed/replaced text
- `+` prefix + green background (#F6FFED), green text (#389E0D) — new/replacement text
- Location label (📌 Product title) in small caps, gray, 11px — section header
- "(mới)" badge in blue next to location name if it's an insert
- [ⓘ Vì sao?] — small ghost button, click shows tooltip with 1-line reason
- Divider separates collapsed content from diff section

---

### STATE 3 — EDITING (click-to-edit inline)

**Hover affordance:**
- Background → very light gray (#F9FAFB)
- Cursor → text cursor
- Small ✏️ icon at end of text, 60% opacity
- Dotted underline beneath text

**Active edit state:**
- Input/textarea with #6366F1 focus ring
- Character counter bottom-right
- "Enter để lưu  ·  Esc để huỷ" hint text, gray 11px
- Auto-save on blur

**Editable fields:**
1. TITLE — single-line input, max 80 chars
2. SUBTITLE — single-line input, max 120 chars
3. ❌ CURRENT SITUATION — auto-grow textarea, max 200 chars
4. ✅ AFTER APPLYING — auto-grow textarea, max 200 chars
5. DIFF VIEW lines — each `+` or `─` line individually editable; hover shows ✏️
6. [ⓘ Vì sao?] tooltip content — editable inline within popover, max 100 chars

**Add/Remove diff items:**
- Hover diff section → [+ Thêm dòng] at bottom
- Hover diff line → [🗑] at end of line

**Read-only fields:**
- 📍 Affected location chips
- Impact level badge (🔴🟡⚪)
- Category icon

---

## FULL EXAMPLE DATA

Card Data:
- Checkbox: checked
- Icon: 💬
- Title: "Show 3 lợi ích cụ thể trước khi user click"
- Subtitle: "Bổ sung hook + benefit bullets quanh khu mua hàng"
- Impact: 🔴 High
- Current (1 line): "Khu mua hàng chỉ có title + price + nút CTA, user phải scroll mới hiểu sản phẩm làm gì"
- After (1 line): "Title rõ kết quả + 1 câu hook + 3 lợi ích ngay trên CTA → user hiểu value trong 3s"
- Affected locations: ["Product title", "Dưới title", "Trên Add to Cart"]

Diff content:

📌 Product title — REPLACE
─  Green Tea Clay Mask - deep pore cleanse, oil control & hydration | 40g
+  Green Tea Clay Mask Stick — Cleanses Oil & Minimizes Pores
ⓘ Vì sao? → "Ngắn hơn, đặt kết quả lên trước, bỏ thông số thừa"

📌 Dưới title — INSERT (mới)
+  "Giúp làm sạch bụi bẩn trong lỗ chân lông, giảm dầu thừa và để lại làn da mịn màng trong 10 phút"
ⓘ Vì sao? → "1 câu hook giải thích value trước khi user phải scroll"

📌 Trên Add to Cart — INSERT (mới)
+  ✓ Làm sạch sâu lỗ chân lông
+  ✓ Kiểm soát dầu
+  ✓ Quy trình dễ dàng trong 10 phút
ⓘ Vì sao? → "3 benefit bullets ngay trước CTA giảm do dự ở thời điểm quyết định"

---

## STICKY BOTTOM BAR

Fixed at bottom of left panel:
- Left: ghost input "Ask OptiAI to refine the plan..." with sparkle icon
- Right: primary CTA button dark/black, white text, "APPLY SELECTED CHANGES  8/11 →"
- White background, top border, subtle box shadow

---

## VISUAL STYLE

- Font: Inter
- CTA button: #111827 background, white text
- Diff green bg: #F0FDF4, text #15803D
- Diff red bg: #FEF2F2, text #991B1B, strikethrough
- Card bg: white, border #E5E7EB
- Category label: uppercase, 11px, #6B7280, letter-spacing 0.05em
- Border radius: 8px cards, 6px chips/badges
- Overall bg: #F9FAFB
- High badge: red-50 bg + red-700 text
- Medium badge: yellow-50 + yellow-700
- Low badge: gray-100 + gray-600

---

## WHAT TO SHOW

1. One card in COLLAPSED state (checked)
2. Same card in EXPANDED state (diff view visible)
3. One field (Title) in EDITING state — focus ring, character counter, hint text
4. Sticky bottom bar
5. One card in collapsed + unchecked state (40% opacity)
````

---

## Turn 9 — User

Tạo 1 file Copy.md và hãy copy lại toàn bộ conversation này vào file này cho tôi.

---

## Turn 9 — Assistant

*(File này — Copy.md — chứa toàn bộ conversation được tạo theo yêu cầu này.)*
