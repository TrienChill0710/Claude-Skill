# Loading Screen — Content & Behavior Specification
**Screen:** Store Generation Loading Screen
**Business Model:** Dropship
**Version:** 2.0 — Layout-free (dành cho AI designer tự quyết định layout)

---

## 1. Mục đích màn hình

Màn hình này xuất hiện sau khi user điền thông tin (brand name, business model) và nhấn "Tạo store". Hệ thống đang chọn template và áp dụng các tối ưu CR.

**Mục tiêu chính:** Không phải màn hình chờ. Đây là màn hình chứng minh năng lực của hệ thống. Khi user xem xong, họ phải cảm thấy: *"Hệ thống này thực sự hiểu conversion rate, không phải chỉ tạo template đẹp."*

**Cơ chế build trust:** Mỗi item hiện ra phải làm đồng thời 2 việc:
1. Nói hệ thống đang làm **gì cụ thể** — hành động có tên, đặt tên được
2. Giải thích ngắn **tại sao** hành động đó quan trọng với CR — dùng con số hoặc nguyên lý cụ thể

Khi user vào store xong, họ sẽ nhận ra từng element đã được đề cập — trust được build retroactively.

---

## 2. Các thành phần bắt buộc trên màn hình

Màn hình phải chứa đủ 4 thành phần sau. Layout, vị trí, kích thước là quyết định của designer.

### Thành phần 1 — Brand context
Hiển thị brand name user đã điền. Mục đích: tạo cảm giác cá nhân hóa, user thấy đây là store *của mình* đang được chuẩn bị, không phải demo chung.

### Thành phần 2 — Tiến trình tổng thể
Một chỉ báo thể hiện % hoàn thành tổng thể, cập nhật theo số items đã xong trong script. Mục đích: user biết còn bao lâu, không bị anxiety khi chờ.

### Thành phần 3 — Activity log (quan trọng nhất)
Danh sách các tối ưu đang/đã được áp dụng, xuất hiện tuần tự. Mỗi item gồm:
- **Tiêu đề:** tên hành động cụ thể
- **Giải thích:** tại sao quan trọng với CR

Mỗi item có 3 trạng thái:
- **Đã hoàn thành:** icon thành công, hiển thị rõ
- **Đang chạy:** icon loading/progress, được highlight để thu hút chú ý
- **Chưa đến:** chưa xuất hiện — không render trước

Items xuất hiện tuần tự từng cái một. Không hiện tất cả cùng lúc.

### Thành phần 4 — Reveal State (trạng thái kết thúc)
Sau khi tất cả items hoàn thành, màn hình chuyển sang trạng thái kết thúc gồm:
- Tổng kết số tối ưu đã áp dụng: *"13 tối ưu CR đã được áp dụng"*
- CR Score ước tính với animation count-up (ví dụ: 0 → 84/100)
- Benchmark context: *"Top 20% trong Dropship stores"*
- Một CTA duy nhất để vào store

CTA chỉ xuất hiện sau khi CR Score dừng lại — không xuất hiện đồng thời.

---

## 3. Script đầy đủ — Business Model: Dropship

Tổng 13 items, chia 6 giai đoạn. Thời gian mỗi item: 1.5–2.5 giây. Tổng loading: ~25–35 giây.

---

### Giai đoạn 1 — Chọn nền tảng

**Item 1**
> **Tiêu đề:** Chọn template Dropship tỷ lệ chuyển đổi cao nhất
> **Giải thích:** Template được chọn dựa trên cấu trúc đã kiểm chứng với hàng ngàn Dropship stores

*Đây là item duy nhất nhắc đến "template" — nói thẳng, không che giấu. Trust được tạo bằng sự minh bạch.*

**Item 2**
> **Tiêu đề:** Nhận diện ngành hàng và đối tượng mua của bạn
> **Giải thích:** Store Dropship cần cấu trúc khác với POD hay niche store — buyer behavior khác nhau

---

### Giai đoạn 2 — First Impression

**Item 3**
> **Tiêu đề:** Tối ưu hero section: Value proposition hiện trong 5 giây đầu
> **Giải thích:** 68% buyer quyết định ở lại hay rời đi trong khoảng này — mỗi giây đều tính

**Item 4**
> **Tiêu đề:** CTA button: Contrast ratio 5.2:1 với background
> **Giải thích:** Đạt ngưỡng tối ưu click-through — button mờ là nguyên nhân phổ biến nhất của low CTR

---

### Giai đoạn 3 — Trust Layer

*Dropship buyer có 2 lo ngại chính: hàng có đến không, bao lâu. Giai đoạn này giải quyết cả 2.*

**Item 5**
> **Tiêu đề:** Thêm shipping estimate rõ ràng tại hero section
> **Giải thích:** "Nhận hàng trong X ngày" gần CTA chính — shipping time là rào cản mua #1 với Dropship buyer

**Item 6**
> **Tiêu đề:** Đặt 4 trust badges tại vị trí above-the-fold
> **Giải thích:** Secure Payment · Free Return · Tracked Shipping · 24/7 Support — giảm lo ngại trước khi buyer scroll xuống

---

### Giai đoạn 4 — Product Page

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

### Giai đoạn 5 — Checkout

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

### Giai đoạn 6 — Reveal State

Sau item 13, dừng ~1 giây rồi chuyển sang Reveal State với nội dung:

- *"13 tối ưu CR đã được áp dụng"*
- *"Store [Brand name] đã sẵn sàng"*
- CR Score với animation count-up: `84/100`
- Benchmark: *"Top 20% trong Dropship stores"*
- CTA: *"Xem store của bạn →"*

---

## 4. Micro-copy guidelines

**Tone:** Chuyên gia kỹ thuật, không phải marketing. Dùng số liệu cụ thể. Tránh tính từ chung chung.

| Tránh | Dùng thay thế |
|-------|---------------|
| *"Đang tối ưu store tuyệt vời của bạn"* | *"Sticky Add-to-Cart bar khi scroll xuống reviews"* |
| *"AI đang làm việc cho bạn"* | *"Checkout form: Rút gọn xuống còn 7 fields thiết yếu"* |
| *"Sắp xong rồi!"* | *"13 tối ưu CR đã được áp dụng"* |
| *"Tăng doanh thu ngay hôm nay"* | *"Mỗi field thừa tăng abandon rate ~10%"* |

**Cấu trúc câu giải thích:** Luôn theo pattern:
> *[Con số hoặc tên nguyên lý] — [Hệ quả với buyer behavior]*

---

## 5. Timing

| Sự kiện | Thời lượng |
|---------|------------|
| Mỗi item (từ xuất hiện đến hoàn thành) | 1.5–2.5 giây |
| Tổng loading | ~25–35 giây |
| Dừng sau item cuối trước khi chuyển Reveal | ~1 giây |
| CR Score count-up animation | ~800ms |
| CTA xuất hiện sau khi số dừng | Delay 300ms |

---

## 6. Điều không làm

- Không hiện tất cả 13 items cùng lúc — mất đi hiệu ứng "đang làm việc cho bạn"
- Không dùng fake progress chạy nhanh rồi stuck — gây frustration
- Không bỏ qua items để loading nhanh hơn — user cần đọc đủ để build trust
- Không hiện CTA trước khi Reveal State hoàn tất
- Không dùng màu cảnh báo (đỏ, cam) trong quá trình loading — toàn bộ screen phải truyền cảm giác confident

---

## 7. Edge cases

**Loading thực tế nhanh hơn script:** Giữ minimum display time 20 giây. Chạy hết script trước khi vào Reveal State.

**Loading thực tế chậm hơn script:** Thêm item padding như:
> *"Kiểm tra tốc độ load mobile..."*
> *"Nén và tối ưu hình ảnh sản phẩm..."*

Không để chỉ báo tiến trình dừng quá 5 giây.

**Nếu có lỗi:** Không hiển thị technical error. Hiển thị:
> *"Đang thử lại tối ưu [tên item]..."* — sau đó tiếp tục bình thường.
