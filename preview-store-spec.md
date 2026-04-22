# Preview Store — Content & Behavior Specification
**Screen:** Store Preview với CR Audit Panel
**Business Model:** Dropship (cùng pipeline với loading-screen-spec-v2.md)
**Version:** 1.0

---

## 1. Mục đích màn hình

Màn hình này xuất hiện ngay sau khi user click CTA "Xem store của bạn →" từ Reveal State.

**Mục tiêu:** Biến trust được gieo ở loading screen thành trust có bằng chứng thị giác.

Loading screen đã primed user với 13 optimizations cụ thể. Khi họ vào store, não họ đang trong trạng thái **chủ động tìm kiếm** các element đó. Màn hình này phải cho họ tìm thấy — và đặt tên cho — từng thứ họ đang tìm.

**Cơ chế trust chính:** Recognition Loop
```
Loading screen nói "CTA button: contrast 5.2:1"
→ User vào store, thấy button nổi bật
→ Click annotation dot → "CTA Button · Contrast 5.2:1 ✓"
→ "Ồ, đúng là cái này họ vừa làm"
→ Trust được confirm, không phải claimed
```

Mỗi item trong loading script phải có annotation tương ứng trên store. Đây là sợi dây kết nối bắt buộc.

---

## 2. Layout tổng thể

```
┌─────────────────────────────────────────────────────────────┐
│  [Brand Name]  Homepage · PDP · Checkout  [CR 84/100 ████]  │  ← Top Bar
├──────────────────────────────────────┬──────────────────────┤
│                                      │                      │
│                                      │   CR Audit Panel     │
│         Store Preview                │                      │
│         (với annotation dots)        │   Current page:      │
│                                      │   Homepage (6 items) │
│                                      │                      │
│                                      │                      │
└──────────────────────────────────────┴──────────────────────┘
```

**Tỷ lệ split:** 65% preview / 35% panel

**Responsive:**
- Desktop: side-by-side như trên
- Tablet: preview full width, panel collapsed thành bottom drawer, expand khi user tap
- Mobile: không hỗ trợ preview — redirect sang "Mở trên desktop để xem đầy đủ"

---

## 3. Thành phần 1 — Top Bar

Persistent, không disappear khi scroll.

**Bố cục từ trái sang phải:**

```
[◀ Quay lại]  [Brand Name]  |  [Homepage]  [PDP]  [Checkout]  |  CR 84/100  Top 20%  |  [Publish →]
```

### 3a. Brand Name
- Hiển thị tên brand user đã điền
- Font: đủ lớn để user nhận ra "đây là store của mình"
- Không có link, không interactive

### 3b. Page Navigator
3 tab: **Homepage · PDP · Checkout** — đây là happy flow mua hàng

- Tab active được underline hoặc background highlight
- Click tab → smooth scroll store preview về đầu trang tương ứng
- Audit panel đồng thời cập nhật sang items của trang đó

Thứ tự là cố định: Homepage → PDP → Checkout. Đây là journey mua hàng, không phải sitemap.

### 3c. CR Score
- Hiển thị `84/100` — giữ nguyên số từ Reveal State
- Kèm pill text: `Top 20% Dropship`
- Màu fill bar hoặc ring (không dùng màu cảnh báo)
- Score này là tổng thể — không thay đổi khi switch trang

**Tại sao giữ score persistent:**
User cần anchor point liên tục. Score biến mất = user bắt đầu quên, doubt trở lại.

### 3d. CTA Publish
- Nút "Publish →" ở góc phải
- State: disabled với tooltip "Xem hết 3 trang để mở khóa" cho đến khi user đã visit đủ Homepage + PDP + Checkout
- Sau khi đủ: enabled, màu primary

**Lý do gate Publish sau khi xem đủ 3 trang:**
Tăng chance user thấy đủ audit insights. User hiểu store của họ trước khi publish = giảm churn sớm.

---

## 4. Thành phần 2 — Store Preview Area

### 4a. Render
Store preview render như embedded browser. User có thể scroll tự do trong frame.

**Trạng thái ban đầu:** Homepage, scroll position = top.

### 4b. Annotation Dots
Các điểm tròn nhỏ đặt trên các element đã được optimize. Là bridge giữa loading script và store thực tế.

**Appearance:**
- Circle nhỏ, numbered (1–13 theo thứ tự loading script)
- Màu: primary accent của sản phẩm, không đỏ/cam
- Subtle pulse animation để attract attention khi mới load
- Không che nội dung — đặt ở góc hoặc cạnh element, không center

**Behavior:**
- Default: visible
- Hover dot → dot expand, panel scroll đến item tương ứng và highlight
- Click dot → panel expand item đó, show chi tiết Level 2-3
- Toggle "Ẩn annotations" ở top bar nếu user muốn xem store clean

**Trạng thái dot:**
- **Chưa xem:** Filled circle, số bên trong
- **Đã hover/click:** Filled circle + checkmark thay số
- **Tất cả đã xem:** Subtle congratulation state trên panel

### 4c. Annotation Map theo trang

**Homepage (Items 1–6):**
| Item | Element trên store | Vị trí dot |
|------|-------------------|------------|
| 1 | Template tổng thể | Top-left corner của hero |
| 2 | Layout structure | Top-right của page |
| 3 | Hero headline | Cạnh headline text |
| 4 | CTA button chính | Góc phải nút |
| 5 | Shipping estimate text | Cạnh dòng text |
| 6 | Trust badges row | Góc phải badge đầu tiên |

**PDP (Items 7–10):**
| Item | Element trên store | Vị trí dot |
|------|-------------------|------------|
| 7 | Price với gạch ngang | Cạnh giá gốc |
| 8 | Sticky ATC bar | Góc phải sticky bar |
| 9 | Stock indicator | Cạnh "Còn X sản phẩm" |
| 10 | Review stars gần giá | Cạnh star rating |

**Checkout (Items 11–13):**
| Item | Element trên store | Vị trí dot |
|------|-------------------|------------|
| 11 | Form fields | Cạnh form |
| 12 | Progress bar | Cạnh progress indicator |
| 13 | Trust badges + payment logos | Cạnh payment section |

---

## 5. Thành phần 3 — CR Audit Panel

### 5a. Header Panel
```
CR Audit · Homepage
6 optimizations applied
```
Cập nhật tự động khi user switch trang.

### 5b. Audit Items
Mỗi item gồm 3 level, expand dần:

**Level 1 — Collapsed (default):**
```
✓  [Số]  Tiêu đề từ loading script
```

**Level 2 — Hover:**
```
✓  [Số]  Tiêu đề từ loading script
         Giải thích tại sao quan trọng với CR
```

**Level 3 — Click:**
```
✓  [Số]  Tiêu đề từ loading script
         Giải thích tại sao quan trọng với CR
         
         Đã áp dụng:
         [Chi tiết cụ thể hơn về implementation]
         
         Benchmark: [So sánh với store cùng model]
```

**Trạng thái item:**
- `✓` xanh: đã xem (user đã hover hoặc click dot tương ứng)
- `●` pulse: chưa xem
- Highlight border: khi user hover dot tương ứng trên preview

### 5c. Panel Footer — sau khi user xem hết 3 trang

```
┌────────────────────────────────────┐
│  13 tối ưu CR đã được áp dụng      │
│  CR Score: 84/100 · Top 20%        │
│                                    │
│  2 cơ hội cải thiện:               │
│  → Hero image chưa tối ưu mobile   │
│    +3–5% mobile conversion nếu fix │
│  → Thiếu exit-intent popup         │
│    Recover ~8% abandoning visitors │
│                                    │
│  [Bắt đầu chỉnh sửa →]            │
└────────────────────────────────────┘
```

**Top 2 điểm yếu:** Phải là actionable, specific, không generic. Mỗi điểm có ước tính impact:
```
→ Hero image chưa tối ưu mobile → +3–5% mobile conversion nếu fix
→ Thiếu exit-intent popup → Recover ~8% abandoning visitors
```

---

## 6. Interaction Model hoàn chỉnh

### 6a. Bidirectional linking (quan trọng nhất)
Hai chiều phải hoạt động đồng thời:

**Từ panel → store:**
- Hover item trong panel → corresponding dot trên store pulse + highlight
- Click item → store scroll đến element đó + dot mở rộng + highlight element với border

**Từ store → panel:**
- Hover dot → panel scroll đến item tương ứng + item highlight
- Click dot → panel expand item đó, show Level 3 details

### 6b. Page switching
User click tab (Homepage / PDP / Checkout):
1. Store preview animate scroll sang trang mới (không hard cut)
2. Annotation dots fade out → trang mới dots fade in
3. Panel header cập nhật: "CR Audit · PDP"
4. Panel items cập nhật sang items của trang đó
5. Items đã xem ở trang trước giữ nguyên trạng thái ✓

### 6c. Progress tracking
- Top bar hiển thị subtle progress: `Đã xem: 2/3 trang`
- Sau khi xem đủ 3 trang → Publish button enable
- Panel footer Flow Score hiện ra

### 6d. Toggle annotations
Button nhỏ ở top bar: `[● Ẩn annotations]`
- Click → tất cả dots biến mất, panel vẫn hiển thị
- User có thể xem store clean như buyer thực sự sẽ thấy
- Click lại → dots trở lại
- Đây là feature quan trọng: cho user trải nghiệm cả hai POV (as owner với annotations, as buyer không có annotations)

---

## 7. Audit Script chi tiết — Level 3 content

Level 1 và 2 đã có từ loading-screen-spec-v2.md. Đây là Level 3 bổ sung cho mỗi item:

### Homepage

**Item 3 — Hero section**
- Level 3: "Headline đặt ở vị trí F-pattern hotspot. Value prop xuất hiện trong viewport đầu tiên, không cần scroll."
- Benchmark: "Top 25% Dropship stores — 68% stores để value prop below-the-fold"

**Item 4 — CTA button**
- Level 3: "Màu button tạo contrast 5.2:1 với nền. Đạt WCAG AA. Size tối thiểu 44×44px cho touch target."
- Benchmark: "34% Dropship stores có button contrast dưới 3:1 — không đạt threshold click-through tối ưu"

**Item 5 — Shipping estimate**
- Level 3: '"Nhận hàng trong 7–12 ngày" đặt trong 200px từ CTA button. Đo bằng pixel proximity.'
- Benchmark: "Shopify data: stores với shipping estimate gần CTA có CTR cao hơn 22%"

**Item 6 — Trust badges**
- Level 3: "4 badges: Secure Payment · Free Return · Tracked Shipping · 24/7 Support. Thứ tự theo mức lo ngại của buyer Dropship."
- Benchmark: "Baymard Institute: 61% buyers abandon vì thiếu trust signals tại decision point"

### PDP

**Item 7 — Price anchoring**
- Level 3: "Giá gốc gạch ngang ở trên, giá sale ở dưới lớn hơn. Khoảng cách đủ để mắt nhận ra diff ngay."
- Benchmark: "Price anchor tăng perceived value trung bình 17% — đặc biệt với impulse purchase"

**Item 8 — Sticky ATC bar**
- Level 3: "Bar xuất hiện sau khi user scroll qua hero image. Chứa: product name, price, ATC button. Không che review content."
- Benchmark: "Sticky ATC tăng add-to-cart rate 8–15% trên stores có long-form PDP"

**Item 9 — Stock indicator**
- Level 3: '"Còn 7 sản phẩm" đặt trong 80px từ ATC button. Text màu warning nhẹ (không đỏ cấp bách — cân bằng urgency và trust).'
- Benchmark: "Scarcity signal tăng conversion ~12% — hiệu quả nhất với new visitors"

**Item 10 — Review proximity**
- Level 3: "Star rating và số review đặt ngay dưới product title, trước giá. Eye-tracking flow: Title → Stars → Price → ATC."
- Benchmark: "Review gần giá giảm price objection 19% so với review đặt cuối trang"

### Checkout

**Item 11 — Form rút gọn**
- Level 3: "7 fields: Email · Name · Address · City · Province · Postal · Phone. Loại bỏ: Company, Address Line 2 (optional → auto-hidden), Birthday."
- Benchmark: "Baymard: mỗi field thừa tăng abandon 10%. 7 fields vs 12 fields = ~50% reduction in field-induced abandon"

**Item 12 — Progress bar**
- Level 3: "3 bước: Thông tin · Vận chuyển · Thanh toán. Bước hiện tại highlighted. Bước trước có dấu ✓."
- Benchmark: "Progress indicator giảm drop-off giữa chừng 18% — buyer biết còn bao xa là commit"

**Item 13 — Trust tại payment**
- Level 3: "Payment logos (Visa, Mastercard, PayPal) + lock icon đặt ngay trên nút thanh toán. Không ở footer."
- Benchmark: "Payment-adjacent trust signals giảm abandon tại bước thanh toán ~15% — đây là highest-anxiety moment"

---

## 8. Reveal State — sau khi xem hết 3 trang

Sau khi user đã visit đủ Homepage + PDP + Checkout, panel footer xuất hiện summary CR Score và 2 cơ hội cải thiện.

**Đồng thời:** Top bar Publish button chuyển từ disabled → enabled với subtle animation.

**Không có modal, không có confetti, không có interruption.** User vẫn đang trong preview — việc Publish button enable là signal tự nhiên rằng họ đã sẵn sàng.

---

## 9. Micro-copy

| Vị trí | Copy |
|--------|------|
| Panel header | `CR Audit · Homepage · 6 optimizations` |
| Item chưa xem | `●  [Tiêu đề]` |
| Item đã xem | `✓  [Tiêu đề]` |
| Toggle annotations on | `● Ẩn annotations` |
| Toggle annotations off | `○ Hiện annotations` |
| Publish disabled | `Xem hết 3 trang để publish` |
| Publish enabled | `Publish store →` |
| Footer summary | `13 tối ưu CR đã được áp dụng · CR Score: 84/100` |
| Footer điểm yếu header | `2 cơ hội cải thiện` |
| Footer điểm yếu CTA | `Bắt đầu chỉnh sửa →` |

**Tone cho Level 3 content:**
Giống Loading Screen — chuyên gia kỹ thuật, không phải marketing. Dùng số liệu, cite nguồn khi có.

---

## 10. Điều không làm

- **Không auto-scroll store** khi user chưa tương tác — để user tự khám phá, đừng dẫn tay
- **Không hiện popup "Bạn đã xem xong chưa?"** — patronizing, phá trải nghiệm
- **Không highlight tất cả dots cùng lúc ngay khi load** — quá nhiều attention cạnh tranh nhau
- **Không đặt Publish button ở panel** — Publish là quyết định của user, không phải bước kế tiếp tự nhiên của audit
- **Không gating từng trang nghiêm ngặt** — user có thể jump tab bất kỳ lúc nào, chỉ gate Publish sau khi đủ 3 trang
- **Không reset trạng thái ✓ khi switch trang** — user đã xem là đã xem, không bắt xem lại

---

## 11. Edge cases

**User ngay lập tức click Publish mà không xem audit:**
→ Publish button disable cho đến khi visit đủ 3 trang. Không modal giải thích — tooltip đủ.

**User không click vào bất kỳ dot nào:**
→ Không vấn đề. Họ vẫn thấy store, vẫn thấy CR Score ở top bar, vẫn có đủ trust context. Audit là optional depth, không phải mandatory flow.

**Store preview chưa render xong:**
→ Shimmer loading trên preview area. Panel hiện items ngay lập tức (không cần chờ store render). Dots fade in sau khi preview đã stable.

**User muốn chia sẻ preview:**
→ "Copy link" button nhỏ trong preview area. Link share không có annotations — người nhận thấy store clean như buyer thực sự.

---

## 12. Connection với màn hình kế tiếp

Sau khi user click "Bắt đầu chỉnh sửa →" từ panel footer:
→ Vào **Guided Refinement** — AI đề xuất 3 việc có impact cao nhất theo thứ tự ưu tiên.

Top 2 điểm yếu từ Flow Score trở thành 2 trong 3 đề xuất đầu tiên của Guided Refinement. Sợi chỉ liên tục từ audit → refinement.
