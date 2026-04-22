# Store Screen — UI Specification
**Screen:** Preview Store với CR Highlights
**Dành cho:** AI UI Generator
**Version:** 1.0

---

## 1. Mục đích màn hình

User vừa trải qua loading screen — họ đã biết 13 tối ưu CR được áp dụng cho store. Màn hình này cho họ *nhìn thấy* những tối ưu đó trực tiếp trên store.

**Một câu mô tả:** Store được render đầy đủ, một số element được highlight tinh tế. User hover vào highlight → tooltip giải thích element đó đang giúp tăng CR như thế nào.

Không có panel sidebar. Không có score. Chỉ có store và highlights.

---

## 2. Layout

```
┌─────────────────────────────────────────────┐
│  [Homepage]  [Product Page]  [Checkout]      │  ← Tab bar
├─────────────────────────────────────────────┤
│                                             │
│                                             │
│            Store (full width)               │
│        với highlighted elements             │
│                                             │
│                                             │
└─────────────────────────────────────────────┘
```

- **Tab bar:** fixed top, không scroll theo trang
- **Store area:** full width, full height còn lại, có thể scroll
- Không có sidebar, không có panel phụ

---

## 3. Tab Bar

3 tab theo đúng thứ tự happy flow mua hàng:

```
[Homepage]   [Product Page]   [Checkout]
```

- Tab active: underline hoặc background tint, rõ ràng
- Click tab → store area render trang tương ứng, scroll về top
- Default khi vào màn hình: tab **Homepage** active

---

## 4. Highlight System

### 4a. Visual của highlight

Mỗi element được tối ưu CR có một **highlight ring** bao quanh:

- **Border:** 2px, màu accent (ví dụ: xanh lam `#3B82F6` hoặc màu primary của design system)
- **Border radius:** inherit từ element — nếu element bo góc thì highlight cũng bo góc
- **Background overlay:** không có — highlight chỉ là border, không che nội dung
- **Glow nhẹ:** box-shadow `0 0 0 4px rgba(accent, 0.15)` — tạo cảm giác "được chọn" mà không quá nổi
- **Không dùng màu cảnh báo (đỏ, cam, vàng)** — highlight phải truyền cảm giác tích cực

### 4b. Badge indicator

Mỗi highlighted element có một **badge nhỏ** đặt tại góc trên phải của element:

```
[⚡ CR]
```

- Hình dạng: pill nhỏ
- Màu: cùng màu accent với highlight border
- Icon: ⚡ hoặc icon CR phù hợp với design system
- Text: "CR" — ngắn, không giải thích thêm
- Mục đích: thu hút mắt user vào element đó

### 4c. Cursor

Khi hover vào bất kỳ highlighted element nào, cursor đổi sang `help` hoặc `pointer` — signal rõ ràng "có thể tương tác".

---

## 5. Tooltip

### 5a. Trigger

- **Trigger:** hover vào highlighted element (cả badge và element đều trigger)
- **Delay xuất hiện:** 150ms sau khi hover — đủ để tránh tooltip flicker khi chuột di chuyển ngang
- **Dismiss:** chuột rời khỏi element → tooltip fade out sau 100ms

### 5b. Visual của tooltip

```
┌──────────────────────────────────┐
│  [Icon]  Tên element             │
│  ──────────────────────────────  │
│  Giải thích ngắn tại sao         │
│  element này giúp tăng CR,       │
│  dùng số liệu cụ thể.            │
└──────────────────────────────────┘
```

- **Width:** 280–320px, không co lại theo content
- **Background:** dark (`#1A1A1A` hoặc neutral dark) — tương phản tốt với mọi màu store
- **Text màu:** trắng `#FFFFFF` cho tên, `rgba(255,255,255,0.75)` cho giải thích
- **Border radius:** 8px
- **Shadow:** `0 8px 24px rgba(0,0,0,0.2)`
- **Padding:** 14px 16px
- **Animation:** fade in + translate lên 4px, duration 150ms, easing ease-out

### 5c. Vị trí tooltip

- **Default:** xuất hiện phía trên element, căn giữa theo chiều ngang
- **Nếu không đủ chỗ phía trên:** flip xuống dưới element
- **Nếu gần mép phải màn hình:** align right
- **Không bao giờ bị crop bởi viewport**

---

## 6. Nội dung tooltip — Homepage (6 elements)

---

**Element 1 — Template layout tổng thể**
Badge đặt tại: top-right của hero section

```
Icon: 🏗️  Template tỷ lệ chuyển đổi cao

Template được chọn dựa trên cấu trúc đã
kiểm chứng với hàng ngàn Dropship stores.
```

---

**Element 2 — Cấu trúc trang**
Badge đặt tại: top-right của navigation bar

```
Icon: 🎯  Cấu trúc dành riêng cho Dropship

Store Dropship cần layout khác POD —
buyer behavior và điểm quyết định mua khác nhau.
```

---

**Element 3 — Hero headline**
Badge đặt tại: top-right của headline text block

```
Icon: ⏱️  Value proposition trong 5 giây đầu

68% buyer quyết định ở lại hay rời đi trong
khoảng này. Headline đặt tại F-pattern hotspot,
trong viewport đầu tiên.
```

---

**Element 4 — CTA button chính**
Badge đặt tại: top-right của button

```
Icon: 👆  Contrast ratio 5.2:1

Đạt ngưỡng tối ưu click-through theo WCAG AA.
Button mờ là nguyên nhân phổ biến nhất
của low CTR trên hero section.
```

---

**Element 5 — Shipping estimate**
Badge đặt tại: top-right của dòng text shipping

```
Icon: 📦  Thời gian giao hàng gần CTA

Shipping time là rào cản mua #1 với Dropship
buyer. Đặt trong 200px từ CTA — Shopify data:
CTR tăng 22% khi có shipping estimate gần button.
```

---

**Element 6 — Trust badges row**
Badge đặt tại: top-right của khu vực badges

```
Icon: 🛡️  4 trust signals trước khi scroll

Secure Payment · Free Return · Tracked Shipping
· 24/7 Support. Baymard: 61% buyers abandon vì
thiếu trust signals tại điểm quyết định đầu tiên.
```

---

## 7. Nội dung tooltip — Product Page (4 elements)

---

**Element 7 — Price anchoring**
Badge đặt tại: top-right của khu vực giá

```
Icon: 💰  Price anchor tạo perceived value

Giá gốc gạch ngang cạnh giá sale. Buyer cảm
nhận "đang được deal" ngay cả khi không so sánh.
Tăng perceived value trung bình 17%.
```

---

**Element 8 — Sticky Add-to-Cart bar**
Badge đặt tại: top-right của sticky bar

```
Icon: 📌  CTA luôn trong tầm với

68% quyết định mua xảy ra sau khi đọc reviews.
Sticky bar đảm bảo CTA không bao giờ out-of-view
tại thời điểm buyer sẵn sàng mua.
```

---

**Element 9 — Stock indicator**
Badge đặt tại: top-right của dòng stock

```
Icon: ⚡  Scarcity signal gần CTA

"Còn X sản phẩm" tăng add-to-cart rate ~12%.
Đặt trong 80px từ ATC button. Hiệu quả nhất
với impulse purchase của Dropship buyer.
```

---

**Element 10 — Review stars gần giá**
Badge đặt tại: top-right của star rating

```
Icon: ⭐  Social proof cạnh price

Eye-tracking flow: Title → Stars → Price → ATC.
Review đặt gần giá giảm price objection 19%
so với đặt ở cuối trang.
```

---

## 8. Nội dung tooltip — Checkout (3 elements)

---

**Element 11 — Form fields rút gọn**
Badge đặt tại: top-right của form container

```
Icon: ✂️  7 fields thiết yếu

Loại bỏ mọi field không cần thiết. Baymard:
mỗi field thừa tăng abandon rate ~10%.
7 fields vs 12 fields = giảm ~50% form-induced abandon.
```

---

**Element 12 — Progress bar checkout**
Badge đặt tại: top-right của progress indicator

```
Icon: 🗺️  Buyer biết còn bao xa

3 bước: Thông tin · Vận chuyển · Thanh toán.
Progress indicator giảm drop-off giữa chừng 18% —
không ai muốn bỏ cuộc khi đã đi được nửa đường.
```

---

**Element 13 — Trust badges + payment logos**
Badge đặt tại: top-right của khu vực payment trust

```
Icon: 🔒  Trust tại high-anxiety moment

Visa · Mastercard · PayPal + lock icon đặt ngay
trên nút thanh toán. Trust signals đặt đúng vị trí
này giảm abandon tại bước thanh toán ~15%.
```

---

## 9. Behavior — Trạng thái và animation

### Khi màn hình load lần đầu
1. Store render — 0ms
2. Highlights (border + glow) fade in đồng loạt — delay 400ms, duration 300ms
3. Badges xuất hiện sau highlights — delay 700ms, duration 200ms, staggered 50ms mỗi badge
4. Không có hướng dẫn overlay, không có onboarding tooltip — user tự khám phá

### Khi switch tab
1. Store area fade out nhẹ (opacity 0, 150ms)
2. Render trang mới
3. Store area fade in (opacity 1, 150ms)
4. Highlights và badges của trang mới fade in giống lần load đầu

### Khi hover highlight
1. Glow của element tăng nhẹ — `box-shadow` rộng hơn, opacity cao hơn
2. Badge scale lên 1.1x
3. Tooltip xuất hiện sau 150ms delay

### Khi không hover
- Highlights và badges hiển thị bình thường, không pulse, không animation liên tục
- Chỉ static — không làm phân tâm khi user đọc nội dung store

---

## 10. Điều không làm

- **Không animate highlight liên tục (pulse, blink)** — gây distraction khi user đang đọc store
- **Không hiện tooltip ngay lập tức khi hover** — cần 150ms delay để tránh flicker
- **Không stack nhiều tooltip cùng lúc** — mỗi thời điểm chỉ có 1 tooltip visible
- **Không dùng màu đỏ/cam/vàng cho highlight** — phải là màu tích cực, không phải cảnh báo
- **Không che nội dung store bằng overlay** — highlight là border, không phải mask
- **Không tự động scroll sang tab tiếp theo** — user tự quyết định khi nào chuyển trang
