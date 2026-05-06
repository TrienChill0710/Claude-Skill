# Judge UI — Product Detail Screen

---

## Bước 1 — Context

| Item | Phân tích |
|---|---|
| **Task chính** | View → Edit → Understand performance → Take action (analyze/optimize) |
| **User profile** | Dropshipping seller, có thể nhiều store + nhiều product → cần scan nhanh |
| **Mental model** | "Product này tốt/xấu? Tại sao? Phải làm gì tiếp?" |
| **Ưu tiên** | Tự tin (cần evidence để decide) > Tốc độ |

---

## Bước 2 — Goal Achievement (5-level)

### 1. **Functional** ✅
Đầy đủ: edit info, preview, analyze entry point, action buttons.

### 2. **Reliable** ⚠️
Description hiển thị **duplicate content** (HEAT & COLD RESISTANT lặp 3 lần) → có thể là bug hoặc data issue, nhưng visual khiến user nghi ngờ độ tin cậy.

### 3. **Usable** ❌ (vấn đề chính)
**Goal "hiểu tại sao chưa bán tốt" KHÔNG đạt được** — đây là lỗi nghiêm trọng nhất:
- 3 metrics hiển thị **số trần trụi**, không biết tốt/xấu
- `$24.09 Revenue` — của period nào? hôm nay? tháng này? lifetime?
- Không có comparison, benchmark, trend
- Muốn diagnose → phải click AI card → thêm 1 step nữa

### 4. **Pleasurable** ⚠️
Layout cân đối nhưng cramped — preview panel ở image 1 nhồi nhét quá nhiều (countdown, stock, 2 CTA, color picker) trong width hẹp.

### 5. **Meaningful** — Chưa đủ để đánh giá

---

## Bước 3 — IA & Interaction Design Issues

### 🔴 Critical Issues

**1. Top bar — "Product name" trông như placeholder**
- Phải hiển thị tên thật ("Mini Wifi Wide Angle Camera")
- "Product name" generic làm screen trông như chưa load xong
- Vi phạm **#1 Visibility of System Status**

**2. Metric cards — không context**
```
Hiện tại:  Store CR  3.8%
Cần có:    Store CR  3.8%  ↓ -0.4% vs last week
                            Below industry avg (4.5%)
```
Vi phạm **#6 Recognition vs Recall** — user phải tự nhớ benchmark, không có visible info để so sánh.

**3. Action bar (top right) — 4 button đồng cấp**
Duplicate / View / Hide / View on catalog — tất cả cùng weight visual. Vi phạm **Hick's Law** + **#8 Aesthetic**.
- Nào là primary action?
- "View" và "View on catalog" trùng lặp về nghĩa
- Hide product = destructive nhưng không có visual warning

**4. AI card chiếm vị trí top — đúng hay sai?**
Goal là "view detail + understand why" → AI card *nên* nổi bật **NHƯNG** đang bị disconnect với metrics:
```
[ AI card: "Improve product page?" ]  ← lời đề nghị
[ Metrics: 3.8% / $24.09 / $48.09 ]   ← evidence
```
Phải **đảo logic**: cho user thấy *vấn đề trong metrics* trước, rồi AI card xuất hiện như *câu trả lời*.

### 🟡 Important Issues

**5. Terminology — jargon không phù hợp novice**
- **CR** (Conversion Rate) — viết tắt brand-specific
- **AOV** (Average Order Value) — OK nếu target audience là seller có kinh nghiệm
- **"Processing rate"** + "lower rate indicates high quality" — **phản trực giác** (thường rate cao = tốt). Đổi thành **"Quality Score"** + scale rõ ràng (0-100, higher = better)

**6. Description editor**
- Rich text editor full-feature có thể overkill — seller dropshipping ít khi cần `<code>` tag
- Editor height auto-grow khiến content list dài đẩy mọi thứ phía dưới xuống xa

**7. Preview panel (image 1) — quá tải trong 320px**
Trong khu hẹp đã chứa:
- Logo + search + cart
- Product image (chiếm ~30% chiều cao)
- Image gallery (4 thumbnails)
- Rating, name, price, badge
- Color picker
- Stock counter
- **Discount countdown** — urgency tactic, có thể dark pattern
- 2 CTAs (Add to Cart + Buy Now)

→ Vi phạm **#8 Minimalist** nghiêm trọng. Preview để **check design**, không phải replicate 100%.

**8. "Set as Home Page" cuối screen**
Out of context. Tại sao 1 product setting lại nằm ở footer? Vi phạm **#4 Consistency** + proximity grouping.

**9. Sidebar icons không có label**
8 icon không text → user phải memorize hoặc hover-and-wait. Vi phạm **#6 Recognition vs Recall**. Mobile user thì không có hover.

**10. Layout shift giữa 2 state**
- Expanded: "Product info" và "Product design" chia 2 column 50/50
- Collapsed: Cùng layout nhưng wider → "Product design" đột ngột thoáng hơn

→ Inconsistent. Section nào critical phải **giữ nguyên proportion**, không adapt theo space available.

### 🟢 Done well

✅ Collapse pattern (chevron + vertical PREVIEW label) — clear affordance
✅ AI card visual identity (gradient, sparkle) — nổi bật khỏi noise
✅ Field labels rõ ràng, input states proper
✅ Default tag với close icon — consistent removal pattern

---

## Khuyến nghị cải thiện

### 🎯 Priority 1 — Fix Goal Achievement

**A. Re-architect "Why not selling well?" zone**

Đổi từ:
```
[ AI Card ] → [ Metrics ] → [ Edit Forms ]
```

Thành:
```
[ Health Status Card ]              ← 1 sentence diagnosis
  "Conversion 23% below benchmark
   — likely caused by: weak headline,
   missing trust signals"
[ Detailed Metrics with context ]   ← evidence
[ AI Card as response ]             ← "Want to fix this? →"
[ Edit Forms ]
```

**B. Metrics with context**
Mỗi card thêm:
- Period selector (default: "Last 7 days")
- Delta arrow (↑ ↓)
- Benchmark line ("Industry avg: 4.5%")
- Status color (green/yellow/red dot)

**C. Top bar — show real product name**
Thay "Product name" bằng product thật + breadcrumb:
```
< Products / Dropship / Mini Wifi Wide Angle Camera
```

---

### 🎯 Priority 2 — Reduce Cognitive Load

**D. Action bar — establish hierarchy**
```
Primary:    [ View on catalog ↗ ]   ← solid button, brand color
Secondary:  [ Duplicate ] [ ⋯ More ]
                            └─ Hide product
                            └─ Export
                            └─ Delete
```

Gom `View` + `View on catalog` thành 1. `Hide` đẩy vào More menu (destructive nên ẩn bớt).

**E. Preview panel — declutter**
Bỏ countdown timer khỏi preview (đó là feature flag riêng, không phải core preview). Chỉ giữ:
- Image
- Title + price
- Rating
- 1 CTA chính

**F. Sidebar — add labels** (ít nhất khi expand) hoặc tooltip on hover delay 300ms.

---

### 🎯 Priority 3 — Polish

**G. "Processing rate" → "Quality Score"**
Đổi naming convention sang positive scale (0-100, higher = better) + visual indicator.

**H. Description editor**
- Collapse rich text toolbar khi không focus
- Set max-height + scroll inside (không push content xuống)
- Add "Format with AI" shortcut button

**I. "Set as Home Page" relocate**
Move vào "Product design" section hoặc settings drawer — không để standalone ở footer.

**J. Layout consistency**
Cố định ratio cho main content area (e.g. 60/40 split) bất kể preview state — section sizes không thay đổi đột ngột khi toggle preview.

---

## TL;DR

| Severity | Issue | Impact |
|---|---|---|
| 🔴 Critical | Metrics không context | Goal "hiểu tại sao" không đạt |
| 🔴 Critical | "Product name" placeholder | Trust |
| 🔴 Critical | Action buttons no hierarchy | Hick's Law |
| 🟡 High | Preview panel cramped | Cognitive overload |
| 🟡 High | Jargon (CR/Processing rate) | Onboarding friction |
| 🟢 Medium | Sidebar no labels | Recall load |
| 🟢 Medium | Layout shift on collapse | Spatial inconsistency |

> **One sentence**: Màn hình **chứa đủ feature** nhưng **fail ở goal** — user không tự diagnose được "tại sao chưa bán tốt" mà phải click thêm vào AI flow. Fix priority 1 (metrics with context + diagnosis card) sẽ unlock 80% giá trị màn hình này.
