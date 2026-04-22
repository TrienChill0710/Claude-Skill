# Loading Screen — Design Specification
**Screen:** Store Generation Loading Screen
**Business Model:** Dropship
**Version:** 1.0

---

## 1. Mục đích màn hình

Màn hình này xuất hiện sau khi user điền thông tin (brand name, business model) và nhấn "Tạo store". Hệ thống đang chọn template và áp dụng các tối ưu CR.

**Mục tiêu chính:** Không phải màn hình chờ. Đây là màn hình chứng minh năng lực của hệ thống. Khi user xem xong loading screen, họ phải cảm thấy: *"Hệ thống này thực sự hiểu conversion rate, không phải chỉ tạo template đẹp."*

**Cơ chế build trust:** Mỗi item xuất hiện trên screen phải làm đồng thời 2 việc:
1. Nói hệ thống đang làm **gì cụ thể** (hành động có tên, đặt tên được)
2. Giải thích ngắn **tại sao** hành động đó quan trọng với CR (con số hoặc nguyên lý)

Khi user vào store xong, họ sẽ nhận ra từng element đã được đề cập — trust được build retroactively.

---

## 2. Layout tổng thể

```
┌──────────────────────────────────────────────────────┐
│                                                      │
│   [Logo sản phẩm]                                    │
│                                                      │
│   Đang chuẩn bị store Dropship của bạn...           │
│   [Brand name của user]                              │
│                                                      │
│   ──────────────────────────────── [XX%]            │
│   [Progress bar fill animation]                      │
│                                                      │
│   ┌──────────────────────────────────────────┐      │
│   │  [Feed các items hoàn thành + đang chạy] │      │
│   └──────────────────────────────────────────┘      │
│                                                      │
└──────────────────────────────────────────────────────┘
```

**Bố cục:** Căn giữa màn hình. Nền tối hoặc nền sáng tối giản — không có distraction. Chỉ có loading content, không có navigation, không có button nào để click.

---

## 3. Các thành phần UI

### 3.1 Header
- **Headline:** `Đang chuẩn bị store Dropship của bạn...`
- **Sub-headline:** Hiển thị brand name user đã điền — ví dụ: `"TrendVibe Store"` — để tạo cảm giác cá nhân hóa
- Font: Lớn, clean, weight medium

### 3.2 Progress Bar
- **Style:** Full-width bar, fill animation từ trái sang phải
- **Label %:** Hiển thị số % bên phải bar, cập nhật realtime
- **Behavior:** Tiến trình tương quan với số items đã hoàn thành trong feed phía dưới
- **Không dùng** spinner vòng tròn — progress bar tuyến tính truyền đạt tiến độ rõ ràng hơn

### 3.3 Activity Feed (phần quan trọng nhất)

Đây là feed dọc hiển thị từng tối ưu đang/đã được áp dụng.

**Mỗi item trong feed có cấu trúc:**
```
[Icon trạng thái]  [Tiêu đề hành động]
                   [Giải thích ngắn — tại sao quan trọng với CR]
```

**3 trạng thái của mỗi item:**

| Trạng thái | Icon | Style |
|------------|------|-------|
| Đã hoàn thành | ✅ checkmark màu xanh | Text màu mặc định, opacity 100% |
| Đang chạy | ⟳ spinner xoay | Text màu accent (highlight), có subtle pulse animation |
| Chưa đến | — | Ẩn hoàn toàn, chưa render |

**Behavior:** Items xuất hiện tuần tự từ trên xuống. Item mới xuất hiện bằng fade-in nhẹ. Feed tự scroll để item đang chạy luôn visible.

---

## 4. Script đầy đủ — Business Model: Dropship

Tổng 13 items, chia 6 giai đoạn. Thời gian ước tính mỗi item: 1.5–2.5 giây. Tổng loading: ~25–35 giây.

---

### Giai đoạn 1 — Chọn nền tảng (2 items)

**Item 1**
> **Tiêu đề:** Chọn template Dropship tỷ lệ chuyển đổi cao nhất
> **Giải thích:** Template được chọn dựa trên cấu trúc đã được kiểm chứng với hàng ngàn Dropship stores

*Ghi chú cho designer: Đây là item duy nhất nhắc đến "template". Nói thẳng, không che giấu. Tạo trust ngay từ đầu bằng sự minh bạch.*

**Item 2**
> **Tiêu đề:** Nhận diện ngành hàng và đối tượng mua của bạn
> **Giải thích:** Store Dropship cần cấu trúc khác với POD hay niche store — buyer behavior khác nhau

---

### Giai đoạn 2 — First Impression (2 items)

**Item 3**
> **Tiêu đề:** Tối ưu hero section: Value proposition hiện trong 5 giây đầu
> **Giải thích:** 68% buyer quyết định ở lại hay rời đi trong khoảng này — mỗi giây đều tính

**Item 4**
> **Tiêu đề:** CTA button: Contrast ratio 5.2:1 với background
> **Giải thích:** Đạt ngưỡng tối ưu click-through — button mờ là nguyên nhân phổ biến nhất của low CTR

---

### Giai đoạn 3 — Trust Layer (2 items)

*Dropship buyer có 2 lo ngại chính: hàng có đến không, bao lâu. Giai đoạn này giải quyết cả 2.*

**Item 5**
> **Tiêu đề:** Thêm shipping estimate rõ ràng tại hero section
> **Giải thích:** "Nhận hàng trong X ngày" gần CTA chính — shipping time là rào cản mua #1 với Dropship buyer

**Item 6**
> **Tiêu đề:** Đặt 4 trust badges tại vị trí above-the-fold
> **Giải thích:** Secure Payment · Free Return · Tracked Shipping · 24/7 Support — giảm lo ngại trước khi buyer scroll xuống

---

### Giai đoạn 4 — Product Page (4 items)

*Đây là giai đoạn quan trọng nhất — nơi quyết định Add to Cart xảy ra.*

**Item 7**
> **Tiêu đề:** Price anchoring: Giá gốc gạch ngang cạnh giá sale
> **Giải thích:** Anchor price tạo perceived value — buyer cảm nhận "đang được deal" ngay cả khi không so sánh

**Item 8**
> **Tiêu đề:** Sticky Add-to-Cart bar khi buyer scroll xuống phần reviews
> **Giải thích:** 68% quyết định mua xảy ra sau khi đọc reviews — CTA phải luôn trong tầm với tại thời điểm đó

**Item 9**
> **Tiêu đề:** Urgency indicator: Số lượng tồn kho hiển thị gần CTA
> **Giải thích:** Scarcity signal tăng add-to-cart rate ~12% — đặc biệt hiệu quả với impulse purchase của Dropship

**Item 10**
> **Tiêu đề:** Review stars đặt cạnh giá, không đặt ở cuối trang
> **Giải thích:** Proximity của social proof và price giảm price objection — buyer nhìn giá, thấy luôn trust signal

---

### Giai đoạn 5 — Checkout (3 items)

**Item 11**
> **Tiêu đề:** Checkout form: Rút gọn xuống còn 7 fields thiết yếu
> **Giải thích:** Mỗi field thừa tăng abandon rate ~10% — fields không cần thiết là nguyên nhân abandon thầm lặng nhất

**Item 12**
> **Tiêu đề:** 3-step progress bar tại checkout
> **Giải thích:** Buyer biết mình đang ở bước nào, còn bao xa — giảm anxiety, giảm drop-off giữa chừng

**Item 13**
> **Tiêu đề:** Trust badge và payment logos ngay cạnh nút thanh toán
> **Giải thích:** Đây là high-anxiety moment — trust signals đặt đúng vị trí này giảm abandon ~15%

---

### Giai đoạn 6 — End State (Reveal)

Khi item 13 hoàn thành, progress bar đạt 100%, feed dừng lại ~1 giây, sau đó màn hình chuyển sang **Reveal State:**

```
┌──────────────────────────────────────────────────────┐
│                                                      │
│   ✅  13 tối ưu CR đã được áp dụng                 │
│                                                      │
│   Store [Brand name] đã sẵn sàng                   │
│                                                      │
│   CR Score ước tính: 84/100                         │
│   Top 20% trong Dropship stores                     │
│                                                      │
│   ────────────────────────────────────              │
│                                                      │
│   [ Xem store của bạn → ]          (CTA primary)   │
│                                                      │
└──────────────────────────────────────────────────────┘
```

**Behavior của Reveal State:**
- Fade transition từ loading feed sang reveal content
- CR Score "count up" animation: từ 0 → 84 trong ~1 giây
- CTA button xuất hiện sau khi số dừng lại (không xuất hiện đồng thời)
- Không có countdown timer — user tự quyết định khi nào click

---

## 5. Micro-copy guidelines

**Tone:** Chuyên gia kỹ thuật, không phải marketing. Dùng số liệu cụ thể. Tránh tính từ chung chung.

| Tránh | Dùng thay thế |
|-------|---------------|
| *"Đang tối ưu store tuyệt vời của bạn"* | *"Sticky Add-to-Cart bar khi scroll xuống reviews"* |
| *"AI đang làm việc cho bạn"* | *"Checkout form: Rút gọn xuống còn 7 fields thiết yếu"* |
| *"Sắp xong rồi!"* | *"13 tối ưu CR đã được áp dụng"* |
| *"Tăng doanh thu ngay hôm nay"* | *"Mỗi field thừa tăng abandon rate ~10%"* |

**Cấu trúc giải thích:** Luôn format theo pattern:
> *[Con số hoặc tên nguyên lý] — [Hệ quả với buyer behavior]*

Ví dụ đúng: *"68% quyết định mua xảy ra sau khi đọc reviews — CTA phải luôn trong tầm với tại thời điểm đó"*

---

## 6. Animation & Timing

| Sự kiện | Animation | Duration |
|---------|-----------|----------|
| Item mới xuất hiện | Fade in + slide up nhẹ | 200ms |
| Item chuyển từ ⟳ sang ✅ | Icon swap + màu chuyển xanh | 300ms |
| Progress bar tăng | Ease-in-out fill | Liên tục |
| Feed scroll khi item mới | Smooth scroll | 200ms |
| Chuyển sang Reveal State | Fade out feed → Fade in reveal | 400ms |
| CR Score count-up | Linear count 0→84 | 800ms |
| CTA button xuất hiện | Fade in sau khi số dừng | Delay 300ms |

---

## 7. Điều không làm

- Không dùng spinner vòng tròn trung tâm — thiếu thông tin, không build trust
- Không để feed scroll nhanh đến mức user không đọc được giải thích
- Không dùng tiến độ giả (fake progress) chạy nhanh rồi stuck ở 90% — gây frustration
- Không thêm illustration hay animation trang trí không liên quan đến nội dung
- Không show tất cả 13 items cùng lúc — mất đi hiệu ứng "đang làm việc cho bạn"
- Không dùng màu đỏ hay warning color trong loading — toàn bộ screen phải truyền cảm giác confident, chuyên nghiệp

---

## 8. Edge cases

**Nếu loading thực tế nhanh hơn script:** Thêm minimum display time 20 giây. Nếu hệ thống xong sớm hơn, giữ animation chạy đến khi hết script. Không bao giờ bỏ qua items — user cần đọc đủ.

**Nếu loading thực tế chậm hơn script:** Thêm item bổ sung như:
> *"Kiểm tra tốc độ load mobile..."*
> *"Nén và tối ưu hình ảnh sản phẩm..."*

Không để progress bar dừng ở một chỗ quá 5 giây.

**Nếu có lỗi trong quá trình gen:** Không hiển thị technical error. Hiển thị:
> *"Đang thử lại tối ưu [tên item]..."* — sau đó tiếp tục bình thường.
