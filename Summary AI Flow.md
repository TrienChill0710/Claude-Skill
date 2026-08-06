# TỔNG QUAN QUY TRÌNH THIẾT KẾ UI/UX BẰNG AI & HTML (CODE-FIRST WORKFLOW)

> **Tài liệu Tóm tắt (Handoff Summary)**  
> Tổng hợp chi tiết về quy trình phối hợp giữa **Designer (Con người)** và **AI Assistant**, giải thích bản chất file HTML Mockup, đánh giá Ưu/Nhược điểm và cơ chế quản lý **Design System (DS)** 100% bằng AI.

---

## 1. Tổng quan Quy trình (Overview)

Quy trình này thay thế cách làm truyền thống (vẽ trên Figma) bằng mô hình **Code-first / AI-assisted UI-UX Workflow**. Trong đó:
* **Figma Canvas** được thay thế bằng **File HTML/CSS Mockup** (đóng vai trò làm *Ground Truth* - Bản mẫu chuẩn trực quan).
* **Viết Spec Handoff thủ công** được thay thế bằng **AI Pipeline tự động audit & sinh tài liệu Markdown (`SCREEN-*.md`)**.

---

## 2. Phân định Vai trò (Human vs AI)

* **Designer (Con người):**
  * Không cần tự viết các tài liệu kỹ thuật/Markdown.
  * Mở file `.html` mockup và **tập trung 100% vào sáng tạo & tinh chỉnh visual** (màu sắc, layout, spacing, copy...).
  * Duyệt kết quả và chỉ đạo AI ở từng bước.

* **AI Assistant (Claude/Antigravity):**
  * Đọc Wireframe từ domain để sinh mockup HTML ban đầu.
  * Audit 2 chiều giữa Mockup HTML và Design System (Tokens & Components).
  * Viết & cập nhật các file tả thiết kế (`SCREEN-*.md`, `COMP-*.md`).
  * Sinh file đối chiếu `GEN-CHECK-*.html` để chụp ảnh so sánh pixel-level.
  * Ghi vết nhật ký thay đổi vào `Execution/tracking/decisions.md`.

---

## 3. Quy trình 3 Bước Lặp lại (3-Step Loop)

```
[PO/BA Sync WIRE mới]
          │
          ▼
 BƯỚC 1 — Gen Mockup (Prompt cho AI)
 ──► AI đọc Wireframe ──► Dựng file HTML mockup chuẩn Design System
          │
          ▼
 BƯỚC 2 — Bạn Edit Visual (Thủ công)
 ──► Sửa trực tiếp trên file HTML — màu, layout, spacing, copy...
          │
          ▼
 BƯỚC 3 — Full Pipeline Handoff (Prompt cho AI)
 ──► AI Audit Token/Component ──► Viết SCREEN-*.md ──► Chạy GEN-CHECK verify ──► Handoff Dev
```

---

## 4. Bản chất của File `.html` Mockup

* **Không phải Code FE Production đầy đủ:** File `.html` mockup không chứa logic nghiệp vụ phức tạp, kết nối API backend hay quản lý state (React/Vue/Angular).
* **Là Bản thiết kế mẫu trực quan (Visual Prototype):** Đây là mã HTML/CSS thật chạy trên trình duyệt, thay thế cho file thiết kế Figma. 
* **Vai trò:** Làm căn cứ chuẩn 100% để AI quét ra tài liệu Spec và để Developer dựa vào đó code lại vào codebase chính của dự án.

---

## 5. Đánh giá Ưu điểm & Nhược điểm (So với Figma)

### 🟢 Ưu điểm
1. **Độ chính xác 100% (Zero Discrepancy):** Màu sắc, spacing, flexbox, font rendering... trùng khớp 100% với CSS thật.
2. **Tốc độ cực nhanh nhờ AI:** AI dựng khung mockup từ Wireframe trong vài giây và viết tự động 100% tài liệu Handoff.
3. **Quản lý Phiên bản chặt chẽ (Git):** Dễ dàng commit, branch, diff lịch sử thiết kế dưới dạng text/code.
4. **Ép tuân thủ Design System:** Hạn chế tình trạng Designer tự vẽ màu/cỡ chữ ngẫu hứng không thuộc hệ thống.

### 🔴 Nhược điểm
1. **Rào cản kỹ thuật nhẹ:** Designer cần biết thao tác cơ bản với HTML/CSS hoặc Chrome DevTools.
2. **Khó Brainstorming phác thảo nhanh ở giai đoạn đầu:** Figma tốt hơn ở khoản phác thảo 10-20 ý tưởng kéo-thả cạnh nhau trên canvas rộng.
3. **Thiếu Live Collaboration đồ họa:** Không có tính năng multiplayer cursor/comment trực tiếp trên giao diện như Figma.
4. **Phụ thuộc vào Design System & AI Rules ban đầu:** Cần có quy tắc AI (`agent-ds-author.md`) được thiết lập chuẩn.

---

## 6. Giải pháp Quản lý Design System (DS) 100% bằng AI

### 6.1 Nguồn gốc Design System trong Code Workflow
1. **Dùng Thư viện Code mở:** Sử dụng sẵn bộ Tokens/Component từ Tailwind, Shadcn/UI, Ant Design HTML...
2. **Export từ Figma có sẵn:** Export bộ Design Tokens (Variables: CSS/JSON) từ Figma sang dự án.
3. **Bootstrap từ Màn hình Mẫu:** Tạo 1-2 màn hình APPROVED ban đầu, AI tự trích xuất thành `component-gallery.html` và bộ Token CSS.

### 6.2 Cơ chế ép AI tuân thủ 100% Design System
* **Index-first Prompting:** Ép AI luôn `grep` kiểm tra `component-gallery.html` trước khi định tạo component mới.
* **Gắn Metadata Attribute:** Mọi element đều được gắn `data-ds-component="X"` và `data-ds-variant="Y"`.
* **Audit 2 chiều & GEN-CHECK:** Bước 3 của pipeline sẽ tự động quét phát hiện các màu/margin hardcode không chuẩn token và bắt AI sửa lại.

### 6.3 Cơ chế Tiến hóa Động (Evolutionary Design System)
> **Giải quyết thắc mắc:** *"1-2 màn hình đầu tiên không thể có đủ hết Component cho toàn dự án!"*

* **1-2 màn đầu:** Thiết lập **"Bộ Gen Visual" (Tokens & Core Foundations)**: Bảng màu, typography, spacing, border-radius, layout gốc.
* **Khi gặp Component MỚI ở các màn sau:**
  1. AI phát hiện Component chưa có trong `component-gallery.html`.
  2. AI dựng Component mới nhưng **kế thừa 100% Token sẵn có** từ "Bộ Gen Visual" gốc (đảm bảo ăn khớp visual).
  3. Designer mở HTML kiểm tra & chỉnh sửa visual theo ý muốn.
  4. AI tự động **đăng ký ngược (Auto-registration)** Component mới này vào `component-gallery.html` để các màn sau tái sử dụng.

---
*Tài liệu này tổng hợp toàn bộ thảo luận về quy trình UI/UX AI Flow.*
