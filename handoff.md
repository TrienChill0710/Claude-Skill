# Handoff Document — Onboarding Flow Brainstorm
**Project:** Web Builder / Store Builder SaaS
**Ngày cập nhật:** 2026-04-22
**Mục đích file:** Tóm tắt toàn bộ cuộc trò chuyện để agent mới tiếp tục mà không cần đọc lại lịch sử

---

## 1. Sản phẩm đang xây dựng là gì

Một **web builder** giúp merchant tạo store ecommerce nhanh, tập trung vào 3 business model:
- **Print on Demand (POD)**
- **General Dropship**
- **Niche Dropship**

**USP của sản phẩm:** AI giúp tăng CR (Conversion Rate) và AOV (Average Order Value) cho store.

**User goal:** Có một store chuyên nghiệp, CR/AOV tốt, nhanh chóng.

---

## 2. User Journey đã được thiết kế

Luồng đã thống nhất theo thứ tự:

1. **Landing Page** — User visit lần đầu
2. **Sign up + Điền thông tin cơ bản** — Brand name, business model, store goal
3. **Loading Screen** — Hệ thống gen store *(spec chi tiết tại `loading-screen-spec-v2.md`)*
4. **Store Screen** — User xem store đã được gen, với CR highlights + hover tooltip *(spec tại `store-screen-spec.md`)*
5. **Guided Refinement** — AI đề xuất 3 việc tiếp theo có impact cao nhất
6. **Publish** — CTA duy nhất "Publish store", sau đó có dashboard AI monitoring

---

## 3. Quyết định quan trọng đã được thống nhất

### Về template vs AI gen
- Backend thực tế dùng **template matching theo business model**, không AI gen thật
- Ngôn ngữ màn hình loading phải **trung thực**: nói thẳng "chọn template" thay vì "AI đang tạo store"
- Template IS the intelligence — trí tuệ nằm ở việc biết template nào phù hợp với business model nào

### Về trust problem
- Giải pháp trust không phải claim số liệu chung chung mà là **CR highlights cụ thể** trực tiếp trên store
- Mỗi element được optimize có highlight ring + badge "⚡ CR" + hover tooltip giải thích WHY + số liệu benchmark
- Format tooltip: *[Con số/nguyên lý] — [Hệ quả với buyer behavior]*
- Trust được build qua recognition: user đã nghe ở loading screen → vào store nhìn thấy đúng element đó

### Về Store Screen (thay thế "Preview Store + CR Audit Panel")
- Quyết định cuối: **không có sidebar panel**. Chỉ có store đầy đủ + highlights + tooltip on hover
- Đơn giản hơn, ít cognitive load hơn, buyer journey không bị interrupt
- Tooltip xuất hiện 150ms sau hover, dark background, 280–320px width
- 3 tab navigation: Homepage | Product Page | Checkout (theo happy flow mua hàng)

### Về Loading Screen
- **Không phải màn hình chờ** — là màn hình chứng minh năng lực
- Mỗi item trong loading phải: (1) nói hệ thống làm gì cụ thể + (2) giải thích tại sao quan trọng với CR
- Script 13 items, chia 6 giai đoạn, dropship-specific

---

## 4. Template đang dùng — Figma Reference

**File:** [Ecom] Trendie • General Dropship  
**Figma URL:** `https://www.figma.com/design/znvtVRAgOucsCoYMUBDHHS/-Ecom--Trendie-%E2%80%A2-General-Dropship`  
**Node Homepage:** `4002:1836` (HD Home frame)

### CR Analysis đã thực hiện — Homepage

Đã đọc và audit toàn bộ homepage của template. Kết quả:

**Điểm mạnh hiện có (giữ nguyên làm CR highlights):**
- Deal of the Week: countdown timer + anchor price ($90 → $45, 50% OFF) + scarcity ("Only 10 items left") + dual CTA (Add to cart + Buy now) → section CR tốt nhất trang
- Benefits bar: 3 trust signals ngay dưới hero (free shipping, international delivery, return policy)
- "Best Selling" label trên section → social proof signal
- Star rating + review count visible trên product cards
- SALES badge trên product cards

**Vấn đề cần fix trước khi dùng template (theo thứ tự ưu tiên):**

| # | Vấn đề | Severity |
|---|--------|----------|
| 1 | Review text không khớp product title trong "Customer Love Us" — placeholder data sai hoàn toàn | Destroy trust |
| 2 | Product cards không có anchor price (không có giá gốc gạch ngang) — mất perceived value của discount | High |
| 3 | "Deal of the Week" section đặt quá sâu — sau 4 collection sections, section CR tốt nhất bị chôn vùi | High |
| 4 | Hero CTA "SHOP NOW" quá generic — không có context value | Medium |
| 5 | Free shipping threshold $150 quá cao cho average Dropship order ($30–$80) | Medium |
| 6 | Announcement bar bị ẩn (visible: false) — real estate trust signal đang bỏ trống | Medium |
| 7 | "SALES" badge không show % discount — kém hiệu quả hơn "30% OFF" | Low |

**Chưa audit:** Product Page (PDP) và Checkout — cần làm tiếp ở session sau.

---

## 5. Files đã tạo

### `loading-screen-spec.md`
Spec đầy đủ cho loading screen, bao gồm layout suggestion. Dùng khi muốn có reference layout cụ thể.

### `loading-screen-spec-v2.md` ← **Dùng cái này để handoff cho AI designer**
Spec layout-free — chỉ có goal, content, behavior, script. Dùng khi muốn AI designer tự quyết định layout.

Nội dung v2 gồm:
- Mục đích màn hình
- 4 thành phần bắt buộc (Brand context, Tiến trình tổng thể, Activity log, Reveal State)
- Script 13 items đầy đủ cho Dropship
- Micro-copy guidelines + bảng "tránh/dùng"
- Timing table
- Điều không làm
- Edge cases (loading nhanh/chậm/lỗi)

### `store-screen-spec.md` ← **Spec màn hình sau loading**
Spec cho Store Screen — màn hình user xem store với CR highlights và hover tooltips.

Nội dung gồm:
- Layout: full-width store + tab bar (Homepage | Product Page | Checkout)
- Highlight system: border ring + glow + badge "⚡ CR" trên mỗi element được optimize
- Tooltip spec: visual, vị trí, timing, animation
- 13 tooltip contents đầy đủ (map 1:1 với 13 items trong loading script)
- Behavior: staggered animation khi load, bidirectional hover, page switching
- Điều không làm

### `preview-store-spec.md`
Spec cũ hơn, có cả sidebar audit panel. **Không dùng** — đã bị thay bởi `store-screen-spec.md` với approach đơn giản hơn.

---

## 6. Phần chưa làm — cần tiếp tục

### A. CR Analysis cho Product Page (PDP) — ưu tiên cao
Đã audit Homepage xong. Cần tiếp tục với PDP (node `1:2` trong Figma file).
Các element cần chú ý theo spec:
- Price anchoring
- Sticky ATC bar
- Stock indicator
- Review proximity to price

### B. CR Analysis cho Checkout — ưu tiên cao
Node `2489:4915` trong Figma file.
Các element cần chú ý:
- Form fields count
- Progress bar
- Trust badges gần payment button

### C. Store Screen — tooltip content cho PDP và Checkout
`store-screen-spec.md` đã có đủ 13 tooltips. Nhưng các tooltips hiện dùng placeholder element positions — cần verify lại vị trí badge sau khi xem PDP và Checkout thực tế trong Figma.

### D. Loading Screen spec cho POD và Niche Dropship
Hiện chỉ có spec cho General Dropship. POD và Niche Dropship cần script riêng vì pain point khác:
- POD: nhấn vào quality proof, mockup, return policy
- Niche Dropship: nhấn vào expertise signals, community proof

### E. Sign up / Onboarding form
Chưa spec màn hình điền thông tin (brand name, business model). Ghi chú: chỉ hỏi đủ để gen store, không hỏi thêm. Business model + Brand name là đủ.

---

## 7. Context bổ sung

- Business model được chọn ở sign up là: Print on Demand / General Dropship / Niche Dropship — không đi sâu vào ngành hàng cụ thể
- Benchmark CR tham khảo: POD 1.5–2.5% | General Dropship 1.8–3.2% | Niche Dropship 2.0–4.0%
- Giai đoạn đầu chưa có internal data → dùng industry benchmark (Shopify, Baymard Institute, Klaviyo) và cite source rõ ràng
- CLAUDE.md của project chứa các skill UX: Hick's Law, 10 Usability Heuristics, Don't Make Me Think, Judge UI — agent mới nên đọc file đó

---

## 8. Gợi ý bước tiếp theo hợp lý

Nếu muốn tiếp tục theo thứ tự logic:
1. **CR Analysis PDP** — đọc Figma node `1:2`, audit theo checklist (price anchor, sticky ATC, stock indicator, review placement)
2. **CR Analysis Checkout** — đọc Figma node `2489:4915`, audit form fields, progress bar, trust signals
3. **Cập nhật store-screen-spec.md** nếu element positions trong PDP/Checkout cần điều chỉnh
4. **Spec Guided Refinement screen** — màn hình sau Store Screen
5. **Loading screen cho POD và Niche Dropship**
6. **Spec Sign up / Onboarding form**
